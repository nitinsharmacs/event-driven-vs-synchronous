tags: #systems #architecture #research

# Event Driven and Synchronous Systems

## Abstract

Increasing size and complexity of softwares require a suitable system design to make system reliable, maintainable and performant. Selecting a design totally depends upon the system requirements and constraints such as performance, uptime, etc.
Synchronous and Event driven system are two designs commonly used in softwares.

Synchronous systems, characterised by waiting for responses, offer real-time data and straightforward implementation. However, they might get drawn back by their tight coupling of processes and overall speed.

In contrast, event-driven systems leverage events to communicate, leading performance and loose coupling. Nonetheless, they introduce complexities and require careful consideration of eventual consistency. The selection between these two approaches can be done through evaluation of specific requirements and trade-offs. 

This paper provides a comprehensive analysis of the strengths, weaknesses, and considerations associated with synchronous and event-driven systems.

## Goal

The goal of this paper is to provide information about
Synchronous and Event-Driven systems in conceptual and architectural perspective.

## Synchronous Systems

A synchronous system refers to a system in which various operations, such as communication, data processing, data transfer, or process execution, happen in a blocking or waiting manner. In other words, the system operates in a synchronized and coordinated fashion, where each operation blocks or pauses the execution until it finishes.

An analogy could be a phone call where each party has to wait for other to finish responding.

![Synchronous systems](./images/synchronous-systems.jpg 'Synchronous execution')

One of the application of synchronous systems are in microservice architecture, where services communicate through REST API or some other methods using HTTP calls, client service has to wait for the response from the server and execution moves forwards once the response comes back.

Let's see some of the synchronous systems implementations.

### Implementations

1. REST (Representational State Transfer) APIs
2. RPC (Remote Procedural Call)
3. GraphQL (Graph Query Language)

#### REST APIs

REST APIs are the interfaces provided by services or applications where other services can send requests to. It is the conventional and easy method for inter-service communication.

Each of the service has its own web server which provides endpoints where other services can send requests.

![REST API call](./images/rest-api.jpeg)

Considering the example of an E-commerce website, client (browser) sends the request to get all products data from the server. Client has to wait for the response from the server and then only client can show all the products. It makes this method of communication synchronous as there is a blocking of execution.

#### Remote Procedure Call

REST APIs are the way to access services provided by the server by using request/response mechanism. This method can be used for inter-service communication. However, using REST APIs as solely method of communication has its own limitations. Some of them are described below.

1. No defined request/response schema.
2. Communication payload can be bulky.

Following diagram shows how services interact using RPC mechanism.

![gRPC](./images/grpc.jpeg)

Figure shows that client and server are interacting using gRPC (Google RPC implementation). When the client sends request to server, client has to wait for the response. Until then client has to block its execution for that request.

Let's see one more way where services interact synchronously.

#### GraphQL

This is a data query and manipulation language. It gets the request from the clients as a form of a query, it parses and resolves the query and send back the response.

Unlike REST APIs, the query has defined schema about what all attributes to send in response. It makes the payload less bulky and only contains the required information.

**GraphQL is a specification** and it can be implemented in different languages such as Javascript, Java, C, C++, Python, etc.

Following figure shows multiple clients sending query to GraphQL server which in turn talks with DB services and other services.

![GraphQL](./images/graphql.jpeg)

Mostly communication is done synchronously using request/response model. However, it provides a mechanism of **Subscription** where clients can get real time updates asynchronously.

So, these were some of the implementations of synchronous communication. Some of them are evolving to provide asynchronous functionality which makes the interaction much effective and performative.

Now, let's examine some of the drawbacks of synchronous communication.

### Benefits of Synchronous Systems

- Simple structure

  Synchronous systems are easier to understand and implement,
  as the parts required for communication are only requester and responder.

- Realtime

  Synchronous systems are blocking such that the data that the client receives will always be realtime.

- Easy - Debugging

  Testing and debugging Synchronous systems is easy, and as the flow of execution is sequential, trace back of errors that occur is easy, correct and testable.

- Single source of truth

  The Systems can maintain single source of truth for data and memory as Synchronous systems will not have multiple actions at the same time

### Drawbacks of Synchronous Systems

- Autonomous micro services

  When there is a complex network of HTTP request/response among micro services, it makes those services less autonomous.

- System Resilience

  It is the ability of a service to provide responses to the client requests even in the face of adversity.
  When micro services have dense network of HTTP request/response and if any service fails, the dependent services may not provide favourable outcomes.

- Slow system

  One microservice has to wait for downstream service for the response. This makes the overall request/response process slow. It becomes worse if there is a chain of those requests.

### When to use Synchronous Systems ?

- Immediate response

  Synchronous system is appropriate for actions such as login and purchase, in which the caller must have a reply in order to proceed.

- Accessing shared data

  When microservices need to access shared data stored in a database, synchronous communication is often used through direct database queries. Microservices can make synchronous requests to the database to fetch, update, or delete data.

