**Technical Product Management Lab** · [Home](../README.md) · [Previous: System design](../04-system-design/README.md) · [Next: Technical requirements →](../06-technical-requirements/README.md)

---

# 05 — Integration Patterns and Failure Handling

Integrations are product dependencies. A polished user journey can still fail when a supplier, payment provider, identity service or downstream platform is slow or inconsistent.

## Patterns to understand
- **Timeout:** stop waiting after a defined limit; surface a controlled outcome.
- **Retry:** repeat transient failures with bounded attempts and backoff.
- **Idempotency:** make repeated requests safe against duplicate side effects.
- **Circuit breaker:** temporarily stop calls to an unhealthy dependency.
- **Queue / asynchronous processing:** decouple work that need not finish in the user request.
- **Webhook:** receive an event from an external system; validate authenticity and handle duplicates.
- **Reconciliation:** compare internal and external records to resolve uncertain or mismatched outcomes.

## Failure-handling decision table
| Scenario | Product behaviour to define | Engineering considerations |
|---|---|---|
| Supplier timeout before booking outcome known | Show pending status; avoid claiming success or failure | Reconciliation, idempotency, status query |
| Supplier returns unavailable | Offer alternatives and preserve user context | Map supplier error to domain reason |
| Duplicate webhook | Do not duplicate state transition | Event ID deduplication |
| Invalid credentials | Explain service issue without exposing secrets | Credential rotation and alerting |
| Rate limit | Communicate temporary delay where needed | Respect retry-after and backoff |
| Partial downstream failure | Define recoverable state and support path | Saga/compensation or manual queue |

## Product acceptance checklist
- User sees a truthful status.
- No duplicate booking, payment or incident is created by retries.
- Every failure has a defined next action.
- Support teams can trace the operation.
- Alerts identify sustained dependency degradation.
- Recovery and reconciliation ownership is explicit.

See [travel booking API integration](../07-product-case-studies/travel-booking-api-integration.md) for an applied example.