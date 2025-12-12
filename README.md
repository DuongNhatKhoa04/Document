# .NET Backend Learning Hub (Revised & Enhanced Edition)

**title:** .NET Backend Learning Hub
**author:** Personal Engineering Roadmap
**status:** Active
**version:** 3.0
**last-updated:** 2025-12-12
**classification:** Internal

---

# 1. Purpose

This documentation defines the official engineering learning roadmap for the .NET Backend Track (2025 Edition). It organizes required competencies — from Intern foundations to CTO-level strategy — based on Microsoft Docs, modern backend engineering standards, and enterprise architecture practices (DDD, CQRS, Clean Architecture, Event-Driven Systems).

The goal is to provide a single, long-living knowledge hub that grows with the engineer, ensuring clarity, consistency, and scalability.

---

# 2. Scope

This roadmap applies to all backend engineers and covers:

* C# fundamentals & language internals
* .NET runtime, CLR, memory model
* ASP.NET Core Web API
* Databases, SQL, Entity Framework Core
* Software architecture patterns & DDD
* Security, authentication, authorization
* Observability, logging, metrics, tracing
* Microservices & distributed systems
* Cloud, containers & DevOps automation
* Engineering leadership, system design & CTO skills

---

# 3. Definitions

**Fundamentals** — Core programming skills required before backend development.
**Backend Development** — APIs, business logic, data access.
**Architecture** — Scalable system patterns and design principles.
**Security** — Protecting systems through secure coding and access control.
**Observability** — Logging, metrics, tracing for reliability.
**Microservices** — Independent distributed components communicating over events or REST.
**Leadership** — Senior-level competencies for system design and guiding teams.

---

# 4. Full Roadmap (Intern → CTO)

This section describes a fully expanded and detailed learning path, now simplified to focus on **knowledge only** (no exercises), and written **entirely in English**.

---

## 🚀 I. Stage 1 – INTERN .NET (Core C# & .NET Runtime)

**Goal:** Build solid foundations in C#, the .NET runtime, memory, OOP, generics, LINQ, async/await.

### 1. C# Fundamentals (Microsoft Docs)

* Program Structure: Main, compilation model, top‑level statements, namespaces, assemblies
* Type System: value vs reference types, struct/class/record, nullable context, casting (implicit/explicit)
* Object-Oriented Programming: encapsulation, inheritance, polymorphism, abstraction, interfaces
* Functional Techniques: delegates, lambdas, LINQ, higher‑order functions
* Exception Handling: using, handling, creating, and throwing exceptions
* Language Concepts: covariance, contravariance, variance in interfaces/delegates, iterators

### 2. .NET Runtime Foundations

* CLR & Memory: Stack vs Heap, GC generations, LOH, boxing/unboxing
* Common Type System (CTS): IL, metadata, assembly structure (.dll / .exe)

---

## 🟦 II. Stage 2 – JUNIOR .NET Developer (ASP.NET Core Fundamentals)

**Goal:** Be able to build standard enterprise-level backend APIs.

### 1. ASP.NET Core Fundamentals

* WebHost, Startup, Middleware pipeline
* Routing, Controllers, Model Binding
* Validation: DataAnnotations, FluentValidation
* Authentication & Authorization: JWT, Cookies, Claims, Policies

### 2. Dependency Injection

* Service lifetimes: Singleton, Scoped, Transient
* Options Pattern

### 3. Entity Framework Core

* Migrations
* LINQ execution behavior
* Relationships
* Loading strategies: eager, lazy, explicit loading

---

## 🟩 III. Stage 3 – MIDDLE .NET Engineer (Architecture & Patterns)

**Goal:** Understand enterprise-grade architecture and pattern-driven development.

### 1. Clean Architecture

* Entities, Use Cases, Infrastructure, API layers
* Domain separation
* DTOs vs Domain Models vs Interfaces

### 2. Essential Design Patterns

* Factory, Strategy, Observer, Adapter, Decorator, Mediator
* Repository Pattern: when it should or should not be used

### 3. CQRS

* Command vs Query segregation
* Mediator pattern (MediatR)
* Validation pipelines
* Cross-cutting concerns

### 4. Domain-Driven Design (DDD)

* Value Objects
* Aggregates
* Domain Events
* Bounded Contexts
* Ubiquitous Language

---

## 🟥 IV. Stage 4 – SENIOR .NET Engineer (Microservices & Event-Driven Systems)

**Goal:** Think in systems, not individual components; build scalable distributed architectures.

### 1. Microservices Architecture

* API Gateway (YARP, Ocelot)
* Service Discovery
* Resilience: Retry, Circuit Breaker (Polly)
* Distributed Tracing (OpenTelemetry)

### 2. Event-Driven Architecture

* EventBus
* Integration Events
* Outbox Pattern
* Idempotency
* Saga Pattern

### 3. Advanced Performance Engineering

* BenchmarkDotNet
* Span<T> and Memory<T>
* Channels
* Async/Await pitfalls

---

## 🟨 V. Stage 5 – TECH LEAD (Foundation for CTO‑Level Thinking)

**Goal:** Make architectural decisions, guide engineers, and design scalable platforms.

### 1. High-Level System Design

* Load Balancing
* Distributed Caching (Redis)
* Message Queues
* CAP Theorem
* Eventual vs Strong Consistency Models

### 2. Cloud & DevOps (Azure-Oriented)

* Azure App Service
* Azure Kubernetes Service (AKS)
* Azure Event Hub
* Azure Service Bus
* CI/CD Pipelines (GitHub Actions / Azure DevOps)

### 3. Observability & SRE Foundations

* Metrics
* Logging
* Tracing
* Alerting

---

## 🟧 VI. Stage 6 – CTO .NET (Master Level)

**Goal:** Architect long-term technology strategy and scale engineering organizations.

### 1. Enterprise Architecture

* Hexagonal Architecture
* Event Sourcing
* Data Mesh
* Zero Trust Architecture
* Compliance Standards: ISO 27001, PCI-DSS

### 2. Product & Technology Strategy

* Technical OKRs
* 3‑Year Technology Roadmap
* Scaling engineering teams
* Technical Debt Governance

### 3. Engineering Leadership

* Coaching engineers
* Build vs Buy decision-making
* Designing systems that remain maintainable for 10+ years

---

# 5. Controls & Governance

Knowledge must be structured, versioned, and continuously improved. Security, architecture, and documentation standards apply across all levels.

(giữ nguyên nội dung cũ)

* Knowledge must be structured and classified.
* Versioning ensures traceability.
* Topics progress from foundational → advanced.
* Security awareness is mandatory.
* Documentation must be reviewed continuously.
* Architecture decisions should use ADRs.

---

# 6. References

* Microsoft Docs
* .NET Platform Architecture Guides
* Azure Architecture Center
* DDD by Eric Evans
* Clean Architecture by Robert C. Martin
* OWASP Standards
* CNCF Observability Models
