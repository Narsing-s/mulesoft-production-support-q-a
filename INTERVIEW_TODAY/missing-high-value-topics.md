# Missing High-Value Customer Interview Topics

This file adds topics not already covered in the interview pack. Focus on practical production-support answers.

## 1. How do you troubleshoot a DLQ or backout queue?

**Answer:** I first identify the message age, volume, business impact, producer/consumer, and whether the failure is transient or data-related. I inspect the original error and correlation/message ID, verify whether the consumer application is healthy, and check if messages are repeatedly failing. For safe recovery, I fix the underlying issue first, then reprocess messages in a controlled manner with duplicate/idempotency checks. I validate successful business processing and monitor the queue afterward. I do not blindly replay the entire DLQ.

## 2. What is the difference between a DLQ and a backout queue?

A **DLQ** is commonly used to isolate messages that cannot be delivered or processed successfully after the configured failure handling. A **backout queue** is commonly associated with IBM MQ message backout handling, where repeatedly failing messages are moved away from the main input queue. Exact behavior depends on the MQ/application configuration.

## 3. How would you reprocess DLQ messages safely?

1. Confirm root cause is fixed.
2. Identify affected message range and business impact.
3. Preserve the original message and metadata.
4. Check whether the transaction is already processed.
5. Reprocess in controlled batches where possible.
6. Monitor consumer/application/queue metrics.
7. Validate downstream business results.
8. Record the number successful, failed, and remaining.

## 4. How do you handle duplicate messages?

I first determine whether the duplicate originated from producer retry, consumer retry, timeout ambiguity, redelivery, or manual reprocessing. I check correlation/business keys and processing history. If the integration supports idempotency, I use the business key or message identifier to prevent duplicate processing. For manual recovery, I verify whether the target transaction already exists before replaying it.

## 5. What is idempotency in integration support?

An operation is idempotent when repeating the same request does not create an unintended additional business effect. In production support, this is especially important during retries, timeout recovery, DLQ replay, and manual reprocessing.

## 6. How do you troubleshoot an IBM MQ message not being consumed?

I check queue depth, consumer application status, channel/connectivity status, credentials, listener/consumer configuration, message age, message format, and application logs. I then correlate the message timestamp/ID with Mule and MQ logs. If the consumer is stopped, I follow the approved restart/recovery procedure; if the message itself is malformed, I isolate it rather than repeatedly retrying it.

## 7. How do you troubleshoot SFTP file failures?

I check whether the file was produced, source/destination path, filename/pattern, file size, permissions, credentials, SSH/TLS/certificate status as applicable, connectivity, and whether the file is locked or partially written. I correlate timestamps and transfer IDs with Mule logs and confirm whether the downstream system received the file. I avoid duplicate delivery during manual retry.

## 8. What do you check for a TLS/certificate issue?

I confirm the exact error, endpoint, certificate validity/expiry, certificate chain/truststore, hostname/SAN match, protocol/cipher compatibility, and whether the issue started after a certificate rotation. I compare the failing endpoint with a known-good endpoint and coordinate certificate replacement through the approved change process. After updating the certificate, I perform both connectivity and business validation.

## 9. What is the difference between authentication and authorization?

**Authentication** verifies who the caller is. **Authorization** verifies what that caller is allowed to access. For example, an invalid token can cause authentication failure, while a valid token without the required permission can result in authorization failure.

## 10. How do API policies affect production troubleshooting?

Policies can reject or alter traffic before the business flow executes. I check client ID/secret, OAuth/token validation, rate limiting, SLA policies, IP restrictions, CORS where relevant, and policy-related HTTP responses. If the Mule flow shows no execution for a request, I also consider gateway/API policy enforcement rather than assuming the application flow is broken.

## 11. What would you check for HTTP 429?

HTTP 429 normally indicates that the caller has exceeded a configured request limit. I check policy/rate-limit metrics, request volume, retry behavior, and whether clients are retrying too aggressively. I avoid increasing limits blindly; I first understand the agreed SLA and traffic pattern.

## 12. What would you check for HTTP 502 vs 503 vs 504?

- **502:** gateway/proxy received an invalid response from an upstream service.
- **503:** service is unavailable or unable to handle the request.
- **504:** gateway/proxy timed out waiting for an upstream response.

I correlate gateway, Mule, and downstream timestamps before deciding where the failure occurred.

## 13. How do you troubleshoot a DataWeave transformation failure?

