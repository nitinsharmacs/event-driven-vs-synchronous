tags: #systems #architecture #research

# Inter Process Communication in Microservices

<!-- isn't this heading look like a bigger scope than our research ??? this large base will be overkill -->

## Abstract

## Goal

The goal of this paper is to provide insights about different communication mechanisms in microservice architecture.

<!-- concept + implementation ? Need a better way to say (not specific to communication mec) -->

## Introduction

## Synchronous communication Style

### Definition

Synchronous involves request/response style of communication where client sends request to the server and waits for it reply. Client can only move forward once it gets back the reply from server.

### Implementations

There are several methods to implement synchronous communication. Some of them are listed below.

1. REST APIs using HTTP
2. RCP
3. GraphQL

#### REST APIs

These are the interfaces provided by services or applications where other services can send requests to. It is the conventional and easy method for inter-service communication.

Each of the service has its own web server up and running on some port. These services provide endpoints where other services can send requests.

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

![gRPC](https://grpc.io/img/landing-2.svg)



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

## Asynchronous communication Style

### Definition

Asynchronous communication is based on the concept of events and messages. The caller service emits an event and processes subsequent requests without waiting for the response. An **event** is change in state.

## References

1. [IPC in microservices architecture](https://www.diva-portal.org/smash/get/diva2:1451042/FULLTEXT01.pdf)
2. 