- Dependent tasks

  To perform tasks that depend on each other, synchronous systems are useful. For example, a telephone conversation While one person speaks, the other listens. When the first person finishes, the second tends to respond immediately.

- Responsive and interactive experience

  Synchronous systems are frequently employed in user interfaces and web applications to provide a responsive and interactive experience. When a user performs an action, such as submitting a form or making a request, synchronous communication ensures that the user receives immediate feedback or a response.

- consistency and integrity

  Synchronous systems are commonly used in financial applications to ensure the consistency and integrity of transactions. When transferring funds, making payments, or conducting real-time trading, synchronous communication guarantees that all steps are completed and verified before proceeding.

- coordinating complex workflows

  Synchronous systems can be useful for coordinating complex workflows involving multiple microservices. By employing synchronous communication, each microservice can wait for the completion of a specific step or task before executing its own actions, ensuring proper sequencing and coordination.

- Real-Time Collaboration

  Synchronous systems are ideal for real-time collaboration scenarios, where multiple users need to work together simultaneously. Examples include collaborative document editing, shared whiteboards, or real-time chat applications. Synchronous communication enables immediate updates and feedback, allowing users to see changes made by others in real-time.

## Event-Driven Systems

Event-driven systems, are systems that uses events to trigger and communicate between decoupled services where an **event** is change in state. For instance, suppose there is a system that has two microservices, A and B, with A allowing users to configure a car and B storing that data in a database. If the user modifies configuration details in service A, it will trigger an event and tell service B about the change in the configuration of the car. Then service B fetches new data from service A and updates the database through event broker.

![Event-Driven System](./images/event-driven-system.jpg)

An event broker is a system that acts as an intermediary between event producer and consumer, it receives event from producer and transmits them to consumer.

Event-driven system typically consists of

- Event producer (agents)
- Event consumers (sinks)
- Event channels.

In the above example, service A is an event producer, and service B is an event consumer. **Event channel** refer to the pathway through which events flow it may be a queue or an event grid.

### Implementations

Implementing event-driven systems can be done in various ways, depending on the specific requirements and technologies you're using. Here are a few common approaches to consider:

1. Observer pattern :

   The observer pattern is a classic design pattern used to establish a one-to-many relationship between objects. In this pattern, an event source (subject) maintains a list of observers (listeners) and notifies them whenever an event occurs. Observers can then respond to the event accordingly. This pattern is often used in object-oriented programming languages.

![Observer Pattern](./images/observer-pattern.jpeg)

2. Message queues and brokers :

   Message queues and brokers provide a mechanism for decoupling components in an event-driven system. Components can publish events to a message queue, and other components can subscribe to the queue to receive and process those events asynchronously. Popular message brokers include Apache Kafka, RabbitMQ, and Amazon Simple Queue Service (SQS).

![Message queues and broker](./images/message-queue.jpeg)

3. Reactive programming :

   Reactive programming is a programming paradigm that deals with asynchronous data streams and event propagation. It emphasizes the use of reactive streams and operators to handle and transform events in a declarative manner. Reactive frameworks like RxJava, Reactor, and Akka provide powerful tools for building event-driven systems.

4. Event sourcing and CQRS :

   Event sourcing is a technique where changes to an application's state are captured as a sequence of events. Instead of persisting the current state, you persist the events that lead to that state. Combined with Command Query Responsibility Segregation (CQRS), you can separate the write (command) and read (query) models of an application. This approach allows you to maintain a full history of events and easily implement features like event replay and auditing.

5. Webhooks :

   Webhooks are a simple and popular way to implement event-driven systems in web applications. With webhooks, you define specific URLs in your application that other services can call when specific events occur. The receiving application can then process the event payload and take appropriate actions. Webhooks are commonly used for integrating third-party services and triggering actions based on external events.

![Webhooks](./images/webhooks.jpeg)

These are just a few examples of how you can implement event-driven systems. The choice of approach depends on the complexity of your system, the technologies you're using, and the specific requirements you have for event handling and propagation.

### Benefits of Event-Driven Systems

- Loose coupling

  In above example we have seen that service A is not aware of existence of service B, so making changes to any service will not affect communication between them and services can evolve independently.

- Resilience

  Let say service B is down for some reason, the producer service that is service A can till send message to the queue without interruption. The service B can pick up that message and processes that once it is up and running.

- Performance

  The sender service doesn't need to wait for the response of the receiving service, so it saves time and the sender service can proceed with its other tasks, which improves the system's overall performance.

- System extensibility

  New microservices can be added to the architecture without requiring changes to existing microservices that is service A and B.

- Cut costs

  Event-driven systems are push-based, so everything happens on-demand as the event presents itself in the router. This way, you’re not paying for continuous polling to check for an event. This means less network bandwidth consumption, less CPU utilization, less idle fleet capacity, and less SSL/TLS handshakes.

### Drawbacks of Event-Driven Systems

