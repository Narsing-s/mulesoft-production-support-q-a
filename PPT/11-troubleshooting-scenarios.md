# 11 — Troubleshooting Scenarios

## Scenario 1 — DB Timeout
Check DB health, query duration, connection pool, locks, network and recent changes.

## Scenario 2 — SFTP Failure
Validate endpoint, credentials, path, permissions, polling and filters.

## Scenario 3 — Scheduler Did Not Run
Check app status, schedule, timezone, deployment, disabled settings and logs.

## Scenario 4 — HTTP 200 but Wrong Data
Treat as functional/data incident. Validate source → transformation → response and affected population.

## Scenario 5 — Restart Temporarily Fixes Issue
Restart is mitigation, not RCA. Investigate recurrence pattern, resources, connection pools and downstream behavior.

## Scenario 6 — Cannot Reproduce
Use production correlation evidence, sanitized payload, matching configuration assumptions and dependency behavior.

## Scenario 7 — Mule or SAP?
Prove boundaries: Mule received? Mule sent? What did SAP return? Correlate timestamps and IDs.
