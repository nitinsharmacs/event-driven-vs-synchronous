tags: #systems #architecture #research

# Event-Driven and Synchronous Systems

## Abstract

## Goal

The goal of this paper is to provide information about
Synchronous and Event-Driven systems in conceptual and architectural perspective.

## Introduction

This paper would explain about synchronous and event-driven systems by taking into account how service interaction takes place in microservices architecture.

<!-- Introductions and Goals has to be refactored -->

## Synchronous Systems

A synchronous system refers to a system in which various operations, such as communication, data processing, data transfer, or process execution, happen in a blocking or waiting manner. In other words, the system operates in a synchronized and coordinated fashion, where each operation blocks or pauses the execution until it finishes.

An analogy could be a phone call where each party has to wait for other to finish responding.

<!-- Image for Synchronous systems -->

One of the application of synchronous systems are in microservice architecture, where services communicate through REST API or some other methods using HTTP calls, client service has to wait for the response from the server and execution moves forwards once the response comes back.

Let's see some of the synchronous systems implementations.

### Implementations

1. REST APIs
2. RPC
3. GraphQL

<!-- Include Synchronous systems examples other than communication -->

#### REST APIs

REST APIs are the interfaces provided by services or applications where other services can send requests to. It is the conventional and easy method for inter-service communication.

Each of the service has its own web server which provides endpoints where other services can send requests.

<!-- Image for illustrating Rest API -->

Considering the example of an E-commerce website, client (browser) sends the request to get all products data from the server. Client has to wait for the response from the server and then only client can show all the products. It makes this method of communication synchronous as there is a blocking of execution.

#### Remote Procedure Call

REST APIs are the way to access services provided by the server by using request/response mechanism. This method can be used for inter-service communication. However, using REST APIs as solely method of communication has its own limitations. Some of them are described below.

1. No defined request/response schema.
2. Communication payload can be bulky.

Following diagram shows how services interact using RPC mechanism.

<!-- Image for illustrating gRPC -->

Figure shows that client and server are interacting using gRPC (Google RPC implementation). When the client sends request to server, client has to wait for the response. Until then client has to block its execution for that request.

Let's see one more way where services interact synchronously.

#### GraphQL

This is a data query and manipulation language. It gets the request from the clients as a form of a query, it parses and resolves the query and send back the response.

<!-- Image for illustrating gRPC -->

Unlike REST APIs, the query has defined schema about what all attributes to send in response. It makes the payload less bulky and only contains the required information.

**GraphQL is a specification** and it can be implemented in different languages such as Javascript, Java, C, C++, Python, etc.

Mostly communication is done synchronously using request/response model. However, it provides a mechanism of **Subscription** where clients can get real time updates asynchronously.

So, these were some of the implementations of synchronous communication. Some of them are evolving to provide asynchronous functionality which makes the interaction much effective and performative.

Now, let's examine some of the drawbacks of synchronous communication.

### Drawbacks of Synchronous Systems

1. **Autonomous micro services.**

   When there is a complex network of HTTP request/response among micro services, it makes those services less autonomous.

2. **System Resilience**

   It is the ability of a service to provide responses to the client requests even in the face of adversity.
   When micro services have dense network of HTTP request/response and if any service fails, the dependent services may not provide favourable outcomes.

3. **Slow system**

   One microservice has to wait for downstream service for the response. This makes the overall request/response process slow. It becomes worse if there is a chain of those requests.

## Event-Driven Systems

Event-driven systems, are systems that uses events to trigger and communicate between decoupled services where an **event** is change in state. For instance, suppose there is a system that has two microservices, A and B, with A allowing users to configure a car and B storing that data in a database. If the user modifies configuration details in service A, it will trigger an event and tell service B about the change in the configuration of the car. Then service B fetches new data from service A and updates the database through event broker.

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

2. Message queues and brokers : 

    Message queues and brokers provide a mechanism for decoupling components in an event-driven system. Components can publish events to a message queue, and other components can subscribe to the queue to receive and process those events asynchronously. Popular message brokers include Apache Kafka, RabbitMQ, and Amazon Simple Queue Service (SQS).

