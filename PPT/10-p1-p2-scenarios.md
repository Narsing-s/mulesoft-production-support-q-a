# 10 — P1/P2 Incident Scenarios

## Scenario 1 — 400 Files Stuck
Quantify impact → check consumer/agent → inspect queue and logs → verify downstream → controlled restart only if justified → verify backlog drains → reconcile.

## Scenario 2 — Intermittent 500
Compare successful/failed transactions using correlation IDs, timestamps, payload characteristics, downstream responses and load.

## Scenario 3 — Queue Backlog
Determine whether producer rate exceeds consumer throughput or the consumer is failing.

## Scenario 4 — Duplicate Processing
Investigate source retry, acknowledgement, restart behavior and idempotency before reprocessing.

## Scenario 5 — Certificate Expiry
Identify dependencies → approved renewal → trust-chain validation → controlled deployment → end-to-end validation.

## Scenario 6 — No Logs
Prove whether the request reached Mule, then use upstream/downstream evidence and verify environment/time/log configuration.
