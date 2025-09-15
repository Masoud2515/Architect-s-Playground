# 🏗️ Architect’s Playground

█████╗ ██████╗ ██╗ ██╗ ██████╗ ███████╗███╗ ██╗
██╔══██╗██╔══██╗██║ ██║██╔════╝ ██╔════╝████╗ ██║
███████║██████╔╝██║ ██║██║ ███╗█████╗ ██╔██╗ ██║
██╔══██║██╔══██╗██║ ██║██║ ██║██╔══╝ ██║╚██╗██║
██║ ██║██║ ██║╚██████╔╝╚██████╔╝███████╗██║ ╚████║
╚═╝ ╚═╝╚═╝ ╚═╝ ╚═════╝ ╚═════╝ ╚══════╝╚═╝ ╚═══╝

ARCHITECT’S PLAYGROUND
Build. Break. Learn. Repeat. — Together.


> 🧪 A collaborative playground to master modern architecture, observability, security, testing & resilience patterns — one PR at a time.

---

## 🌟 چرا این پروژه؟

هدف ما **ساخت یک محیط امن برای شکستن، یادگیری و رشد جمعی** است.  
اینجا جاییه که:

- هر PR یه فرصت برای یادگیریه.
- هر خطا یه درس جدیده.
- هر لاگ، هر تست، هر Retry — یه قدم به سمت معماری حرفه‌ای.

---

## 🧩 تکنولوژی‌ها و الگوهای مورد استفاده

![CQRS](https://img.shields.io/badge/CQRS-Implemented-blue)
![MediatR](https://img.shields.io/badge/MediatR-Used-green)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-Event--Driven-orange)
![gRPC](https://img.shields.io/badge/gRPC-Inter--Service-red)
![Redis](https://img.shields.io/badge/Redis-Caching-purple)
![Polly](https://img.shields.io/badge/Polly-Resilience-important)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-Observability-blueviolet)
![Prometheus+Grafana](https://img.shields.io/badge/Observability-Prometheus%20%2B%20Grafana-brightgreen)
![Docker](https://img.shields.io/badge/Docker-Containerized-teal)
![ErrorOr](https://img.shields.io/badge/ErrorOr-Explicit%20Errors-success)
![Team Learning](https://img.shields.io/badge/Team-Learning%20Together-success)

✅ **الگوهای طراحی**: CQRS, Mediator, Factory, Strategy, Option, Pipeline  
✅ **امنیت**: JWT, OAuth2, IdentityServer, Policy-Based Auth  
✅ **تاب‌آوری**: Polly (Retry, Circuit Breaker, Timeout, Fallback)  
✅ **اعتبارسنجی**: FluentValidation + Pipeline در MediatR  
✅ **مدیریت خطا**: Exception Handling Middleware + Problem Details + ErrorOr  
✅ **لاگ‌گیری**: Structured Logging با Serilog + TraceId از OpenTelemetry  
✅ **تست**: Unit Test, Integration Test, TDD, Mocking  
✅ **Observability**: OpenTelemetry (Trace, Metric, Log), Prometheus, Grafana, Alertmanager  
✅ **زیرساخت**: Docker, Docker Compose, Health Checks

> 📚 **مستندات کامل فنی**: [`docs/TECH_STACK.md`](./docs/TECH_STACK.md)

---

## 👥 مشارکت کنندگان

این پروژه با همکاری دوستان زیر در حال ساخته شدنه:

- [@Masoud2515](https://github.com/Masoud2515) — نقش: Developer
- [@friend1](https://github.com/friend1) — نقش: ...
- [@friend2](https://github.com/friend2) — نقش: ...

> 💡 **هر کس می‌تونه یه سرویس، یه فیچر، یا حتی یه تست رو بگیره و پیاده‌سازی کنه.**  
> **اصلاحاً: هر کس می‌تونه یه چیزی رو Build کنه، بعد یه نفر دیگه Break کنه، همه Learn کنن، و بعد Repeat!**

---

## 🚀 شروع کار

```bash
git clone https://github.com/your-org/architects-playground.git
cd architects-playground
docker-compose up -d
