## Reflection

### a. How much data your publisher program will send to the message broker in one run?

In one run, the publisher program will send **5 events** to the message broker.

If we look at the `main.rs` code for the publisher provided in the tutorial, we can see that the `publish_event` method is called 5 separate times within the `main` function. Each call creates and sends a new `UserCreatedEventMessage` containing a different `user_id` and `user_name`.

### b. The url of: "amqp://guest:guest@localhost:5672" is the same as in the subscriber program, what does it mean?

Because the publisher and subscriber are two completely separate and independent programs , they don't send data directly to each other. Instead, they both rely on a "middleman" to handle the communication. In this case, it's the RabbitMQ message broker.

Using the exact same URL means that both programs are connecting to the exact same RabbitMQ message broker instance running on my machine.

* The publisher uses this connection to drop off the 5 events to the broker.
* The subscriber uses this connection to listen to the broker and consume the events that the publisher just dropped off.

If they had different URLs, they would be talking to different message brokers and wouldn't be able to communicate with each other!


### RabbitMQ Screen

![RabbitMQ](images/rabbitmq_screen.png)


### Running Subscriber and Publisher

- **Publisher**
![publisher](images/publisher.png)

- **Subscriber**
![subscriber](images/subscriber.png)

After I run the publisher app, it immediately sent 5 events. Then, the subscriber app received those 5 events.