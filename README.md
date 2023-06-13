# Event driven system and Synchronous system

## Abstract

## Goal

The goal of this paper is to provide information about
Synchronous and Event-Driven systems in conceptual and architectural perspective.

## Introduction

### Synchronous Systems

A Synchronous system is a system,
where communication, data processing, data transfer, or process execution happen at a blocking/waiting manner.
A analogy could be a phone call from a requester to a responder,
where the communication or instructions happens only when the responder responds by keeping the requester waiting.

For this system to be practical, a request-response model is required.
where a client requests a server/responder and the responder takes care of responding to this request by a response from its black-boxed processes.

#### Applications

Some of the applications of this Synchronous system being :

1. HTTP
2. RPC
3. REST
4. GraphQL and others

#### Limitations

Although Synchronous system is simple and straight forward to implement, it has some limitations :

1. Wait time overhead added with addition to response processing time.
2. Bottleneck for processing large number of requests

### Event Driven Systems

        1. Examples of each concept
            1. Intro
            2. How it works
            3. Applications
            4. Limitations

## Likelihoods of Use

## Differences

## Conclusion

## References

1. [Patterns for microservices — Sync vs Async](https://medium.com/inspiredbrilliance/patterns-for-microservices-sync-vs-async-5de3be11eb96)
2. [Microservices patterns: synchronous vs asynchronous communication](https://greeeg.com/en/issues/microservices-patterns-synchronous-vs-asynchronous)
3. [Exploring Microservices Communication Patterns](https://levelup.gitconnected.com/synchronous-vs-asynchronous-by-example-36b7b87711e7)
