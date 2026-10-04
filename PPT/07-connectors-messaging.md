# 07 — Connectors & Messaging

## Slide 1 — Database Connector
For a DB failure, isolate whether the problem is:
- database availability
- network/DNS
- credentials
- TLS
- connection pool
- query performance
- locks/blocking
- transaction behavior

Compare a failed timestamp with database-side evidence when available.

## Slide 2 — Connection Pool Exhaustion
Typical symptoms:
- requests waiting for a connection
- increased latency
- timeout errors
- failures increase during traffic spikes

Check pool configuration, active/idle connections, long-running queries and whether connections are being held longer than expected.

**Do not simply increase the pool** without checking DB capacity.

## Slide 3 — SFTP Troubleshooting
Check in order:
1. host and port
2. network reachability
3. username/key/password
4. host-key or TLS requirements where applicable
5. remote directory
6. permissions
7. filename/filter pattern
8. polling schedule
9. duplicate/partial-file handling

A successful connection does not prove the expected file exists in the expected directory.

## Slide 4 — MQ Troubleshooting
For queue backlog determine:
- producer rate
- consumer health
- connection state
- consumer throughput
- application errors
- poison messages
- downstream dependency health

Calculate whether the consumer can drain backlog faster than new messages arrive.

## Slide 5 — Poison Message
A poison message repeatedly fails processing and can block or repeatedly consume retry capacity.

Investigate the message content, error type and retry behavior. Use approved dead-letter/quarantine handling where designed.

**Never discard a business message without understanding reconciliation requirements.**

## Slide 6 — Idempotency
An operation is idempotent when repeating it does not create an unintended additional business effect.

Examples:
- use a business transaction ID
- store processed message IDs
- use database unique constraints
- make downstream update operations repeat-safe

Idempotency is essential when retries or manual reprocessing are possible.

## Slide 7 — Safe Reprocessing
Before reprocessing:
1. identify affected records/messages/files
2. determine whether partial processing already occurred
3. check idempotency/duplicate controls
4. preserve original evidence
5. reprocess only the approved scope
6. monitor the result
7. reconcile source vs target counts

## Slide 8 — Questions 57–62
57. How do you troubleshoot a DB timeout?
58. What causes connection-pool exhaustion?
59. How do you troubleshoot an SFTP file failure?
60. How do you investigate MQ backlog?
61. How do you handle duplicate messages?
62. How do you safely reprocess failed transactions?

## Slide 9 — Interview Takeaway
Do not say “restart the connector” as the first answer.

Say:

**Identify the boundary → collect evidence → isolate connector/dependency issue → apply the safest approved mitigation → verify → reconcile.**