I capture the exact error and payload structure, identify the failing DataWeave expression, and compare the actual payload against the expected schema. I check null/missing fields, data types, arrays/objects, date formats, and unexpected source values. For production, I protect sensitive data and use a representative sanitized payload when reproducing.

## 14. How do you troubleshoot a flow that is processing slowly?

I compare current latency with the baseline and identify where time is spent: inbound request, transformation, database, external API, MQ, SFTP, or other connector. I check CPU, memory, thread/concurrency indicators, downstream latency, payload size, and recent deployments. I do not immediately increase workers; first I identify the bottleneck.

## 15. What is backpressure?

Backpressure is a mechanism by which a system prevents producers from overwhelming downstream consumers. In integration platforms, it helps control throughput when processing capacity is lower than incoming traffic. During an incident, I look for queue buildup, latency, rejected requests, and resource pressure.

## 16. How do you handle a production deployment validation?

I verify deployment status, application health, logs, configuration, properties/secrets, connectivity, certificates, and policies. Then I perform a smoke test and a representative business transaction. I monitor errors and latency for a defined period and confirm downstream processing. Deployment status alone is not considered successful business validation.

## 17. What if deployment succeeded but the API is returning 404?

I first confirm the application is running and the listener is started. Then I verify the HTTP listener host/port, base path, API path, RAML/router configuration, deployed properties, and exact URL/method. I also check whether a gateway or proxy is exposing a different base path. I reproduce with the exact method and URL rather than testing only the root path.

## 18. How do you distinguish a MuleSoft issue from a downstream issue?

I follow the transaction path and use evidence. If Mule receives the request and fails before calling the downstream system, Mule/configuration/transformation is likely involved. If Mule successfully reaches the downstream endpoint and receives a timeout/5xx, I investigate the downstream service and network path. I communicate the finding as evidence, not assumption.

## 19. How do you handle a customer saying "everything is down"?

I acknowledge the impact, establish scope using monitoring and transaction data, identify whether the issue affects all APIs or a subset, and determine the common dependency. I provide factual updates with impact, current findings, mitigation, and next action. I avoid making an unverified root-cause statement during the initial incident.

## 20. How do you handle a production issue during shift handover?

I provide current impact/severity, incident timeline, correlation IDs, affected applications, investigation completed, evidence collected, current hypothesis, actions already taken, pending actions, business/customer contacts, and next checkpoint. The receiving engineer should be able to continue without restarting the investigation.

## 21. What is the difference between incident, problem, and change?

- **Incident:** restore service or reduce business impact.
- **Problem:** identify and eliminate the underlying cause of recurring incidents.
- **Change:** controlled modification to production to fix, improve, or prevent an issue.

A good support process connects all three: restore first, determine root cause, then implement an approved permanent change.

## 22. What makes a good RCA?

A good RCA clearly states impact, detection time, timeline, technical root cause, contributing factors, why monitoring did or did not detect it, recovery actions, permanent fix, and preventive actions. It should be evidence-based and avoid assigning blame.

## 23. How do you prioritize multiple P1/P2 incidents?

I prioritize using business impact, number of affected users/transactions, SLA, regulatory or financial impact, and availability of workarounds. I communicate ownership and escalation clearly and make sure lower-priority incidents are not silently abandoned.

## 24. What production metrics do you monitor?

I look at request/transaction volume, success and error rate, response time/latency, throughput, CPU, memory, queue depth, message age, application availability, downstream failures, and recurring error patterns. The exact metrics depend on the integration architecture.

## 25. What is the difference between a health check and a business smoke test?

A health check proves that the application/runtime is available. A business smoke test proves that a representative business transaction actually works end-to-end. Both are needed after important production changes.

## 26. What is your approach when you cannot reproduce a production issue?

I preserve evidence: timestamps, correlation IDs, request/response metadata where permitted, logs, metrics, queue state, downstream responses, deployment/configuration changes, and affected business keys. I compare successful and failed transactions and look for timing, data, volume, or dependency differences. Intermittent does not mean impossible to diagnose; it means evidence collection becomes more important.

## 27. Customer asks you to restart immediately. What do you do?

I first confirm impact and capture enough evidence to avoid losing diagnostic information. If restart is an approved recovery action and the application is genuinely unhealthy, I restart it and validate business functionality afterward. If the problem is clearly a healthy Mule app waiting on a failed dependency, I avoid an unnecessary restart and explain the evidence.

## 28. Strong customer-facing closing statement

"My approach in production support is to restore service safely, communicate clearly, use monitoring and logs to isolate the failing layer, validate the business transaction after recovery, and then drive RCA and preventive action so the issue does not keep recurring."
