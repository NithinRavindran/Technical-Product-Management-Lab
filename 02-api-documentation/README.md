**Technical Product Management Lab** · [Home](../README.md) · [Previous: API fundamentals](../01-api-fundamentals/README.md) · [Next: Postman →](../03-postman/README.md)

---

# 02 — API Documentation and OpenAPI

## What good API documentation answers
- What capability does the endpoint expose?
- What method and path should the consumer call?
- What authentication and permissions are required?
- Which fields are required, optional, constrained or sensitive?
- What response codes and error formats can occur?
- Are there rate limits, pagination rules or idempotency requirements?

## Example contract
See [travel-booking-openapi.yaml](travel-booking-openapi.yaml) for a small OpenAPI 3.0 example covering a booking resource.

## Product review checklist
- Endpoint names reflect business resources and actions.
- Request and response examples are realistic but synthetic.
- Date/time format and timezone are explicit.
- Currency and monetary precision are explicit.
- Enumerated values and state transitions are documented.
- Error responses are consistent and actionable.
- Breaking-change and versioning policy is agreed.
- Sensitive fields are not exposed unnecessarily.

## Versioning questions
Prefer a deliberate compatibility policy over changing contracts silently. Discuss whether changes are additive or breaking, how consumers are notified, how long old versions remain supported, and how deprecation is measured.

## Review exercise
For each endpoint, write one positive test, one validation test, one permission test and one dependency-failure test. Ask engineering to confirm expected behaviour before treating the contract as final.

Next: [Postman and API testing](../03-postman/README.md).