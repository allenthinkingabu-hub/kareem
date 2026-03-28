# Agent Skills — SA-ANA-001 Code Design Analysis

## Overview

Defines the skills a qualified Code Design Analysis AI Agent must possess.

## Core Skills

### SK-01: Code Reading & Deep Structural Comprehension
- Navigate file hierarchies to understand class/interface/module boundaries
- Trace execution flows across multiple files and abstraction levels
- Identify layering patterns and architectural boundaries from code alone

### SK-02: Design Pattern Identification (GoF)
- **Creational**: Factory Method, Abstract Factory, Builder, Prototype, Singleton
- **Structural**: Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy
- **Behavioral**: Chain of Responsibility, Command, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor

### SK-03: Architectural Style Recognition
- Layered (N-Tier) Architecture
- Hexagonal (Ports and Adapters) Architecture
- Domain-Driven Design (DDD)
- Clean Architecture (Onion / Dependency Rule)
- Microservices Architecture
- Event-Driven Architecture

### SK-04: Responsibility Analysis & SRP Compliance
- Decompose class/method responsibilities into distinct concerns
- Identify Single Responsibility Principle (SRP) violations
- Map responsibility taxonomy: coordination, validation, persistence, transformation, notification, orchestration, etc.

### SK-05: Dependency Mapping
- Trace inbound callers (who depends on this component)
- Trace outbound dependencies (what this component depends on)
- Identify external system touchpoints (databases, message queues, external APIs)

### SK-06: Coupling & Cohesion Analysis
- Afferent coupling (Ca): number of classes that depend on this class
- Efferent coupling (Ce): number of classes this class depends on
- Instability index: Ce / (Ca + Ce)
- Cohesion assessment: are all methods/fields related to a single purpose?

### SK-07: FR/NFR Extraction from User Intent
- Parse free-form intent statements to extract explicit and implicit requirements
- Classify requirements as Functional (FR) or Non-Functional (NFR)
- Assign priority levels (High/Medium/Low) and NFR categories (Performance, Security, Maintainability, etc.)

### SK-08: Gap Analysis Between Requirements and Current Design
- Map each confirmed FR/NFR against current code evidence
- Rate gap severity: 🔴 High / 🟡 Medium / 🟢 Low
- Identify risks triggered by each gap

### SK-09: Improvement Direction Formulation
- Propose design pattern-based improvement directions for critical and moderate gaps
- Articulate trade-offs: what is gained vs. what is given up
- Define prerequisites for applying each direction

### SK-10: Anti-Pattern Detection
- **God Class**: class with too many responsibilities
- **Feature Envy**: method that uses more of another class's data than its own
- **Shotgun Surgery**: single change requires modifications in many classes
- **Divergent Change**: class that changes for many different reasons
- **Data Clumps**: groups of data that always appear together
- **Primitive Obsession**: overuse of primitive types instead of objects
- **Long Method**: method that does too much
- **Inappropriate Intimacy**: two classes know too much about each other's internals

## Modifying Skills

To add a new skill, append a new `SK-N` section. To modify an existing skill, edit the relevant section.
