tags: #systems #architecture #research 

# Interprocess communication in Microservices

## Abstract

## Goal

The goal of this paper is to provide insights about different communication mechanisms in microservice architecture.

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

### Limitations

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