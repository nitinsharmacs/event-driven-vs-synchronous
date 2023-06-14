# Inter Process Communication in Microservices

<!-- Title not decided yet -->

## Abstract

<!-- Filler Abstract -->

## Goal

The goal of this paper is to provide information about
Synchronous and Event-Driven systems in conceptual and architectural perspective.

## Introduction

### Synchronous Systems

A Synchronous system is a system,
where communication, data processing, data transfer, or process execution happen at a blocking/waiting manner.

A analogy could be a phone call from a requester to a responder,
where the communication or instructions happens only when the responder responds.

For this system to be practical, a request-response model is required where a client requests a server/responder and the responder takes care of responding to this request by a response from its black-boxed processes.

Synchronous involves request/response style of communication where client sends request to the server and waits for it reply. Client can only move forward once it gets back the reply from server.

#### Implementations

There are several implementations of this Synchronous system:

1. HTTP (Hyper Text Transfer Protocol)
2. RPC, gRPC (Remote Procedure Call)
3. REST (RESTful API services)
4. GraphQL (API query language)

##### REST APIs, HTTP

These are the interfaces provided by services or applications where other services can send requests to. It is the conventional and easy method for inter-service communication.

Each of the service has its own web server up and running on some port. These services provide endpoints where other services can send requests.

##### Remote Procedure Call (RPC)

In microservice architecture, there are various methods of communication. Remote procedure call is one of them. In monolithic architecture where everything is coupled together to make a single unit, processes communicate by calling procedures from another unit in the same system. There is no separation as everything is running at the same place.

In distributed environment, achieving the same functionality of calling a procedure of different service is done by using Remote Procedure call.

###### gRPC (Google's version of RPC)

gRPC is an google implementation for RPC. It is based on binary encoding format [protocol buffer](https://developers.google.com/protocol-buffers) and implemented on top of [HTTP/2](https://developers.google.com/web/fundamentals/performance/http2).

It is strongly typed, polyglot (supports several languages), and provides both server and client side streaming.

![gRPC](https://grpc.io/img/landing-2.svg)

### Event Driven Systems

Introduction about Event Driven

## Limitations of Systems

### Synchronous Systems

Although Synchronous system is simple and straight forward to implement, it has some limitations :

1. Wait time overhead added with addition to response processing time.
2. Bottleneck for processing large number of requests

3. Autonomous micro services.

When there is a complex network of HTTP request/response among micro services, it makes those services less autonomous.

<!-- This sentence can be elaborated -->

4. System Resilience

It is the ability of a service to provide responses to the client requests even in the face of adversity.
When micro services have dense network of HTTP request/response and if any service fails, the dependent services may not provide favorable outcomes.

5. Slow system

One microservice has to wait for downstream service for the response. This makes the overall request/response process slow. It becomes worse if there is a chain of those requests.

### Event Driven Systems

Some Limitations of Async systems

## Likelihoods of Use (When to use what ?)

## Conclusion

## References

1. [IPC in microservices architecture](https://www.diva-portal.org/smash/get/diva2:1451042/FULLTEXT01.pdf)
1. [Patterns for microservices — Sync vs Async](https://medium.com/inspiredbrilliance/patterns-for-microservices-sync-vs-async-5de3be11eb96)
1. [Microservices patterns: synchronous vs asynchronous communication](https://greeeg.com/en/issues/microservices-patterns-synchronous-vs-asynchronous)
1. [Exploring Microservices Communication Patterns](https://levelup.gitconnected.com/synchronous-vs-asynchronous-by-example-36b7b87711e7)
