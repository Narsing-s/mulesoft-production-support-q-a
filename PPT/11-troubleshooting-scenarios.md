# 11 — Troubleshooting Scenarios

## Scenario 1 — DB Timeout
Start with the timestamp and correlation/request ID.

Check:
- DB reachability
- connection acquisition time
- query duration
- pool utilization
- locks/blocking
- DB resource health
- network/TLS
- recent application or DB changes

Mitigate only after identifying the safe operational action.

## Scenario 2 — SFTP Failure
Determine whether failure occurs during:
1. connection
2. authentication
3. directory access
4. file discovery
5. file transfer
6. downstream processing

This avoids treating every SFTP error as a credential problem.

## Scenario 3 — Scheduler Did Not Run
Verify:
- application was running at the expected time
- scheduler configuration
- timezone
- deployment/environment
- whether schedule was disabled
- previous execution state
- startup/deployment logs

Then determine whether the missed run requires controlled backfill.

## Scenario 4 — HTTP 200 but Wrong Data
Treat this as a functional/data incident, not a healthy transaction.

Trace:
**source data → retrieval → DataWeave transformation → business rules → response.**

Compare a correct and incorrect transaction and quantify the affected population.

## Scenario 5 — Restart Temporarily Fixes Issue
A restart is mitigation, not root cause.

If it recurs, investigate:
- memory/CPU pressure
- connection pools
- stuck threads
- resource leaks
- downstream connections
- queue/file backlog
- traffic patterns
- deployment/configuration changes

## Scenario 6 — Cannot Reproduce
Production evidence becomes critical:
- correlation ID
- exact timestamp/timezone
- request/response metadata
- error type
- application version
- sanitized payload
- dependency behavior

Compare failed and successful transactions instead of repeatedly retrying blindly.

## Scenario 7 — Mule or SAP?
Prove the boundary.

Ask:
- Did Mule receive the request?
- Did Mule transform it?
- Did Mule send it to SAP?
- Did SAP acknowledge/reject it?
- Is there a common transaction/correlation ID?
- Do timestamps line up?

The goal is evidence-based ownership, not guessing.

## Scenario 8 — 500 Only for Some Payloads
Compare successful and failed payloads for:
- missing fields
- datatype differences
- size
- special characters
- business-rule values
- downstream validation

If a specific data pattern causes failure, classify it as a functional/data issue even if the final status is 500.

## Scenario 9 — Queue Backlog Growing
Measure producer rate versus consumer rate.

Then inspect:
- consumer health
- processing latency
- downstream response time
- poison messages
- connection failures
- recent releases

A restart may restore consumption, but RCA must explain why throughput degraded.

## Scenario 10 — File Reprocessed Twice
Determine whether the first attempt partially completed.

Check:
- target-side records
- business transaction ID
- processed-file/message state
- timestamps
- downstream acknowledgements

Only reprocess after duplicate impact is understood.

## Scenario 11 — Certificate Failure
Check:
- certificate expiry
- correct alias
- truststore/keystore
- certificate chain
- hostname validation
- environment-specific configuration

After renewal, perform a controlled connectivity test and monitor dependent flows.

## Scenario 12 — Production Password Changed
Validate the new secret through the approved secure configuration mechanism.

Do not put credentials into source code, chat, screenshots or logs. Restart/redeploy only if the runtime requires configuration reload.

## Scenario 13 — No Mule Logs
Do not conclude that Mule is not involved.

Check:
- request reached the listener
- gateway/access logs
- application status
- correct application/environment
- logging level
- correlation ID
- downstream-side evidence

## Slide — Troubleshooting Formula
**Impact → Timestamp/ID → First failing boundary → Evidence → Recent change → Safe mitigation → Verification → Reconciliation → RCA.**
