# MuleSoft L2/L3 Production Support — Scenario Practice

## Scenario 1 — API is down

**Question:** A critical Mule API is down in production. What will you do?

**Answer structure:**
1. Check business impact and severity.
2. Check Runtime Manager application status.
3. Check Anypoint Monitoring and enterprise monitoring.
4. Review startup/runtime logs.
5. Check recent deployment/configuration changes.
6. Determine Mule vs downstream issue.
7. Perform approved restart/rollback/recovery if appropriate.
8. Run health checks and smoke tests.
9. Monitor after recovery.
10. Document RCA and preventive action.

## Scenario 2 — Application is running but transactions fail

**Question:** Runtime Manager shows the application as running, but users report failures.

**Answer:**

Running status does not guarantee transaction health. I check transaction-level errors, correlation IDs, application logs, downstream responses, authentication, transformations and connectivity. I determine whether the failure affects all transactions or specific payloads. I then recover or escalate based on the actual failure point.

## Scenario 3 — 1,000 orders are stuck

**Question:** Business says 1,000 orders are stuck.

**Answer:**

I identify the affected integration and business impact. I check queue depth, Mule application health, monitoring and logs. I determine whether the consumer is down, messages are repeatedly failing, or a downstream application is unavailable. I restore processing or coordinate with the owning team, then monitor the backlog until it reduces and validate business processing.

## Scenario 4 — HTTP 500 from downstream

**Question:** Mule receives HTTP 500 from a downstream system.

**Answer:**

I first establish whether Mule generated the 500 or the downstream service returned it. I use correlation ID, timestamp and logs to trace the transaction. If downstream generated it, I check the dependency status and coordinate with that team. If Mule generated it, I investigate the flow and error handling. I follow the approved retry/reprocessing procedure only where appropriate.

## Scenario 5 — Authentication failure

**Question:** An API suddenly starts returning 401.

**Answer:**

I check credentials/token validity, expiration, authentication configuration and recent security changes. I check whether the issue is environment-specific and whether all transactions are affected. If a credential or secret rotation is required, I follow the approved change process and validate the integration afterward.

## Scenario 6 — Application restart

**Question:** Would you restart immediately when users report errors?

**Answer:**

No. I first establish whether Mule is actually unhealthy. If Mule is healthy and the downstream system is unavailable, restarting Mule may not solve anything. I restart only when there is an approved operational reason and after considering active transactions/messages.

## Scenario 7 — Deployment succeeded but business flow fails

**Question:** The deployment is green, but business transactions fail immediately afterward.

**Answer:**

I treat deployment success and functional success separately. I check startup logs, properties, secrets, certificates, endpoints, connectivity and downstream dependencies. I compare with the previous version and coordinate rollback or hotfix if required. After recovery I perform smoke testing and monitor the affected flow.

## Scenario 8 — Recurring incident

**Question:** The same API fails every few days. What do you do?

**Answer:**

I do not treat each event as an isolated incident. I analyze incident history, logs, timestamps, downstream behavior and changes to identify a common pattern. I document the root cause and work with development/infrastructure teams on permanent corrective action. I also recommend monitoring or alerting improvements.

## Scenario 9 — Development says it is not MuleSoft

**Question:** Development says the issue is not on their side. What do you do?

**Answer:**

I keep the discussion evidence-based. I provide the correlation ID, timestamps, request/response information, Mule logs and the exact processor where the failure occurs. We determine which layer failed from the evidence and involve the correct owner rather than debating ownership.

## Scenario 10 — Multiple simultaneous incidents

**Question:** Three incidents arrive at the same time. How do you prioritize?

**Answer:**

I prioritize using business impact, severity, affected transaction/user volume and SLA. A critical production outage takes precedence over a low-impact isolated failure. I also consider whether there is a workaround and whether the incident is actively growing.

## Scenario 11 — Slow API

**Question:** API is available but response time has increased significantly.

**Answer:**

I compare current response time with normal baselines in monitoring. I check Mule CPU/memory/runtime behavior, logs, downstream response times, database or external-service latency and recent changes. I determine where the latency is introduced and coordinate with the responsible team. I monitor after remediation.

## Scenario 12 — Post-recovery validation

**Question:** Application is back up. Is the incident resolved?

**Answer:**

Not immediately. I verify application health, execute agreed smoke tests, validate representative business transactions, check error rates and monitor for a period after recovery. Only after confirming business functionality do I consider the service fully recovered.