- Complexity

  Event-driven systems can introduce additional complexity compared to more traditional synchronous systems. The asynchronous nature of event-driven communication requires careful design and handling of events, event ordering, event schemas, and event-driven workflows. This complexity can make the system more challenging to develop, test, and maintain.

- Inconsistency

  Event-driven systems often rely on eventual consistency, meaning that the system's state might not be immediately consistent across all microservices. It can take time for events to propagate and for all subscribers to process and react to events. This can lead to temporary inconsistencies or race conditions in the system, which need to be carefully managed.

- Over-engineering of processes

  Sometimes a simple call from one service to another is enough. In event-driven systems, it usually requires much more infrastructure to support it, which will add costs like need of queueing system.

- Testing

  Testing and debugging event-driven systems can be more complex than traditional systems. Ensuring proper event ordering, verifying the correctness of event-driven workflows, and simulating different event scenarios for testing can be challenging.

- Debugging

  To debug event-driven systems need advance tooling and techniques.

### When to use Event-Driven systems ?

- Monitoring and alerting

  Rather than continuously checking on your resources, we can use event-driven systems for monitoring and alerting on any anomalies, changes, and updates.

- Parallel processing

  If we need to perform multiple operations on the same data, for instance, we want to store user input in the database and also pass that data to another system, which will display it on the UI. Based on user input, we can trigger an event and simultaneously assign both tasks to two different microservices.

- User interfaces

  Event-driven systems are commonly used in graphical user interfaces (GUIs) where user actions, such as clicking a button or typing text, trigger events that are handled by the system. This approach allows for interactive and responsive user experiences.

- Real-time data processing

  Event-driven systems are well-suited for real-time data processing that needs to react to external events in a timely manner. Data may include stock trading data, sensor network data,etc.

- Message Brokering

  Event-driven systems can be used to implement message brokers or event buses that facilitate communication between different components or services in a distributed system. Events are published and subscribed to by interested parties, enabling loose coupling and scalability.

- Asynchronous Processing

  Event-driven systems are often used to handle asynchronous tasks or background processing. For instance, when a user uploads a file to a server, an event can be triggered to initiate processing or perform additional operations without blocking the user interface.

- IoT Applications

  Internet of Things (IoT) applications frequently rely on event-driven systems to handle data generated by sensors and devices. Events can be used to trigger actions, such as sending notifications or analyzing sensor data.

## Conclusion

In conclusion, synchronous systems operate by waiting for responses before proceeding, while event-driven systems use events to trigger communication between services. Synchronous systems offer simplicity and real-time data but can result in increased coupling and slower performance. Event-driven systems provide loose coupling and performance benefits but can be complex and introduce eventual consistency. The choice between the two can depend on scale and speed of the architecture.

## References

1. [IPC in microservices architecture](https://www.diva-portal.org/smash/get/diva2:1451042/FULLTEXT01.pdf)
2. [Patterns for microservices — Sync vs Async](https://medium.com/inspiredbrilliance/patterns-for-microservices-sync-vs-async-5de3be11eb96)
3. [Microservices patterns: synchronous vs asynchronous communication](https://greeeg.com/en/issues/microservices-patterns-synchronous-vs-asynchronous)
4. [Exploring Microservices Communication Patterns](https://levelup.gitconnected.com/synchronous-vs-asynchronous-by-example-36b7b87711e7)[Microservice communication part 1-every programmer must know](https://medium.com/javarevisited/microservices-communication-part-1-every-programmer-must-know-7c6607d2d563)
5. [Do you know about GraphQL](https://medium.com/javarevisited/do-you-know-about-graphql-the-query-language-for-api-s-4038660865be)
6. [An architect's guide to APIs: SOAP, REST, GraphQL, and gRPC](https://www.redhat.com/architect/apis-soap-rest-graphql-grpc)
7. [Benefits of event-driven systems](https://www.neebal.com/blog/advantages-and-disadvantages-of-event-driven-architecture)
8. [Pros and Cons of Event-Driven Architecture](https://foreignpolicyi.org/event-driven-architecture/)
9. [What Is Event-Driven Architecture, and When Should I Use It?](https://levelup.gitconnected.com/what-is-event-driven-architecture-and-when-should-i-use-it-1ea9987b85d)
10. [Example of event-driven architecture](https://simplicable.com/IT/event-driven-architecture)
11. [What is an Event-Driven Architecture?](https://aws.amazon.com/event-driven-architecture/#:~:text=You%20can%20use%20an%20event,services%20independently%20from%20other%20teams.)
12. [Microservice Communication Styles](https://www.oreilly.com/library/view/building-microservices-2nd/9781492034018/ch04.html)
13. [Synchronous vs. asynchronous microservices communication patterns](https://www.theserverside.com/answer/Synchronous-vs-asynchronous-microservices-communication-patterns)
14. [Synchronous vs. asynchronous communications: The differences](https://www.techtarget.com/searchapparchitecture/tip/Synchronous-vs-asynchronous-communication-The-differences)
