---
layout: default
title: Microservices Design Patterns
parent: Micro Services
resource: true
desc: "Microservices Design Patterns interview questions and answers."
categories: [Microservices Design Patterns]
---

# Microservices Design Patterns
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---


##  Microservices Design Patterns

microservice architecture has to be built on below principles.

1. Scalability
2. Availability
3. Resiliency
4. Independent, autonomous
5. Decentralized governance
6. Failure isolation
7. Auto-Provisioning
8. Continuous delivery through DevOps

---

##  Integration Patterns


###  API Gateway Pattern

####  Problem
When an application is broken down to smaller microservices, there are a few concerns that need to be addressed:

How to call multiple microservices abstracting producer information.

On different channels (like desktop, mobile, and tablets), apps need different data to respond for the same backend service, as the UI might be different.

Different consumers might need a different format of the responses from reusable microservices. Who will do the data transformation or field manipulation?

How to handle different type of Protocols some of which might not be supported by producer microservice.

#### Solution

An API Gateway helps to address many concerns raised by microservice implementation, not limited to the ones above.

An API Gateway is the single point of entry for any microservice call.

It can work as a proxy service to route a request to the concerned microservice, abstracting the producer details.

It can fan out a request to multiple services and aggregate the results to send back to the consumer.

One-size-fits-all APIs cannot solve all the consumer's requirements; this solution can create a fine-grained API for each specific type of client.

It can also convert the protocol request (e.g. AMQP) to another protocol (e.g. HTTP) and vice versa so that the producer and consumer can handle it.

It can also offload the authentication/authorization responsibility of the microservice.

---

###  Aggregator Pattern

####  Problem

####  Solution

---

###  Client-Side UI Composition Pattern

####  Problem

####  Solution

---


##  Database Patterns

###  Database per Service

####   Problem

####   Solution

---

###  Shared Database per Service

####   Problem

####   Solution

---

###   Command Query Responsibility Segregation (CQRS)

####   Problem

####   Solution

---

###   Saga Pattern

####   Problem

####   Solution

---

##  Observability Patterns


###   Log Aggregation

####   Problem

####   Solution

---



###   Performance Metrics

####   Problem

####   Solution

---

###   Distributed Tracing

####   Problem

####   Solution

---

###   Health Check

####   Problem

####   Solution

---

##  Cross-Cutting Concern Patterns

###   External Configuration

####   Problem

####   Solution

---


###   Service Discovery Pattern

####   Problem

####   Solution

---



###   Circuit Breaker Pattern

####   Problem

####   Solution

---


###   Blue-Green Deployment Pattern

####   Problem

####   Solution

---

