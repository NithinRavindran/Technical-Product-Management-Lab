**Technical Product Management Lab** · [Home](../README.md) · [Previous: API documentation](../02-api-documentation/README.md) · [Next: System design →](../04-system-design/README.md)

---

# 03 — Postman and API Testing

## Purpose
A Postman collection makes API scenarios repeatable for product, QA and engineering reviews. The sample collection in this folder uses a reserved `.example.test` host and synthetic identifiers; it will not call a real service.

## Suggested environment variables
| Variable | Example | Handling |
|---|---|---|
| `baseUrl` | `https://api.example.test/v1` | Non-secret |
| `accessToken` | Set locally | Secret; never commit |
| `bookingId` | `BK-1042` | Synthetic test ID |

## Test scenarios
1. Retrieve a known booking — expect 200 and required response fields.
2. Retrieve an unknown booking — expect 404.
3. Create a booking with missing traveller ID — expect validation failure.
4. Create a booking without authentication — expect 401.
5. Retry a create request with the same idempotency key — verify no duplicate booking.
6. Simulate provider timeout — verify user-facing status and support traceability.

## What a PM should inspect
- Are scenarios aligned with acceptance criteria?
- Are test data and environment safe?
- Are negative paths covered?
- Can QA correlate a request with logs using a trace or correlation ID?
- Is the expected behaviour agreed for asynchronous or uncertain outcomes?

Import [booking-api.postman_collection.json](booking-api.postman_collection.json) into Postman to inspect the example requests. It uses a placeholder domain and requires a real test environment to execute.