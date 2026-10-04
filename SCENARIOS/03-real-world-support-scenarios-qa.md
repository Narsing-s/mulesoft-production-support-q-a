# Real-World MuleSoft L2/L3 Support Scenarios

## Scenario 76 — File published but consumer cannot process it
**Question:** Mule successfully publishes a file, but the consumer says it never processed it. What do you check?

**Answer:** I verify the publish transaction, destination queue/path, message/file identifier, consumer status, backlog, and downstream processing logs. I separate “Mule published successfully” from “consumer processed successfully” and reconcile the handoff.

## Scenario 77 — Consumer stopped during a business-critical window
**Question:** A consumer stops during a critical business window. What is your priority?

**Answer:** I assess business impact, confirm the stopped state, check backlog growth, and follow the approved restart/escalation procedure. After recovery I monitor consumption and validate downstream completion rather than stopping at “consumer is running.”

## Scenario 78 — Files fail intermittently with no application exception
**Question:** File placement fails intermittently, but Mule logs show no useful exception. What do you do?

**Answer:** I verify whether the operation reached Mule, then inspect SFTP/server, network, DNS, permissions, file locks, and transfer-side evidence. I compare successful and failed timestamps and collect evidence for the owning infrastructure team.

## Scenario 79 — API receives traffic but no business records are created
**Question:** Monitoring shows requests and HTTP 200 responses, but the database has no expected records. What do you investigate?

**Answer:** I trace the transaction through routing, transformation, DB execution, transaction boundaries, and response handling. I verify that the correct database/environment is being used and that the business success response is not being returned before persistence is actually confirmed.

## Scenario 80 — Authentication failure begins after secret rotation
**Question:** Authentication started failing immediately after a secret rotation. What is your approach?

**Answer:** I correlate the failure with the rotation, verify the new secret through the approved secret-management process, confirm the application is reading the updated value, and test connectivity. I never paste credentials into source code, tickets, or chat.

## Scenario 81 — P1 has multiple possible causes
**Question:** During a P1, you find three possible causes. How do you proceed?

**Answer:** I prioritize hypotheses based on impact and evidence. I test the safest, fastest checks first while maintaining parallel investigation tracks. I communicate confirmed facts separately from hypotheses so stakeholders understand the current confidence level.

## Scenario 82 — Reprocessing could affect business twice
**Question:** A failed transaction may have actually succeeded downstream. Can you reprocess it?

**Answer:** Not until I determine the transaction's actual business state. I check downstream status and reconciliation records and use an idempotency key or business transaction ID where available. If the state cannot be confirmed, I escalate rather than creating a duplicate side effect.

## Scenario 83 — API policy and backend both show errors
**Question:** Some requests fail at the policy layer while others fail in the backend. How do you separate them?

**Answer:** I classify transactions by response code and correlation information. Policy failures are investigated at the gateway/security layer, while backend failures are traced through Mule's outbound call and downstream response. Separating failure classes prevents mixing unrelated problems.

## Scenario 84 — One downstream dependency is unavailable
**Question:** One dependency is down, but the main API should remain available for other functions. What do you consider?

**Answer:** I check whether the architecture supports graceful degradation, asynchronous processing, fallback behavior, or route-specific error handling. I avoid hiding a real dependency failure with false success responses unless the API contract explicitly supports that behavior.

## Scenario 85 — Production logs contain sensitive data
**Question:** You discover credentials or sensitive business data in logs. What do you do?

**Answer:** I avoid copying or exposing the sensitive values, immediately follow the security incident process, and notify the appropriate security/engineering team. I recommend masking/redaction and reviewing logging configuration. Sensitive information should not be used as casual troubleshooting evidence.

## Scenario 86 — Application restart causes temporary success
**Question:** After every restart, transactions work for a short period and then slow down. What pattern do you look for?

**Answer:** I correlate the degradation with memory, CPU, thread usage, connection pools, queue depth, traffic, and downstream latency. The repeated recovery-after-restart pattern strongly suggests a resource or state-related issue that needs permanent analysis.

## Scenario 87 — Release has no visible errors but business behavior changed
**Question:** A deployment is technically healthy, but business results changed unexpectedly. What do you compare?

**Answer:** I compare mapping logic, routing conditions, configuration, reference data, feature flags, API contracts, and downstream behavior between the previous and current release. Technical health does not guarantee business correctness.

## Scenario 88 — Business wants a quick workaround
**Question:** Business asks you to disable a validation rule to clear a backlog. What do you do?

**Answer:** I assess the risk first. If the validation protects data quality or downstream integrity, disabling it may create a larger incident. I explain the risk, propose a controlled alternative, and make any change only through the approved process.

## Scenario 89 — Incident is resolved but RCA is incomplete
**Question:** Can you close the incident before the root cause is fully known?

**Answer:** The service can be considered recovered when impact is removed and validation is complete, but the problem/RCA follow-up should remain tracked if the cause is unknown. Recovery and resolution are not always the same thing.

## Scenario 90 — Interviewer asks for your overall troubleshooting method
**Question:** How do you troubleshoot an unfamiliar MuleSoft production issue?

**Answer:** I start with impact and scope, then collect timestamp, correlation ID, API/flow, response code, payload pattern, and recent changes. I check monitoring and logs, isolate Mule versus infrastructure versus downstream, apply the safest approved mitigation, verify technical and business recovery, reconcile affected transactions, and document RCA and preventive actions.
