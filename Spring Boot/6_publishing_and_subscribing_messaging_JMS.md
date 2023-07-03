# Java Message Service (JMS)

JMS is an API for controlling Message-Oriented Middleware(MOM). It enables loosely coupled, asynchronous communication between the components of a distributed application. 

## JMS Domians

It has two approaches:

- **Point-to-Point (PTP)**: allows clients to send messages to another client through **abstractions** called `queues`.
    - The client that sends the message sends it to a queue.
    - The clients that receives the message extracts it from a queue. 

- **Publish and Subscribe (pub/sub)**: allows sending messages to multiple clients via an intermediate abstraction called topics.
    - The client that sends the messages, publishes it to a specific topic.
    - The message is delivered to all clients that are subscribed to the topic.

### Work Flow of JMS Programming Model

- `ConnectionFactory` creates **connection** which creates a **session**, which creates messages based on the approach selected.

- Some JMS providers used for controlling sessions, queues and topics:

    - ActiveMQ
    - Fuse MQ
    - Apollo
    - Qpid
    - JORAM
    - MantaRay

### Spring JMS

Use jmsTemplate

```java
// blah blah blah 

    @Bean
    public JmsTemplate jmsTemplate(){
        JmsTemplate template = new JmsTemplate();
        template.setConnectionFactory(connectionFactory());
        template.setDefaultDestinationName(MESSAGE_QUEUE);
        return template;
    }

    @Bean 
    MessageConverter converter(){
        return new SimpleMessageConverter();
    }
``` 

# Advanced Message Queuing Protocol (AMQP)

- AMQP is an open standard binary application layer protocol. 

- It is independent of the programming language.
- All method of JMS has been integrated into AMQP.


Spring AMQP features:

- Applies core Spring concept

- Provides a template as an abstraction for sending and receiving data.

- Provides support for message-driven POJOs.

- Support publisher confirmations/consumer acknowledgements. 

- AmqpAdmin: Tool that supports basic operations. 

# RabbitMQ Broker

- Spring AMQP provides generic abstractions that do not rely on any particular AMQP broker implementation or client library. 

- RabbitMQ implementation 

Spring AMQP Messaging:

- Message 

- Exchanges: 
    - Direct
    - Fanout
    - Topic
    - Headers 

- Queue

- Binding 

- In the controller, add the RabbitMQ beans and work. RabbitMQ works in 5672. 


# Using Redis as a messaging System 

- Spring Data Redis provodes easy configuration and access to the Redis NoSQL database from Spring applications. It also offers Low level and High Level abstraction for interacting with the store. 


- Spring Data Redis is driven by a keystore-based data structure and can be used as a database, cache, or message broker. 

Features: 

- Connection package is low-level abstraction

- RedisTemplate provides a high-level abstraction for performing various operations, exception translation, and serialization support. 

- Pub/sub support 

- Redis Sentinel and Redis Cluster support. 

- Mapping serializers for JDK, string, JSON, Spring Object/XML

- Sorting and pipelining

- Automatic implementation of repository interfaces, including support for custom finder methods using `@EnableRedisRepositories`. 

- CDI support for repositories. 


> For fast development use: 
    - `spring-boot-devtools` 

