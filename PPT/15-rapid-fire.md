# 15 — Rapid Fire

## Slide 1 — Mule Concepts
**Choice:** evaluates conditions in order; first matching route executes.

**Scatter-Gather:** executes routes in parallel and aggregates their results.

**For Each:** processes collection items sequentially.

**Parallel For Each:** processes collection items concurrently, so concurrency and downstream capacity matter.

## Slide 2 — Error Handling
**On Error Continue:** handles the error and allows the scope/flow to continue with the handled outcome.

**On Error Propagate:** handles the error but propagates failure to the caller/upstream scope.

**Important:** the correct choice depends on business semantics. Do not hide production failures merely to return success.

## Slide 3 — HTTP
401 = authentication failure.

403 = authenticated but not authorized.

404 = requested resource/path not found.

409 = conflict/business state conflict.

429 = throttling/rate limit.

500 = server-side application failure.

502/503/504 = commonly indicate gateway/upstream/service availability or timeout problems; confirm the actual architecture.

## Slide 4 — Integration
**Correlation ID:** technical transaction identifier used to trace a request across logs/components.

**Business transaction ID:** business identifier such as an order or invoice number.

**Idempotency:** repeated processing does not create unintended duplicate business effects.

**Reconciliation:** prove what was received, processed, failed and ultimately delivered.

## Slide 5 — Production Rules
Never hardcode secrets.

Never restart blindly.

Never reprocess blindly.

Never assume the first visible error is the root cause.

Always verify recovery.

Always reconcile affected transactions.

Always preserve evidence before changing state when practical.

## Slide 6 — Scenario Flash Answers
**API is down:** confirm scope → app status → listener/gateway → logs → dependency → safe mitigation.

**Queue backlog:** compare producer vs consumer rate → consumer health → errors/poison messages → downstream.

**SFTP failed:** isolate connection/auth/path/file/permission/transfer stage.

**DB timeout:** isolate network/pool/query/lock/database capacity.

**Certificate error:** expiry → chain → alias → truststore/keystore → hostname → environment.

## Slide 7 — Golden Sentence
“First I confirm impact and scope. Then I collect the correlation ID and timestamp, inspect logs and metrics, isolate the failing boundary, validate configuration and dependencies, apply the safest approved mitigation, verify recovery, reconcile affected transactions and document RCA/prevention.”
