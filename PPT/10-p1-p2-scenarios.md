# Slide 10 — P1/P2 Production Scenarios

## Scenario 1 — Around 400 files are stuck
**Question:** Files were published but are not being consumed. What do you do?

**Answer:** I first quantify impact: number of files, oldest file age, business priority and whether all or only some files are affected. Then I check the producer/API, queue depth, consumer/agent state, Mule logs and downstream dependency.

If the consumer is confirmed stuck and the runbook permits a restart, I capture evidence and perform the controlled restart. Then I monitor the backlog draining and validate a sample end-to-end.

Finally, I reconcile every affected file. I do not blindly replay all files because some may already have reached the downstream system.

## Scenario 2 — Intermittent HTTP 500
**Answer:** I compare successful and failed requests using correlation IDs and timestamps. I check whether failures correlate with a particular payload, customer, downstream dependency, traffic level, worker or recent deployment.

I determine whether the 500 originated in Mule or is a transformed downstream error. If the dependency is failing, I engage that team with evidence.

## Scenario 3 — Queue backlog keeps increasing
**Answer:** I compare producer rate with consumer throughput. Then I determine whether consumers are stopped, slow, repeatedly failing, blocked on a dependency or encountering poison messages.

I check queue depth over time, consumer health, error rates, processing latency and downstream response time. Recovery must also consider duplicate and ordering risks.

## Scenario 4 — Duplicate transactions after reprocessing
**Answer:** I stop uncontrolled replay and identify the business key/message ID. I determine whether the first attempt actually reached the downstream system and whether an acknowledgement was lost.

Then I use idempotency controls or reconciliation to distinguish genuinely unprocessed records from already-completed records.

## Scenario 5 — Certificate expired
**Answer:** I identify affected integrations, certificate alias, truststore/keystore, endpoint and expiry time. After approved renewal, I validate the trust chain and hostname/configuration.

I perform a controlled deployment or restart if required and run end-to-end tests. I also recommend proactive certificate-expiry monitoring.

## Scenario 6 — No Mule logs for a reported failure
**Answer:** I first prove whether the request reached Mule. I check gateway/access logs, client evidence, network/load-balancer evidence and timestamps.

If it reached Mule, I verify log configuration, worker health and whether the failure occurred before application logging. I never conclude that Mule is healthy simply because application logs are empty.

## Scenario 7 — Production password was changed
**Answer:** I confirm the exact affected integration and environment, verify the approved new credential, update the secure configuration according to the deployment process, and restart/redeploy only if required.

Then I test authentication and a real business transaction. I document the change and confirm that no credential was exposed in logs or source control.

## Scenario 8 — SFTP intermittently fails
**Answer:** I compare successful and failed timestamps and check host availability, port connectivity, authentication, remote directory permissions, file naming/filter rules and network stability.

If only specific files fail, I inspect filename/size/content characteristics. If the server itself is unstable, I provide evidence to the SFTP team rather than repeatedly retrying without control.
