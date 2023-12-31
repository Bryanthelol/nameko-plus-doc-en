---
#search:
#  boost: 2 
#search:
#  exclude: true
hide:
  - footer
---

# Overview

## Nameko

In a distributed environment, Nameko provides a microservice architecture that simplifies communication between microservices, making calling a service as easy as calling a local method.

Nameko offers RPC synchronous invocation (also supporting asynchronous invocation), event publication/subscription, and exposes APIs via the HTTP protocol (although it is generally not recommended to use this, but to use other web frameworks).

All these capabilities are achieved on top of RabbitMQ, which is based on the AMQP protocol.

When you start a Nameko microservice process, service discovery is already done through RabbitMQ, so for developers, the focus can be on implementing business logic.

If business volume increases and the number of requests to the microservice rises to a certain level, you can simply increase the number of Nameko microservice instances to cope easily. The underlying RabbitMQ will automatically load balance the Nameko instances.

The content of this document will further explain:

**How to develop distributed microservice applications based on Nameko.**
