**Technical Product Management Lab** · [Home](../README.md) · [Previous: Integrations](../05-integrations/README.md) · [Next: Case studies →](../07-product-case-studies/README.md)

---

# 06 — Technical Product Requirements

## Example feature brief: reliable booking creation

### Problem
A traveller may submit a booking request while an external supplier is slow or returns an uncertain response. Without a clear state and recovery path, users may submit again and create duplicate operations or lose confidence.

### Outcome
Provide an accurate booking status and a safe recovery path when supplier confirmation is delayed.

### Scope
- Submit booking request with a unique idempotency key.
- Persist a traceable booking record.
- Represent pending, confirmed, failed and cancellation states.
- Reconcile uncertain supplier outcomes.
- Expose status to the consuming application.

### Out of scope
- Supplier commercial negotiation.
- Redesign of the complete travel search experience.
- Automatic compensation without agreed business rules.

### User story
As a traveller, I want to see whether my booking is confirmed or still being processed, so that I do not submit the same booking again unnecessarily.

### Acceptance criteria (Given / When / Then)
1. **Successful booking:** Given a valid offer, when the supplier confirms, then the booking is stored as CONFIRMED and a supplier reference is available.
2. **Supplier rejection:** Given the supplier rejects the request, when the response is received, then the booking is stored as FAILED with a safe, actionable reason.
3. **Unknown outcome:** Given the supplier does not respond before timeout, when the request expires, then the booking is marked pending reconciliation and the user is not told it failed.
4. **Duplicate submission:** Given the same idempotency key is reused, when the request is repeated, then the system returns the original operation outcome without creating a second booking.
5. **Unauthorised request:** Given the caller lacks valid authentication, when the endpoint is called, then the request is rejected without exposing booking data.

### Non-functional requirements to agree
- Response-time target and percentile.
- Availability and recovery objectives.
- Data retention and audit requirements.
- Access control and encryption.
- Peak request volume and rate limits.
- Monitoring, trace IDs and alert thresholds.

### Dependencies and risks
| Dependency / risk | Mitigation to discuss |
|---|---|
| Supplier API behaviour differs | Contract tests and supplier-specific mapping |
| Timeout leaves uncertain state | Reconciliation workflow |
| Duplicate requests | Idempotency and deduplication |
| Sensitive traveller data | Data minimisation and access controls |

### Definition of done
- Contract and error responses reviewed.
- Positive, negative and duplicate-request tests pass.
- Logs and alerts are available.
- Support runbook and ownership agreed.
- Product acceptance criteria demonstrated in test environment.

This is an illustrative requirements exercise, not an employer specification.