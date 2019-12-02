# Software Architecture

## Serverless

  - **Benefits**
    - Scalability
    - Cost & utilization
    - Managed infrastructure
    - SaaS integrations
    - Developer productivity
  - **Drawbacks**
    - Cold starts
    - Debugging
    - Obscure infrastructure
    - Opinionated development process

## Microservices

### Domain-Driven Design

  - **Bounded Context**
    - A design technique for **scoping** microservices.
    - Each **bounded context** represents a **domain function** or **microservice**.

### Design Principles

  - **Business Domain Centric**
    - Bounded Context
  - **High Cohesion**
    - Single Focus/Responsibility
  - **Autonomous**
    - Loose Coupling
      - Contract-based
      - Technology agnostic API
      - Avoid client libraries
      - Avoid sharing between services
    - Stateless
    - Independently Changeable
    - Independently Deployable
  - **Resilience**
    - Multi-Instance
    - Design For Failure
      - Fail Fast
      - Timeout
      - Retry
      - Circuit Breaking
    - Degrade Functionality
    - Default Functionality
  - **Observable**
    - Centralized Logging
    - Centralized Metrics
    - Distributed Tracing
  - **Automated**
    - Continuous Integration
    - Continuous Delivery
    - Automated Testing
    - Automated Monitring/Alerting


### API Design

**API Paradigms**

  - Synchronous:
    - RPC: gRPC
    - HTTP: REST
  - Asynchronous:
    - Async API call using callbacks
    - Event-based using message brokers
      - Competing workers pattern
      - Fan-out pattern

**API Composition Patterns**

  - Chained Pattern
  - Proxy Pattern (API Gateway)
  - Aggregate Pattern
    - Front-end Aggregator
    - Back-end Aggregator


## Caching

**Caching Patterns**

  - Client-side Caching
  - Cache-in-the-Middle
  - Server-side Caching
    - Embedded Cache
    - Sidecar Cache
    - Caching Service
      - Look-Aside
      - Read-Through
      - Write-Through
      - Write-Back
      - Write-Around
  - Hierarchical Caching

**Challenges**

  - Cache Update
  - Cache Invalidation


## Stream Processing

  - Stream processing is a computing paradigm for processing and querying continuous streams of data and events.


## Practices

### Handling Overload

  - Set **per-customer limits**
  - Implement **client-side throttling**
  - Define a **criticality** notion for requests
  - Pay attention to **utilization signals**
  - First serve **degraded responses** and then errors
  - Decide when to **retry**

### Addressing Cascading Failures

  - Back off exponentially when retrying
  - Use deadlines, deadline propagation, and cancellation propagation when retrying to not further overload the system
  - Upstream services should reject requests rather than overloading the downstream services
  - Drop some proportion of incoming requests as the backend approaches overload conditions (**load shedding**)
  - Reduce the amount of work that needs to be performed under overload situation (**graceful degradation**)

