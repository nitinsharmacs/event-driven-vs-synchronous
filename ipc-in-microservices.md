tags: #systems #architecture #research

# Event Driven and Synchronous Systems

## Abstract

## Goal

The goal of this paper is to provide information about
Synchronous and Event-Driven systems in conceptual and architectural perspective.

## Introduction

This paper would explain about synchronous and event driven systems by taking into account how service interaction takes place in microservices architecture.

## Synchronous Systems

A synchronous system refers to a system in which various operations, such as communication, data processing, data transfer, or process execution, happen in a blocking or waiting manner. In other words, the system operates in a synchronised and coordinated fashion, where each operation blocks or pauses the execution until it finishes.

An analogy could be a phone call where each party has to wait for other to finish responding. 

In microservice architecture where services are communicating through REST API using HTTP calls, client service has to wait for the response from the server and execution moves forwards once the response comes back.

<!-- Diagram --->

Let's see some of the synchronous communication implementations in microservices.

### Implementations

1. REST APIs
2. RPC
3. GraphQL

#### REST APIs

These are the interfaces provided by services or applications where other services can send requests to. It is the conventional and easy method for inter-service communication.

Each of the service has its own web server up and running on some port. These services provide endpoints where other services can send requests.

![REST API](./images/restapi.png)

Considering the example of an E-commerce website, client sends the request to get all products data from the server. Client has to wait for the response from the server and then only client can show all the products. It makes this method of communication synchronous as there is a blocking of execution. 

#### Remote Procedure Call

In microservice architecture, there are various methods of communication. Remote procedure call is one of them. In monolithic architecture where everything is coupled together to make a single unit, processes communicate by calling procedures from another unit in the same system. There is no separation as everything is running at the same place.

In distributed environment, achieving the same functionality of calling a procedure of different service is done by using Remote Procedure call.

##### Why RPC?

Why do we need RPC? Why can't we use REST API method of communication? 

1. Bulkiness
    REST API commonly implemented using JSON payload over HTTP. JSON schema is bulky and occupy more space than binary format. This makes the request/response bulky. 

2. No schema
    Schema is optional for REST API using JSON. Defining the contracts for the APIs becomes a challenge.


##### gRPC

gRPC is an google implementation for RPC. It is based on binary encoding format [protocol buffer](https://developers.google.com/protocol-buffers) and implemented on top of [HTTP/2](https://developers.google.com/web/fundamentals/performance/http2).

It is strongly typed, polyglot (supports several languages), and provides both server and client side streaming.

![gRPC](./images/grpc.svg)

###### Where to use gRPC?

We can't make everything communication through gRPC. Mostly, gRPC is used for inter-service communication. For public services, REST APIs scheme can be used. 

Moreover, implementing gRPC on a browser based application is not straightforward.

###### gRPC features

1. Strong types and well defined interface
    All the interfaces contracts are well defined. Unlike json schema where there is no schema, gRPC request and response defines rigid schema. It helps in avoiding runtime errors.
    
2. Polyglot
    It can be used with different programming languages.

3. Stream support
    It supports stream feature in both client and server. 

4. Other features includes
    1. Resiliency
    2. Authentication
    3. Encryption
    4. Compression


### Limitations of Synchronous communication

1. Autonomous micro services.

When there is a complex network of HTTP request/response among micro services, it makes those services less autonomous.

2. System Resilience

It is the ability of a service to provide responses to the client requests even in the face of adversity.
When micro services have dense network of HTTP request/response and if any service fails, the dependent services may not provide favourable outcomes.

3. Slow system

One microservice has to wait for downstream service for the response. This makes the overall request/response process slow. It becomes worse if there is a chain of those requests.

## Event Driven System

  Event driven systems, are systems that uses events to trigger and communicate between decoupled services where an **event** is change in state. For instance, suppose there is a system that has two microservices, A and B, with A allowing users to configure a car and B storing that data in a database. If the user modifies configuration details in service A, it will trigger an event and tell service B about the change in the configuration of the car. Then service B fetches new data from service B and updates the database.

  Event-driven system typically consists of 
  * Event emitters (agents)
  * Event consumers (sinks)
  * Event channels.

  In the above example, service A is an event emitter, and service B is an event consumer. **Event channel** refer to the pathway through which events flow it may be a queue or an event grid.

  Event-driven systems communicate asynchronously and use the following protocols for communication :
  * Message Queue Telemetry Transport (AMQP)
  * Advanced Message Queuing Protocol (MQTT)  
  * Websocket
  * Simple Text Oriented Messaging Protocol (STOMP)

## References

1. [IPC in microservices architecture](https://www.diva-portal.org/smash/get/diva2:1451042/FULLTEXT01.pdf)
2. 
