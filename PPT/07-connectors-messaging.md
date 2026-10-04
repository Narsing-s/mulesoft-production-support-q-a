# 07 — Connectors & Messaging

## Slide 1 — Database
Check availability, credentials, network/DNS, TLS, connection pool, timeout, locks and query performance.

## Slide 2 — SFTP
Check host/port, credentials/key, directory, permissions, polling, filename/filter, network and duplicate handling.

## Slide 3 — MQ
For backlog check consumer health, connection status, consumer errors, producer rate, consumer throughput, poison messages and downstream availability.

## Slide 4 — Idempotency
Repeated execution should not create unintended duplicate business effects. Use business keys/message IDs/processed state where appropriate.

## Questions
57. DB timeout?
58. Connection pool exhaustion?
59. SFTP file stuck?
60. MQ backlog?
61. Duplicate message?
62. Safe reprocessing?
