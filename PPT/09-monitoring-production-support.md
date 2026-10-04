# Slide 09 — Monitoring & Production Support

## Q69. What do you monitor in MuleSoft production?
**Answer:** I monitor application availability, error rate, response time, throughput, worker/resource health, queue or file backlog, dependency failures and business-level indicators where available.

A running application is not necessarily healthy. It can still have failed transactions, blocked consumers, authentication failures or downstream outages.

## Q70. How do you use a correlation ID?
**Answer:** I use the correlation ID as the transaction tracing key. I search logs and monitoring tools with the ID and timestamp, identify the flow, connector call, error and downstream response.

This narrows investigation from thousands of log entries to one transaction path.

## Q71. Walk me through a P1 incident.
**Answer:** First I confirm impact and scope: affected APIs, users, transactions and business process. I establish or join the incident bridge and communicate facts without speculation.

In parallel, I investigate logs/metrics and dependency health while identifying a safe mitigation. After recovery, I validate new transactions and reconcile the affected population. I preserve evidence for RCA.

## Q72. Walk me through a P2 incident.
**Answer:** I confirm business impact and SLA, collect correlation IDs/timestamps, isolate the failing component and work toward recovery. I keep stakeholders updated with evidence-based progress and avoid risky changes.

After service restoration, I verify transaction completion and identify whether reprocessing is required.

## Q73. When should you restart a Mule application?
**Answer:** A restart can be an approved mitigation for a known stuck state, memory issue, connector state or application condition. I do not restart blindly because it can remove evidence and interrupt in-flight processing.

Where time allows, I capture logs/metrics, identify the reason, confirm the runbook/approval and define post-restart validation.

## Q74. Recovery vs resolution?
**Answer:** Recovery restores service. Resolution removes or addresses the underlying cause.

For example, restarting a stuck consumer may restore processing. If the consumer repeatedly enters the same state, the incident is not truly resolved until the recurrence cause is addressed.

## Q75. What metrics help identify an API performance problem?
**Answer:** I compare request rate, response time, error rate, payload size, CPU/memory, downstream latency and connection-pool behavior. Comparing a healthy period against the incident period helps isolate whether the bottleneck is Mule, traffic, transformation or a dependency.

## Q76. What is proactive monitoring?
**Answer:** Proactive monitoring detects abnormal behavior before users report it. Examples include certificate-expiry alerts, queue-backlog thresholds, consumer-down alerts, error-rate thresholds, latency alerts and business reconciliation checks.
