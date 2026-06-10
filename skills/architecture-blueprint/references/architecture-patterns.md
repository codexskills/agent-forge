# Architecture Patterns Reference

## Monolith
Single deployable unit containing all application logic.

**Best for:** Teams < 3, simple domain, speed to market, early-stage products.
**Avoid for:** Teams needing independent deploys, complex scaling requirements.
**Characteristics:** Single codebase, single deploy, shared memory, shared database.
**Testing:** Simple — start one process, test end-to-end.
**Operations:** One thing to monitor, one thing to deploy, one thing to scale.

## Modular Monolith
Single deployable unit with enforced internal module boundaries.

**Best for:** Moderate complexity, 2-5 devs, projects that may need to extract services later.
**Avoid for:** Teams needing truly independent scaling of sub-components.
**Characteristics:** Single deploy, module interfaces, shared database but module-level schema ownership.
**Testing:** Modules testable in isolation via interface mocks.
**Operations:** Deploy complexity of monolith with better code organization.

## Microservices
Independent services communicating over network, independently deployable.

**Best for:** Large teams (5+), complex domains, independent scaling needs, polyglot environments.
**Avoid for:** Small teams, early-stage products, simple domains, low ops capacity.
**Characteristics:** Multiple codebases, multiple deploys, network calls between services, eventual consistency.
**Testing:** Complex — requires contract testing, integration test environments.
**Operations:** High overhead — service discovery, monitoring, distributed tracing, orchestration.

## Serverless
Function-per-route architecture, auto-scaling, pay-per-use.

**Best for:** Event-driven workloads, spiky traffic, low ops teams, simple APIs.
**Avoid for:** Long-running processes (>15 min), WebSocket-heavy apps, complex state management, cold-start sensitive apps.
**Characteristics:** Stateless functions, event-driven triggers, managed infrastructure, cold starts.
**Testing:** Local emulation possible but imperfect.
**Operations:** Minimal — provider handles scaling, patching, availability.

## Event-Driven Architecture
Services communicate via asynchronous events through a message broker.

**Best for:** Loose coupling requirements, audit trails, complex workflows with multiple consumers.
**Avoid for:** Simple CRUD apps, real-time request-response requirements.
**Characteristics:** Message broker (Kafka, RabbitMQ, SQS), producers emit events, consumers process asynchronously.
**Testing:** Complex — requires event broker infrastructure, schema evolution management.
**Operations:** Moderate — broker cluster needs monitoring, consumer lag tracking, DLQ management.

## Decision Matrix

| Factor | Monolith | Modular Monolith | Microservices | Serverless | Event-Driven |
|---|---|---|---|---|---|
| Team size | 1-3 | 2-8 | 5+ | Any | 3+ |
| Complexity | Trivial-Simple | Moderate | Complex-Enterprise | Simple-Moderate | Complex |
| Ops comfort | Low | Medium | High | Low | Medium-High |
| Independent scaling | No | No | Yes | Auto | Per-consumer |
| MVP recommendation | Yes | Yes | No | Depends | No |
| Startup cost | Low | Low | High | Low | Medium |
