# 🧠 TECH STACK: Architect’s Playground

> _"We don’t just use tools — we understand why they exist."_

This document explains the **purpose**, **context**, and **real-world value** of every technology, pattern, and library used in this project.  
It’s not a checklist. It’s a **learning journal**.

---

## 🔧 Core Architecture

| Technology | Purpose | Why Here? |
|----------|---------|-----------|
| **CQRS** | Separates read and write models | Reduces complexity in event-driven systems. Enables scaling reads independently. We use it to model user registration (command) vs. user profile lookup (query). |
| **MediatR** | Implementation of Mediator Pattern | Centralizes request handling. Enables clean pipeline behaviors (validation, logging, retry) via decorators. Makes our handlers testable and composable. |
| **ErrorOr** | Return type for explicit success/error outcomes | Replaces magic strings or exceptions for business errors. Gives us typed results like `Result<User, Error>` — making error handling predictable and testable. |
| **FluentValidation + MediatR Pipeline** | Validation as a cross-cutting concern | Validation is NOT in controllers. It’s a pipeline behavior. Clean, reusable, and testable. No more `[Required]` attributes everywhere! |

---

## 🔄 Event-Driven & Async Communication

| Technology | Purpose | Why Here? |
|----------|---------|-----------|
| **RabbitMQ** | Message broker for async communication | Simulates real microservices communication. Used for events like `UserRegisteredEvent`. Helps decouple services and handle failures gracefully. |
| **gRPC** | High-performance RPC between services | Used for internal service-to-service calls (e.g., Auth → Profile). Faster than HTTP/JSON, strongly-typed, ideal for internal APIs. |
| **Redis** | In-memory caching & distributed locks | Caches frequent queries (e.g., user roles). Also used for distributed locking in critical operations (e.g., preventing duplicate registrations). |

---

## 🛡️ Resilience & Fault Tolerance

| Technology | Purpose | Why Here? |
|----------|---------|-----------|
| **Polly** | Resilience patterns (Retry, Circuit Breaker, Fallback) | We simulate network failures in gRPC calls. Polly lets us: <br> • Retry on transient faults<br> • Break circuit after 5 failures<br> • Fall back to cached data<br> This is how real systems survive chaos. |

---

## 🔍 Observability (The Eyes of the System)

| Technology | Purpose | Why Here? |
|----------|---------|-----------|
| **OpenTelemetry** | Standardized telemetry collection (Traces, Metrics, Logs) | We instrument EVERY service to generate traces across boundaries (HTTP → gRPC → RabbitMQ). No vendor lock-in. |
| **Jaeger** | Distributed tracing visualization | See how a single request flows through User → Auth → Notification. Find slow spans. Understand latency bottlenecks. |
| **Prometheus** | Time-series metrics collector | Collects counters (requests/sec), gauges (active users), histograms (latency). Exposed at `/metrics`. |
| **Grafana** | Dashboarding & alerting | Visualize Prometheus metrics. Create dashboards for: <br> • API latency per service<br> • Error rate trends<br> • Queue depth in RabbitMQ |
| **Serilog + Structured Logging** | Rich, structured logs with `TraceId` | Every log line includes `TraceId` from OpenTelemetry. Search logs by request ID across services. No more “where did this fail?” |

> 💡 **Pro Tip**: A trace ID links your log → metric → trace. That’s observability.

---

## 🐳 Infrastructure & DevOps

| Tool | Purpose |
|------|---------|
| **Docker & Docker Compose** | Containerize all services (APIs, DBs, monitoring tools). One command: `docker-compose up -d` |
| **Health Checks** | Built-in ASP.NET Core health endpoints (`/health`) to monitor service readiness |
| **Alertmanager** | Sends alerts (Slack/email) when Prometheus rules trigger (e.g., >5% error rate for 1 min) |

---

## ✅ Testing Philosophy

| Type | Tools | Goal |
|------|-------|------|
| **Unit Tests** | xUnit, Moq | Test logic in isolation (handlers, validators, services) |
| **Integration Tests** | xUnit, TestServer, TestContainers | Test full flow: HTTP → MediatR → Repository → DB → RabbitMQ |
| **TDD** | Yes! | Write tests BEFORE code. We follow Red-Green-Refactor cycle. |
| **Mocking** | Moq | Mock external dependencies (RabbitMQ, Redis, gRPC clients) to keep tests fast and reliable |

---

## 🔐 Security

| Feature | Implementation |
|--------|----------------|
| **JWT Authentication** | Stateless tokens issued by IdentityServer4 (or lightweight alternative) |
| **OAuth2 Flow** | Password grant for internal apps, refresh tokens |
| **Policy-Based Authorization** | Roles + Claims based permissions (e.g., `RequireClaim("Role", "Admin")`) |

---

## 📌 Key Principles We Live By

- ❌ Don’t use a tool because it’s trendy. Use it because it solves a problem you’ve *felt*.  
- ✅ If you can’t explain *why* you’re using it — you shouldn’t be using it.  
- 📚 **Documentation isn’t optional**. It’s how we scale learning.  
- 🤝 Every PR must answer:  
  > _“What did I learn? What broke? How did I make it better for the next person?”_

---

> 📖 **Next Step**: Pick one component above.  
> Go into the code. Find where it’s used.  
> Then ask: _“How would this break in production?”_  
> Now fix it. Or break it on purpose.  
> **That’s how architects are made.**
