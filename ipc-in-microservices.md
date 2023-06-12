tags: #systems #architecture #research 

# Interprocess communication in Microservices

## Abstract

## Goal

The goal of this paper is to provide insights about different communication mechanisms in micro-service architecture.

## Introduction


## Synchronous communication Style

### Definition

Synchronous involves request/response style of communication where client sends request to the server and waits for it reply. Client can only move forward once it gets back the reply from server.

## Asynchronous communication Style

### Definition

Asynchronous communication is based on the concept of events and messages. The caller service emits an event and processes subsequent requests without waiting for the response. An **event** is change in state.


## References
1. [IPC in microservices architecture](https://www.diva-portal.org/smash/get/diva2:1451042/FULLTEXT01.pdf)
2. 