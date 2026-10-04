# Advanced MuleSoft Production Support Scenarios

## Scenario 51 — Error rate increases after a traffic spike
**Question:** Traffic suddenly doubles and error rate rises. What do you check?

**Answer:** I compare traffic, throughput, latency, CPU, memory, thread usage, connection pools, and downstream response time. I determine whether the application or a dependency reached capacity. I then apply controlled scaling or throttling according to the approved design and verify recovery.

## Scenario 52 — Only one API resource is failing
**Question:** The application is healthy, but one endpoint fails while others work. What does that suggest?

**Answer:** I narrow the scope to that resource. I compare its routing, policy, transformation, downstream endpoint, payload, and recent changes with working resources. This prevents unnecessary application-wide restarts.

## Scenario 53 — Error occurs only for one customer
**Question:** One customer fails while all others succeed. How do you investigate?

**Answer:** I compare the customer's payload, credentials, entitlements, configuration, business data, and downstream response with a successful customer. I check whether the issue is data-specific or authorization-specific before changing shared application configuration.

## Scenario 54 — Messages are processed out of order
**Question:** Business requires ordering, but messages are arriving out of order. What do you check?

**Answer:** I check queue configuration, concurrent consumers, parallel processing, partitioning, retries, and downstream ordering rules. If ordering is a business requirement, I ensure the processing design preserves the required sequence rather than increasing concurrency blindly.

## Scenario 55 — Retry succeeds but creates duplicates
**Question:** A retry succeeds after the first request actually completed. How do you handle it?

**Answer:** I verify the original transaction status and identify the duplicate side effect. Then I use idempotency or reconciliation to prevent future duplicates. The key issue is distinguishing “request timed out” from “business operation failed.”

## Scenario 56 — Downstream returns 200 with an error in the body
**Question:** The downstream API returns HTTP 200 but its payload says the transaction failed. What should Mule do?

**Answer:** Mule should validate the business response, not rely only on the HTTP status. If the contract defines the response as a business failure, the flow should handle it consistently, potentially raising a business error and recording the transaction status for reconciliation.

## Scenario 57 — API works directly but fails through gateway
**Question:** Direct testing succeeds, but gateway traffic fails. Where do you investigate?

**Answer:** I compare gateway policies, base paths, authentication, headers, rate limits, TLS, routing, and request transformation. If direct traffic reaches Mule successfully, I focus first on the gateway/client path rather than changing Mule business logic.

## Scenario 58 — Application starts but scheduler remains inactive
**Question:** The application is running, but scheduled processing never starts. What do you verify?

**Answer:** I verify scheduler configuration, timezone, enabled state, deployment configuration, runtime logs, and whether the flow is blocked by an initialization or dependency problem. I also check whether another deployment or operational setting disabled the schedule.

## Scenario 59 — Large payload causes timeout
**Question:** Small requests succeed but large payloads time out. What do you investigate?

**Answer:** I compare payload size with processing time and inspect streaming, memory, transformation complexity, network transfer time, downstream limits, and timeout settings. I optimize processing where possible instead of simply increasing the timeout.

## Scenario 60 — API suddenly receives malformed requests
**Question:** A consumer starts sending malformed payloads. How do you respond?

**Answer:** I confirm the contract violation and identify whether the malformed requests are isolated or widespread. I return the correct validation response, capture enough evidence for the consumer team, and avoid weakening validation just to make invalid traffic pass.

## Scenario 61 — Deployment changed configuration accidentally
**Question:** After deployment, the code is correct but the endpoint points to the wrong environment. What do you check?

**Answer:** I compare environment properties, secure properties, deployment variables, endpoint configuration, and artifact version. I correct the configuration through the approved deployment process and perform an end-to-end smoke test.

## Scenario 62 — Connection pool is healthy but requests hang
**Question:** DB connections are available, but requests still hang. What else do you investigate?

**Answer:** I check query execution, database locks, transaction scope, thread availability, downstream calls, network latency, and application logic. Available connections do not prove that transactions can complete quickly.

## Scenario 63 — One message repeatedly fails after every deployment
**Question:** A specific message fails even after redeployment. What does that suggest?

