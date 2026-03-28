# Knowledge Base — SA-ANA-001 Code Design Analysis

## Overview

Defines the knowledge base a qualified Code Design Analysis AI Agent must possess.

## KB-01: Software Design Patterns (GoF)

### Creational Patterns
| Pattern | Intent | Use When |
|---------|--------|----------|
| Factory Method | Define interface for creating objects, let subclasses decide | Subclass controls which concrete object is created |
| Abstract Factory | Create families of related objects without specifying concrete classes | System independent of how its objects are created |
| Builder | Construct complex objects step by step | Complex construction with many optional parameters |
| Prototype | Clone existing objects | Instances differ only in state, not structure |
| Singleton | Ensure only one instance exists | Exactly one object needed to coordinate system |

### Structural Patterns
| Pattern | Intent | Common Anti-Pattern Risk |
|---------|--------|--------------------------|
| Adapter | Convert one interface to another | Adapter proliferation masking design issues |
| Bridge | Separate abstraction from implementation | Over-engineering simple hierarchies |
| Composite | Compose objects into tree structures | Overly generalized leaf/node handling |
| Decorator | Attach responsibilities dynamically | Deep chains making debugging difficult |
| Facade | Provide simplified interface to subsystem | Facade becoming a God Class |
| Flyweight | Share fine-grained objects | Premature optimization |
| Proxy | Surrogate for another object | Hidden behavior, debugging difficulty |

### Behavioral Patterns
| Pattern | Intent | Key Indicators |
|---------|--------|----------------|
| Chain of Responsibility | Pass request along handler chain | Multiple conditional handlers |
| Command | Encapsulate request as object | Undo/redo, queueing, logging |
| Iterator | Sequential access to collection elements | Traversal mixed with collection logic |
| Mediator | Object encapsulates how others interact | Many-to-many coupling |
| Observer | Notify dependents when state changes | Event-driven, loosely coupled updates |
| State | Alter behavior when internal state changes | Many conditionals on object state |
| Strategy | Interchangeable family of algorithms | Algorithm varies by context |
| Template Method | Skeleton algorithm with deferred steps | Invariant flow, variable details |

---

## KB-02: SOLID Principles

| Principle | Definition | Common Violation |
|-----------|------------|-----------------|
| **S** — Single Responsibility | One class, one reason to change | God Class |
| **O** — Open/Closed | Open for extension, closed for modification | Modifying existing class for every new behavior |
| **L** — Liskov Substitution | Subtypes substitutable for their base type | Subclass violates base class contract |
| **I** — Interface Segregation | Clients depend only on methods they use | Fat interfaces with unrelated methods |
| **D** — Dependency Inversion | Depend on abstractions, not concretions | Direct instantiation of concrete classes |

---

## KB-03: Architectural Patterns

| Pattern | Intent | Use Case |
|---------|--------|----------|
| Repository | Abstraction between domain and data access | Decouple domain from persistence |
| CQRS | Separate read and write models | Different read/write scalability requirements |
| Event Sourcing | Store state as sequence of events | Full audit trail required |
| Saga | Manage distributed transactions | Multi-service transactions without 2PC |
| Anti-Corruption Layer | Isolate domain from external model | Legacy system integration |
| Facade | Simplified interface to complex subsystem | Reduce external coupling |
| Filter Chain | Process data through sequential filters | Middleware, request/response pipelines |

---

## KB-04: Architectural Styles

| Style | Key Characteristics | Strengths | Weaknesses |
|-------|---------------------|-----------|------------|
| Layered (N-Tier) | Presentation → Business → Data | Simple, widely understood | Distributed monolith risk, layer coupling |
| Hexagonal (Ports & Adapters) | Core domain + ports + adapters | Highly testable, infrastructure independent | More upfront design effort |
| Clean Architecture | Dependency rule: entities → use cases → adapters → frameworks | Enforced dependency direction | Overhead for simple systems |
| DDD | Bounded contexts, aggregates, domain events | Complex domain expressibility | Steep learning curve |
| Microservices | Small, independent deployable services | Independent scaling and deployment | Distributed system complexity |
| Event-Driven | Producers, consumers, event bus | Loose coupling, async scalability | Eventual consistency, observability challenges |

---

## KB-05: Design Smell Catalogue

| Smell | Description | Refactoring Direction |
|-------|-------------|----------------------|
| God Class | Too many responsibilities in one class | Extract Class, Move Method |
| Feature Envy | Method uses more of another class's data | Move Method |
| Data Clumps | Same group of data appears together repeatedly | Extract Class, Introduce Parameter Object |
| Shotgun Surgery | One change requires many small changes everywhere | Move Method, Inline Class |
| Divergent Change | Class changes for many different reasons | Extract Class |
| Primitive Obsession | Primitives used instead of small objects | Replace Data Value with Object |
| Long Method | Method too long, does too much | Extract Method, Decompose Conditional |
| Long Parameter List | Too many parameters | Introduce Parameter Object |
| Inappropriate Intimacy | Classes know too much about each other | Move Method, Extract Class |

---

## KB-06: Refactoring Catalogue

| Refactoring | Description | Applicable When |
|-------------|-------------|-----------------|
| Extract Class | Move cohesive fields/methods to a new class | Class has multiple responsibility sets |
| Move Method | Move method to the class it uses most | Feature Envy detected |
| Decompose Conditional | Extract condition and branches into named methods | Complex conditional logic |
| Replace Type Code with Strategy | Use Strategy pattern instead of type codes | Behavior varies by type |
| Extract Method | Name a code fragment as a method | Fragment can be named and reused |
| Introduce Parameter Object | Replace parameter group with an object | Data clumps in parameters |
| Replace Inheritance with Delegation | Delegate instead of extending | Subclass uses only part of superclass |

---

## KB-07: NFR Categories

| Category | Examples | Key Metrics |
|----------|----------|-------------|
| Performance | Response time, throughput, latency | p50/p95/p99, requests/sec |
| Security | Auth, authorization, encryption, input validation | OWASP Top 10 compliance |
| Maintainability | Readability, modularity, test coverage | Cyclomatic complexity, coverage % |
| Scalability | Horizontal/vertical scaling, peak load | Throughput under load |
| Testability | Unit isolation, integration test coverage | Mockability, coverage achievable |
| Observability | Logging, metrics, tracing, alerting | MTTD, alert coverage |
| Reliability | Availability, fault tolerance, error handling | Uptime SLA, MTBF, MTTR |
| Compliance | Regulatory, data residency, audit | Compliance checklist |

---

## KB-08: API Design Principles

| Style | Key Principles |
|-------|----------------|
| REST | Resource-based URLs, HTTP verbs, stateless, HATEOAS |
| GraphQL | Schema-first, single endpoint, flexible queries, N+1 awareness |
| gRPC | Protocol Buffers, streaming, strong typing |
| Event Contracts | Schema versioning, backward compatibility, consumer-driven contracts |

---

## KB-09: Coupling & Cohesion Metrics

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| Afferent Coupling (Ca) | # classes that depend on this class | Higher = more responsibility |
| Efferent Coupling (Ce) | # classes this class depends on | Higher = more fragile |
| Instability Index (I) | Ce / (Ca + Ce) | 0 = stable, 1 = unstable |
| Abstractness (A) | # abstract classes / total classes | 0 = concrete, 1 = abstract |
| Distance from Main Sequence | \|A + I - 1\| | Far from line = problematic zone |

## Modifying the Knowledge Base

To add knowledge, append a new `KB-N` section following the format above.