3. Reactive programming : 

    Reactive programming is a programming paradigm that deals with asynchronous data streams and event propagation. It emphasizes the use of reactive streams and operators to handle and transform events in a declarative manner. Reactive frameworks like RxJava, Reactor, and Akka provide powerful tools for building event-driven systems.

4. Event sourcing and CQRS : 
    
    Event sourcing is a technique where changes to an application's state are captured as a sequence of events. Instead of persisting the current state, you persist the events that lead to that state. Combined with Command Query Responsibility Segregation (CQRS), you can separate the write (command) and read (query) models of an application. This approach allows you to maintain a full history of events and easily implement features like event replay and auditing.

5. Webhooks : 
  
    Webhooks are a simple and popular way to implement event-driven systems in web applications. With webhooks, you define specific URLs in your application that other services can call when specific events occur. The receiving application can then process the event payload and take appropriate actions. Webhooks are commonly used for integrating third-party services and triggering actions based on external events.

These are just a few examples of how you can implement event-driven systems. The choice of approach depends on the complexity of your system, the technologies you're using, and the specific requirements you have for event handling and propagation.


### Benefits of Event-Driven Systems

* **Loose coupling**

  In above example we have seen that service A is not aware of existence of service B, so making changes to any service will not affect communication between them and services can evolve independently.

* **Resilience**

  Let say service B is down for some reason, the producer service that is service A can till send message to the queue without interruption. The service B can pick up that message and processes that once it is up and running.

* **Performance**

  The sender service doesn't need to wait for the response of the receiving service, so it saves time and the sender service can proceed with its other tasks, which improves the system's overall performance.

* **System extensibility**

  New microservices can be added to the architecture without requiring changes to existing microservices that is service A and B.

* **Cut costs**

  Event-driven systems are push-based, so everything happens on-demand as the event presents itself in the router. This way, you’re not paying for continuous polling to check for an event. This means less network bandwidth consumption, less CPU utilization, less idle fleet capacity, and less SSL/TLS handshakes.


### Drawbacks of Event-Driven Systems

* **Complexity**

  Event-driven systems can introduce additional complexity compared to more traditional synchronous systems. The asynchronous nature of event-driven communication requires careful design and handling of events, event ordering, event schemas, and event-driven workflows. This complexity can make the system more challenging to develop, test, and maintain.

* **Inconsistency**

  Event-driven systems often rely on eventual consistency, meaning that the system's state might not be immediately consistent across all microservices. It can take time for events to propagate and for all subscribers to process and react to events. This can lead to temporary inconsistencies or race conditions in the system, which need to be carefully managed.

* **Over-engineering of processes**

  Sometimes a simple call from one service to another is enough. In event-driven systems, it usually requires much more infrastructure to support it, which will add costs like need of queueing system.

* **Testing** 

  Testing and debugging event-driven systems can be more complex than traditional systems. Ensuring proper event ordering, verifying the correctness of event-driven workflows, and simulating different event scenarios for testing can be challenging.

* **Debugging**

  To debug event-driven systems need advance tooling and techniques.

## References

1. [IPC in microservices architecture](https://www.diva-portal.org/smash/get/diva2:1451042/FULLTEXT01.pdf)
2. [Patterns for microservices — Sync vs Async](https://medium.com/inspiredbrilliance/patterns-for-microservices-sync-vs-async-5de3be11eb96)
3. [Microservices patterns: synchronous vs asynchronous communication](https://greeeg.com/en/issues/microservices-patterns-synchronous-vs-asynchronous)
4. [Exploring Microservices Communication Patterns](https://levelup.gitconnected.com/synchronous-vs-asynchronous-by-example-36b7b87711e7)[Microservice communication part 1-every programmer must know](https://medium.com/javarevisited/microservices-communication-part-1-every-programmer-must-know-7c6607d2d563)
5. [Do you know about GraphQL](https://medium.com/javarevisited/do-you-know-about-graphql-the-query-language-for-api-s-4038660865be)
6. [An architect's guide to APIs: SOAP, REST, GraphQL, and gRPC](https://www.redhat.com/architect/apis-soap-rest-graphql-grpc)
7.