**Answer:** It suggests the issue may be data-specific or a deterministic business/validation problem rather than a transient runtime problem. I inspect the message and error details, quarantine it if appropriate, and avoid repeated retries that provide no value.

## Scenario 64 — Monitoring alert fires but users see no impact
**Question:** A CPU alert fires but there are no business failures. What do you do?

**Answer:** I validate whether the alert threshold represents real risk by checking latency, error rate, throughput, memory, and business KPIs. I do not declare an incident solely from one metric; I assess whether user impact or imminent capacity risk exists.

## Scenario 65 — Users report duplicate emails
**Question:** A notification API sends the same email multiple times. How do you troubleshoot?

**Answer:** I trace the notification ID and business key, inspect scheduler retries, message redelivery, API retries, and downstream email-provider behavior. I determine where the duplicate was generated and introduce idempotency or deduplication at the correct layer.

## Scenario 66 — Queue backlog clears but failures remain
**Question:** The queue is empty, but business transactions are still failing. What does that mean?

**Answer:** Queue depth alone is not a success metric. I inspect processing outcomes, dead-letter messages, downstream acknowledgements, error logs, and business reconciliation. A message can leave the queue and still fail downstream.

## Scenario 67 — A certificate was renewed but TLS still fails
**Question:** The certificate was renewed, but the application still reports SSL handshake failure. What do you check?

**Answer:** I verify that the new certificate is installed in the correct keystore/truststore, the correct alias is being used, the full chain is present, passwords are correct, and the deployed runtime is using the updated configuration. I also verify whether a restart/redeployment is required by the platform.

## Scenario 68 — Production issue follows a runtime upgrade
**Question:** An application became unstable after a runtime upgrade. How do you investigate?

**Answer:** I correlate the timing with the upgrade and compare runtime versions, connector versions, configuration, logs, resource metrics, and known compatibility differences. If impact is severe and rollback is approved, I restore the last known-good runtime/application version while RCA continues.

## Scenario 69 — Business asks you to replay everything
**Question:** Business asks you to replay all failed transactions immediately. What do you say?

**Answer:** I first classify failures and verify idempotency and transaction state. Replaying everything can create duplicates or repeat irreversible side effects. I propose a controlled replay of only transactions confirmed safe to reprocess, with monitoring and reconciliation.

## Scenario 70 — You find the root cause but no immediate fix
**Question:** You know the root cause, but the permanent fix needs development time. What do you do?

**Answer:** I document the confirmed RCA, apply the safest available workaround if approved, assess residual risk, and create a permanent remediation plan. I communicate the workaround's limitations and track the problem until the permanent fix is deployed and verified.

## Scenario 71 — High latency is isolated to one region
**Question:** One deployment region is slow while another is healthy. What do you compare?

**Answer:** I compare regional traffic, workers, runtime metrics, network path, DNS, downstream endpoints, configuration, and infrastructure health. Regional comparison is useful because it provides a healthy baseline.

## Scenario 72 — Error starts after a policy update
**Question:** API failures begin immediately after an API policy change. What do you do?

**Answer:** I compare policy configuration before and after the change and identify affected clients, endpoints, and response codes. If the change is confirmed as the cause and rollback is approved, I revert safely and validate client traffic.

## Scenario 73 — Incident has no obvious error message
**Question:** There is no clear error message, only failed business transactions. How do you investigate?

**Answer:** I start with transaction IDs, timestamps, response codes, payload patterns, monitoring, and downstream acknowledgements. I trace the complete path and look for missing or inconsistent evidence rather than waiting for a single obvious exception.

## Scenario 74 — Support team has no runbook
**Question:** A recurring incident has no documented recovery procedure. What would you do?

**Answer:** After safely resolving the incident, I document symptoms, detection, checks, approved mitigation, validation steps, escalation contacts, and rollback considerations. A runbook reduces recovery time and makes future handling consistent.

## Scenario 75 — Same incident keeps returning
**Question:** The incident has happened three times with the same symptom. What is your next step?

**Answer:** I open or update a problem/RCA record and compare all incident timelines. I identify the common trigger and permanent remediation instead of treating each occurrence as an isolated ticket. Repeated incidents are strong evidence that the workaround is not enough.
