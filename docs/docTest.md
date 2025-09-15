
---

## 📂 `docs/TECH_STACK.md`

```md
# 🧩 مستندات فنی — Architect’s Playground

## 🎯 هدف

مستندسازی دقیق تکنولوژی‌ها، الگوها و نحوه پیاده‌سازی هر بخش برای تسهیل یادگیری و مشارکت تیم.

---

## 🧱 ساختار کلی پروژه
architects-playground/
├── src/
│ ├── Services/
│ │ ├── IdentityService/
│ │ ├── OrderService/
│ │ └── PaymentService/
│ └── Shared/ # کتابخانه‌های مشترک
├── tests/ # Unit & Integration Tests
├── infra/ # Docker, Prometheus, Grafana, RabbitMQ
├── docs/ # مستندات
├── docker-compose.yml
└── README.md

---

## 🧰 تکنولوژی‌ها و نحوه استفاده

### 1. CQRS + MediatR

- هر Command/Query در پوشه `Application/Commands` یا `Application/Queries`
- Handlerها در `Application/Handlers`
- Pipelineها (Validation, Logging) در `Application/PipelineBehaviors`

### 2. اعتبارسنجی (Validation)

- با `FluentValidation`
- هر Command/Query یه Validator داره
- Validation در Pipeline اجرا میشه — قبل از Handler
- خطاها به صورت `ProblemDetails` یا `ErrorOr` برگردونده میشن

### 3. مدیریت خطا (Exception Handling)

- `ExceptionHandlingMiddleware` تمام خطاها رو جمع‌آوری و استانداردسازی می‌کنه
- خطاها با `ProblemDetails (RFC 7807)` برگردونده میشن
- لاگ‌گیری کامل از Exception + StackTrace + TraceId

### 4. ErrorOr

- استفاده از `ErrorOr<T>` برای بازگشت خطاهای منطقی بدون Exception
- تعریف خطاها به صورت استاتیک و معنادار
- تبدیل ValidationException به ErrorOr در Pipeline
- استفاده از `.Match(...)` در Controller برای برگردوندن پاسخ مناسب

### 5. لاگ‌گیری (Logging)

- با `Serilog`
- لاگ‌های Structured با Json
- لاگ‌ها شامل `TraceId`, `SpanId` از OpenTelemetry
- خروجی: Console, File, Seq (اختیاری)

### 6. تاب‌آوری (Polly)

- Policyها در `Shared/Resilience` تعریف میشن
- Policyهای پیش‌فرض: `Retry`, `CircuitBreaker`, `Timeout`
- Policyها روی فراخوانی‌های gRPC و خارجی اعمال میشن
- Metrics از وضعیت Circuit Breaker و تعداد Retryها جمع‌آوری میشه

### 7. Observability

- `OpenTelemetry` برای Trace و Metric
- `Jaeger` برای نمایش Traceها
- `Prometheus` برای جمع‌آوری Metricها
- `Grafana` برای داشبورد
- `Alertmanager` برای ارسال هشدار

### 8. امنیت

- `JWT` برای Authentication
- `Policy-Based Authorization`
- `IdentityServer4/Duende` برای OAuth2 (اختیاری)
- `Rate Limiting` با `AspNetCoreRateLimit`

### 9. تست

- `xUnit` برای Unit Test
- `TestContainers` برای Integration Test با دیتابیس واقعی
- `Moq` برای Mocking
- `TDD` تشویق میشه — تست قبل از کد!

---

## 📈 Metrics & Monitoring

| Metric                  | توضیحات                          | ابزار نمایش |
|-------------------------|----------------------------------|-------------|
| `http.server.request.duration` | زمان پاسخ APIها               | Grafana     |
| `circuit_breaker_state` | وضعیت Circuit Breaker           | Grafana     |
| `retry_count_total`     | تعداد Retryها                   | Grafana     |
| `log_events_total`      | تعداد لاگ‌های Error/Warning     | Grafana     |
| `trace_count`           | تعداد Traceهای ثبت شده          | Jaeger      |

---

## 🧭 راهنمای پیاده‌سازی هر بخش

می‌تونی برای هر سرویس یه فایل مثل `docs/guides/identity-service.md` بسازی و نحوه پیاده‌سازی رو توضیح بدی — شامل:

- ساختار پوشه
- نحوه استفاده از MediatR
- نحوه افزودن Validation
- نحوه استفاده از ErrorOr
- نحوه لاگ‌گیری
- نحوه تست‌نویسی
- نحوه اتصال به Observability

---

## 📚 منابع آموزشی

- [MediatR Documentation](https://github.com/jbogard/MediatR)
- [Polly Documentation](https://github.com/App-vNext/Polly)
- [OpenTelemetry .NET](https://opentelemetry.io/docs/instrumentation/net/)
- [FluentValidation](https://docs.fluentvalidation.net/)
- [Serilog](https://serilog.net/)
- [ErrorOr GitHub](https://github.com/amantinband/error-or)
