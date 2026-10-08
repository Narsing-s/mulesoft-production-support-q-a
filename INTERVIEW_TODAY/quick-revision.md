# MuleSoft Customer Interview — Quick Revision

## 30-second introduction

> I have around 4 years of IT experience, with around 3 years focused on MuleSoft. My core experience is L2/L3 production support for enterprise integration applications and APIs. I work on monitoring, incident troubleshooting, log analysis, connectivity and authentication issues, application restarts, deployments, post-deployment validation, RCA and coordination with development and infrastructure teams for permanent fixes.

## Production troubleshooting flow

**Impact → Severity/SLA → Correlation ID → Monitoring → Logs → Failing layer → Recovery → Validation → Monitoring → RCA → Prevention**

## Tools to mention

- Anypoint Monitoring
- Runtime Manager
- Splunk
- ELK
- Dynatrace where applicable
- Mule application logs
- API Manager where applicable

## HTTP status quick recall

| Code | Meaning | Support focus |
|---|---|---|
| 400 | Bad Request | Payload/request validation |
| 401 | Unauthorized | Authentication/token/credentials |
| 403 | Forbidden | Authorization/permissions/policies |
| 404 | Not Found | Endpoint/path/resource |
| 408 | Request Timeout | Timeout/network/downstream latency |
| 429 | Too Many Requests | Rate limit/throttling |
| 500 | Internal Server Error | Identify Mule vs downstream |
| 502 | Bad Gateway | Gateway/upstream dependency |
| 503 | Service Unavailable | Service availability/dependency |
| 504 | Gateway Timeout | Upstream/downstream timeout |

## Error handling

**On Error Continue**
- Handles the error and continues from the error handler.
- Caller can receive successful completion depending on flow behavior.

**On Error Propagate**
- Handles the error and propagates it to the caller.
- Transaction remains failed.

## Retry vs Circuit Breaker

**Retry:** Try the operation again because the failure may be temporary.

**Circuit breaker:** Stop repeatedly calling an unhealthy dependency and allow recovery time before testing again.

## Restart rule

Never say: “I restart whenever the API fails.”

Say:

> “I first determine whether Mule is unhealthy. I restart only when there is an approved operational reason and after considering transaction/message impact.”

## RCA

Remember:

**Timeline → Impact → Evidence → Root cause → Immediate fix → Corrective action → Preventive action**

## Deployment validation

**Deployment status → Startup logs → Configuration → Connectivity → Health check → Smoke test → Business transaction → Monitoring**

## Customer communication

Be:
- factual
- concise
- evidence-based
- SLA-aware
- transparent about what is confirmed vs under investigation

## If you don't know an answer

> “I haven't worked on that directly in production, but based on my MuleSoft support experience, my approach would be…”

Do not bluff.
