# 06 — HTTP, REST & APIkit

## Slide 1 — REST and HTTP
**REST** is an architectural style for resource-oriented APIs. HTTP provides methods, status codes, headers and transport behavior.

In production support, do not troubleshoot only from the status code. Check the complete path: client → gateway/API policy → Mule listener/APIkit → flow → downstream system → response.

## Slide 2 — HTTP Listener
The HTTP Listener accepts inbound requests on a configured host, port and path.

When an endpoint is unreachable, verify:
- application is started
- listener is bound to the expected port
- path/base path is correct
- APIkit/router configuration is correct
- environment properties are loaded
- gateway/ingress route is correct

## Slide 3 — RAML vs APIkit
RAML describes the API contract: resources, methods, parameters, request/response structures and examples.

APIkit can use the contract to route requests to Mule flows and validate API behavior.

**Interview point:** RAML defines the contract; APIkit helps implement/enforce that contract inside Mule.

## Slide 4 — 401 vs 403
**401 Unauthorized:** authentication credentials are missing, invalid or expired.

**403 Forbidden:** the caller is authenticated, but the requested operation is not permitted.

Troubleshooting:
1. confirm request headers/token
2. verify token expiry/issuer/audience
3. identify policy or authorization layer
4. compare with a known-good request
5. check recent policy/credential changes

## Slide 5 — 404 After Deployment
A 404 does not automatically mean the application is down.

Check:
1. Runtime Manager application status
2. startup logs
3. listener host/port/path
4. base path and APIkit configuration
5. environment-specific properties
6. gateway/ingress path
7. exact URL being tested

## Slide 6 — Intermittent 500
First determine whether failures correlate with:
- specific payloads
- specific downstream systems
- traffic spikes
- time windows
- connection-pool exhaustion
- recent deployment/configuration changes

Use correlation IDs to compare successful and failed transactions. Find the **first meaningful error**, not only the final HTTP 500.

## Slide 7 — 429 Too Many Requests
429 normally indicates rate limiting or throttling.

Investigate:
- request volume
- policy limits
- client behavior/retry loops
- downstream limits
- whether multiple consumers share the same quota

Do not immediately increase retries. That can create a retry storm.

## Slide 8 — Timeouts
Separate:
- connection timeout: unable to establish connection
- response/read timeout: connection exists but response is too slow
- Mule processing timeout: application processing exceeds allowed time

Check DNS/network/TLS, downstream latency, connection pools, payload size and recent traffic changes.

## Slide 9 — Questions 49–56
49. What is REST?
50. What is RAML?
51. What is APIkit?
52. What is an HTTP Listener?
53. Explain 401 vs 403.
54. How do you troubleshoot a 404 after deployment?
55. How do you troubleshoot intermittent 500?
56. How do you handle 429 and timeout conditions?

## Slide 10 — Interview Takeaway
For HTTP incidents, answer in this order:

**Status code → correlation ID → listener/API layer → Mule flow → downstream dependency → configuration/security → recent changes → safe mitigation → verification.**
