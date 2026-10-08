# Advanced Customer Interview Scenarios — L2/L3

This file intentionally covers topics not duplicated from the existing interview Q&A and scenario files.

## 1. One application has high CPU

**Answer:** I confirm the CPU trend and affected workers, identify when it started, correlate it with traffic/deployments, inspect logs and transaction volume, and determine whether a flow, transformation, connector or downstream wait is contributing. I take only approved mitigation actions and coordinate with development for profiling/permanent remediation.

## 2. Memory usage keeps increasing

**Answer:** I check heap/memory trends, worker behavior, traffic and recent changes. I look for large payloads, unbounded collections, repeated processing or resource-handling issues. I avoid repeatedly restarting without investigation because that only treats the symptom. I document evidence and involve development/platform teams for a permanent fix.

## 3. Queue depth is continuously increasing

**Answer:** I compare producer and consumer rates, verify the Mule consumer is healthy, check consumer logs and downstream latency, and determine whether messages are being rejected or retried. I monitor backlog recovery after remediation and validate that messages are not being lost or duplicated.

## 4. Duplicate transactions are reported

**Answer:** I identify whether duplication occurs at the source, queue, retry mechanism or downstream call. I use correlation/transaction identifiers and timestamps to trace both messages. I check whether the operation is idempotent and whether retries or redelivery caused the duplicate. I then coordinate a safe correction and preventive fix.

## 5. Messages are stuck in a DLQ

**Answer:** I first identify the failure reason and classify the messages. I check whether the problem is transient, data-related or a poison message. I fix the underlying issue before reprocessing and use the approved controlled reprocessing procedure. I monitor successful consumption and verify duplicates are not created.

## 6. Certificate is expiring

**Answer:** I confirm the affected integration and certificate expiry, identify all environments and endpoints using it, and coordinate renewal through the approved security/change process. After the update I validate TLS connectivity and execute a controlled transaction. I also recommend advance expiry monitoring.

## 7. API latency suddenly doubles after a deployment

**Answer:** I compare before/after monitoring metrics, check deployment changes, logs and downstream latency, and isolate where the extra time is introduced. If the change is the likely cause and rollback is approved, I support rollback. Otherwise I coordinate a hotfix and validate performance afterward.

## 8. Only one business customer is failing

**Answer:** I compare the failing payload and transaction with a successful transaction. I check customer-specific data, routing, authorization, transformation rules and downstream business validation. This helps distinguish a data/business-rule problem from an application-wide outage.

## 9. Intermittent failures cannot be reproduced

**Answer:** I collect exact timestamps, correlation IDs, affected payload characteristics and downstream responses from each occurrence. I compare successful and failed transactions and correlate them with infrastructure, network and dependency metrics. For intermittent issues, evidence and pattern correlation are especially important.

## 10. A deployment introduced an issue but rollback is not possible

**Answer:** I stabilize the service using the approved workaround, isolate the changed behavior, coordinate a hotfix with development and test the fix in the appropriate environment. I keep stakeholders informed and perform targeted production validation after the fix.

## 11. Downstream dependency is completely unavailable

**Answer:** I confirm the dependency outage using logs and monitoring rather than repeatedly retrying blindly. I check whether a fallback or queueing mechanism exists, prevent unnecessary load on the dependency, communicate the impact, and coordinate with the dependency owner. Once restored, I monitor backlog and controlled recovery.

## 12. How do you prevent a recovery from causing a second incident?

**Answer:** I check transaction state, backlog, duplicate risk, downstream capacity and change/runbook requirements before recovery. After the action I validate representative transactions and monitor the system rather than assuming recovery is complete.

## 13. What makes L3 support different from L2?

**Answer:** L2 focuses heavily on operational investigation, recovery and incident resolution using established procedures. L3 goes deeper into application behavior, code-level analysis, complex RCA, performance problems and permanent fixes, usually working closely with developers and platform teams. The boundary depends on the organization's support model.

## 14. What metrics would you monitor for an API?

**Answer:** Availability, request volume, error rate, response time/latency, throughput, resource utilization and downstream dependency behavior. For asynchronous integrations I also monitor queue depth, processing rate, failures, retries and backlog age.

## 15. What is the difference between symptom, immediate cause and root cause?

**Answer:** The symptom is what users observe, such as failed transactions. The immediate cause is the direct failure, such as a downstream timeout. The root cause explains why that condition occurred, such as an infrastructure or configuration problem. RCA should address the root cause, not stop at the symptom.

## 16. How do you handle a change that needs emergency production action?

**Answer:** I follow the organization's emergency-change process, document the business impact and reason, involve the required approvers/owners, perform the smallest safe change, validate it and document the outcome. Emergency does not mean uncontrolled.

## 17. How do you distinguish a Mule issue from an infrastructure issue?

**Answer:** I correlate application logs, runtime health, resource metrics, network/connectivity evidence and downstream behavior. If Mule processing is healthy but the runtime or network layer shows failures, I involve the platform/infrastructure team. I use evidence rather than assumptions.

## 18. How do you handle a failed reprocessing attempt?

**Answer:** I stop repeated blind retries, capture the new failure evidence and compare it with the original error. I determine whether the underlying issue is still present or whether the message itself is invalid. If it is a poison message, I isolate it according to the runbook and escalate for data correction or business decision.

## 19. How do you hand over an incident between shifts?

**Answer:** I provide a concise timeline, severity/SLA, business impact, current status, evidence, actions already performed, pending actions, owners, next checkpoint and any risks. The incoming engineer should be able to continue without repeating the investigation.

## 20. What questions would you ask the customer during an incident?

**Answer:** I would ask when the issue started, which business process is affected, whether all users or transactions are impacted, whether there are known recent business/application changes, examples of failed transactions, business priority and whether a workaround exists. I avoid requesting unnecessary information and focus on evidence needed for diagnosis.
