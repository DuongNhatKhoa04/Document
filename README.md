---
title: .NET Backend Learning Hub
author: Personal Engineering Roadmap
status: Active
version: 2.0
last-updated: 2025-12-11
classification: Internal
---

# 1. Purpose
This document defines the official learning structure and documentation hub
for the .NET Backend Roadmap (2025 Edition).  
It organizes all technical knowledge — from core programming to cloud &
microservices — following a structured, high-level format inspired by ISO 27001.

# 2. Scope
This documentation applies to:

- C# fundamentals
- .NET runtime & ecosystem
- Backend & Web API development
- Databases & ORM
- Software architecture & design patterns
- Security & DevSecOps foundations
- Logging, monitoring & observability
- Microservices & distributed systems
- Cloud & DevOps automation
- Engineering leadership & CTO skills

# 3. Definitions
**Fundamentals** — Core programming knowledge required before backend work.  
**Backend Development** — API, database interaction, business logic.  
**Architecture** — System design, patterns, high-level platform structure.  
**Security** — Authentication, authorization, secure coding practices.  
**Observability** — Logging, metrics, tracing, system monitoring.  
**Microservices** — Distributed, event‑driven services communicating over network.

# 4. Documentation Structure (11 Sections, aligned to roadmap)
This documentation follows the official .NET Backend Roadmap 2025:

---

## 4.1 C# Fundamentals
Core language fundamentals for all backend engineers.

- [C# Basics](01-csharp-fundamentals/csharp-basics.md)
- [OOP](01-csharp-fundamentals/oop.md)
- [Generics](01-csharp-fundamentals/generics.md)
- [Collections](01-csharp-fundamentals/collections.md)
- [LINQ](01-csharp-fundamentals/linq.md)
- [Async & Await](01-csharp-fundamentals/async.md)

---

## 4.2 .NET Runtime & Project Fundamentals
- [.NET Runtime](02-dotnet-runtime/runtime.md)
- [CLR & Memory](02-dotnet-runtime/clr-memory.md)
- [Dependency Injection](02-dotnet-runtime/dependency-injection.md)
- [Project Structure](02-dotnet-runtime/project-structure.md)

---

## 4.3 ASP.NET Core Web API
- [API Basics](03-webapi/api-basics.md)
- [Routing & Controllers](03-webapi/routing.md)
- [Middleware](03-webapi/middleware.md)
- [Validation](03-webapi/validation.md)
- [Authentication & Authorization](03-webapi/auth.md)
- [HttpClient / Refit](03-webapi/http-client.md)

---

## 4.4 Entity Framework Core
- [EF Core Basics](04-efcore/efcore-basics.md)
- [LINQ-to-Entities](04-efcore/linq-to-entities.md)
- [Relationships](04-efcore/relationships.md)
- [Tracking & NoTracking](04-efcore/tracking.md)
- [Loading Strategies](04-efcore/loading.md)
- [Performance Optimization](04-efcore/optimization.md)

---

## 4.5 Software Architecture & Clean Architecture
- [Layered Architecture](05-architecture/layered.md)
- [Clean Architecture](05-architecture/clean.md)
- [Domain Model](05-architecture/domain-model.md)
- [Repository & Service Pattern](05-architecture/repository-service.md)

---

## 4.6 Design Patterns (Backend Perspective)
- [Creational Patterns](06-design-patterns/creational.md)
- [Structural Patterns](06-design-patterns/structural.md)
- [Behavioral Patterns](06-design-patterns/behavioral.md)
- [CQRS](06-design-patterns/cqrs.md)
- [EventDriven Patterns](06-design-patterns/event-driven.md)

---

## 4.7 Security (Backend Developer Security Standard)
- [JWT](07-security/jwt.md)
- [OAuth2](07-security/oauth2.md)
- [OWASP Top 10](07-security/owasp-top10.md)
- [Data Protection](07-security/data-protection.md)

---

## 4.8 Database & SQL
- [SQL Basics](08-database/sql-basics.md)
- [Indexes](08-database/indexes.md)
- [Transactions](08-database/transactions.md)
- [Execution Plans](08-database/execution-plan.md)

---

## 4.9 Testing
- [Unit Testing](09-testing/unit.md)
- [Integration Testing](09-testing/integration.md)
- [Mocking Frameworks](09-testing/mocking.md)

---

## 4.10 Logging, Monitoring & Observability
- [Logging Standards](10-observability/logging.md)
- [Distributed Tracing](10-observability/tracing.md)
- [Metrics & Dashboards](10-observability/metrics.md)

---

## 4.11 Microservices & DevOps
- [Microservices Fundamentals](11-microservices-devops/microservices.md)
- [Event-Driven Architecture](11-microservices-devops/event-driven.md)
- [Docker](11-microservices-devops/docker.md)
- [CI/CD](11-microservices-devops/cicd.md)

---

# 5. Controls & Governance
This learning structure follows governance principles inspired by ISO 27001:

- Knowledge must be structured and classified
- Revisions must be traceable (versioning)
- Topics must progress from foundational → advanced
- Security awareness is mandatory
- Documentation must be continuously reviewed & updated

# 6. References
- Microsoft Docs
- DDD by Eric Evans
- Clean Architecture by Robert C. Martin
- OWASP Standards
- Enterprise Cloud Patterns
