# 01 — API Fundamentals

## Why a Product Manager needs API literacy
An API is a contract that lets software systems exchange capabilities and data. A PM does not need to implement every endpoint, but should understand the user or business outcome, the request/response contract, dependencies, failure modes and operational impact.

## REST in practical terms
| Method | Typical intent | Example |
|---|---|---|
| GET | Retrieve a resource | Read a booking |
| POST | Create or trigger an operation | Create a booking |
| PUT | Replace a resource representation | Replace a profile |
| PATCH | Partially update a resource | Change booking contact |
| DELETE | Remove a resource | Delete a saved search |

## HTTP response codes to recognise
- `200 OK`: request succeeded.
- `201 Created`: resource created.
- `202 Accepted`: accepted for asynchronous processing; completion is not guaranteed yet.
- `204 No Content`: succeeded with no response body.
- `400 Bad Request`: malformed or invalid request.
- `401 Unauthorized`: authentication missing or invalid.
- `403 Forbidden`: authenticated caller lacks permission.
- `404 Not Found`: resource or route not found.
- `409 Conflict`: state conflict or duplicate operation.
- `422 Unprocessable Content`: syntactically valid but semantically invalid input.
- `429 Too Many Requests`: rate limit exceeded.
- `500/502/503/504`: server or upstream availability failures.

## Example request
```http
GET /v1/bookings/BK-1042
Authorization: Bearer <access-token>
Accept: application/json
```

Example response:
```json
{
  "bookingId": "BK-1042",
  "status": "CONFIRMED",
  "currency": "INR",
  "totalAmount": 18450,
  "updatedAt": "2026-11-10T10:15:00Z"
}
```

## Product questions to ask
1. Which user journey or business capability does this API enable?
2. Who owns the API and who consumes it?
3. What is the source of truth for each field?
4. What are required, optional and nullable fields?
5. What happens for invalid, duplicate, delayed or partial requests?
6. Are pagination, filtering, sorting and rate limits defined?
7. How are changes versioned and communicated?

## Definition of ready for an API-dependent feature
- Consumer and provider systems identified.
- Endpoint, method, schema and authentication agreed with engineering.
- Success and failure responses documented.
- Data ownership, privacy and retention considered.
- Timeout, retry and duplicate-request behaviour agreed.
- Monitoring, support ownership and acceptance tests defined.

Next: [API documentation and OpenAPI](../02-api-documentation/README.md).