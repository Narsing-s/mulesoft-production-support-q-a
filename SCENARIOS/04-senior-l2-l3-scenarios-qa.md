# Senior L2/L3 MuleSoft Production Support Scenarios

## Scenario 91 — API works for GET but POST fails
**Question:** GET works normally, but POST requests return errors. How do you investigate?

**Answer:** I compare the HTTP method, request headers, content type, payload schema, validation rules, APIkit routing, and downstream behavior. I also verify whether POST requires additional authorization or business fields. I reproduce with a known-good payload before changing production configuration.

## Scenario 92 — Only one HTTP method returns 405
**Question:** An endpoint returns 405 Method Not Allowed. What do you check?

**Answer:** I verify the API contract, listener configuration, APIkit-generated flows, HTTP method, and gateway routing. A 405 usually means the resource exists but the requested method is not allowed, so I focus on routing and contract configuration.

## Scenario 93 — Client sends XML but API expects JSON
**Question:** A consumer suddenly receives a media-type error. What do you check?

**Answer:** I check the Content-Type and Accept headers, API contract, request transformation, and whether the client changed its payload format. I compare the failing request with a successful request and avoid modifying the API contract without impact assessment.

## Scenario 94 — Downstream returns 502
**Question:** Mule receives a 502 from a downstream gateway. What do you do?

**Answer:** I confirm whether the 502 originated from Mule or the downstream gateway. I trace the outbound call using correlation and timestamps, inspect endpoint/network evidence, and coordinate with the downstream team if Mule successfully sent the request but the gateway could not reach its backend.

## Scenario 95 — Downstream returns 504
**Question:** An API intermittently returns 504. What is your investigation?

**Answer:** I determine which layer generated the timeout and compare request duration with configured timeouts. I check downstream latency, network behavior, Mule threads, connection pools, and traffic patterns. I avoid simply increasing timeouts because that can keep resources occupied longer.

## Scenario 96 — Error occurs only with large arrays
**Question:** Small payloads work, but requests containing large arrays fail. What do you check?

**Answer:** I inspect payload size, DataWeave operations, memory usage, streaming behavior, iteration logic, timeout limits, and downstream constraints. I compare a successful small payload with the failing large payload and optimize the processing path where possible.

## Scenario 97 — Variable unexpectedly becomes null
**Question:** A production flow suddenly receives a null variable. What do you investigate?

**Answer:** I trace where the variable was created and modified and check scope, flow references, routing paths, error handling, and conditional execution. I verify whether the variable was actually initialized for every path before it was consumed.

## Scenario 98 — DataWeave works for one datatype but not another
**Question:** A transformation works when a field is a string but fails when the same field arrives as a number. What do you do?

**Answer:** I compare successful and failed payloads and inspect the actual runtime datatype. I add explicit type handling or normalization where appropriate and regression-test all supported input variations rather than fixing only the observed sample.

## Scenario 99 — API response schema changed unexpectedly
**Question:** A consumer says the API response changed after deployment. How do you troubleshoot?

**Answer:** I compare the previous and current response schemas, DataWeave mapping, RAML/API contract, default values, field names, and datatypes. I check whether the change was intentional and assess backward compatibility before proposing a fix.

## Scenario 100 — Database insert succeeds but response fails
**Question:** The DB insert succeeds, but Mule returns an error to the client. What is the risk?

**Answer:** The client may retry even though the business operation already committed, creating duplicates. I verify transaction state and downstream status before reprocessing. This is a classic case where idempotency and reconciliation are critical.

## Scenario 101 — Same request arrives twice seconds apart
**Question:** The same request is received twice within seconds. How do you identify the cause?

**Answer:** I compare correlation IDs, business transaction IDs, client retry behavior, gateway logs, Mule logs, and downstream acknowledgements. I determine whether Mule duplicated the request or the client sent it twice before changing application logic.

## Scenario 102 — Object Store data appears stale
**Question:** An application is returning old information from Object Store. What do you check?

**Answer:** I verify the key, TTL/expiration configuration, write/update path, environment, and whether the expected update actually occurred. I also check whether multiple workers or deployments are involved and whether the design expects shared or persistent state.

## Scenario 103 — Scheduler triggers duplicate processing
**Question:** A scheduler appears to process the same records twice. What do you investigate?

**Answer:** I check overlapping scheduler executions, multiple workers, locking/idempotency controls, retry behavior, and whether the previous execution completed before the next one started. I verify transaction identifiers to prove duplicate processing.

## Scenario 104 — Batch job runs but misses records
**Question:** A batch job completes successfully but business says some records were not processed. What do you check?

**Answer:** I reconcile the source count, records accepted by the batch, filtered records, failed records, and downstream results. A successful batch execution does not automatically mean every source record was successfully processed.

## Scenario 105 — Application deployment hangs
**Question:** A deployment remains in progress for an unusually long time. What do you do?

**Answer:** I check deployment status, runtime events, startup logs, resource availability, artifact/package issues, and platform health. I avoid starting multiple deployments simultaneously because that can complicate recovery.

## Scenario 106 — Worker repeatedly crashes
**Question:** One worker repeatedly crashes while others remain healthy. What do you investigate?

**Answer:** I inspect worker-specific logs and metrics, memory/CPU, payload patterns, traffic distribution, scheduled tasks, connector behavior, and recent changes. I determine whether the worker crash is caused by a specific workload or resource condition.

## Scenario 107 — Application health is green but business transactions fail
**Question:** Runtime Manager shows the application as running, but transactions are failing. What does that tell you?

**Answer:** Application health and business health are different. I check endpoint-level error rates, transaction success, downstream responses, and business KPIs. A running JVM/application does not prove the integration is functionally healthy.

## Scenario 108 — Downstream API changes its response format
**Question:** A downstream system changes its response JSON without notifying the Mule team. What do you do?

**Answer:** I capture the failing response, compare it with the expected contract, and identify the transformation impact. I coordinate with the downstream owner and determine whether Mule needs a backward-compatible mapping or the dependency needs to restore the contract.

## Scenario 109 — Network team says connectivity is fine
**Question:** The network team says connectivity is healthy, but Mule still cannot connect. How do you proceed?

**Answer:** I ask for evidence covering the exact endpoint, port, timestamp, source, and destination. I check DNS resolution, TLS handshake, authentication, firewall rules, proxy configuration, and application-level connection errors. “Network is healthy” is not enough without matching transaction evidence.

## Scenario 110 — P1 recovery requires a risky change
**Question:** A risky configuration change could restore a P1 faster. Would you do it?

**Answer:** I would assess business impact, rollback capability, change authorization, and risk. During a P1 I still follow emergency-change procedures. I prefer the safest reversible mitigation and ensure the incident commander and required stakeholders understand the risk before proceeding.

## Scenario 111 — Production issue started without deployment
**Question:** No deployment occurred, but failures suddenly started. What are possible causes?

**Answer:** I investigate external changes such as certificates, passwords, downstream releases, API policies, network changes, database health, traffic spikes, scheduled jobs, and expired credentials. “No Mule deployment” only rules out one category of change.

## Scenario 112 — Monitoring shows increased latency after database maintenance
**Question:** API latency increased immediately after DB maintenance. How do you prove the relationship?

**Answer:** I compare timestamps, DB execution times, connection behavior, locks, query plans, and application latency before and after maintenance. If the timing and database evidence align, I provide that evidence to the DBA team while continuing to monitor the API.

## Scenario 113 — Consumer claims they never received the response
**Question:** Mule shows a successful response, but the client says it timed out. What do you investigate?

**Answer:** I determine whether Mule completed the request before or after the client timeout. I inspect response timing, gateway/load-balancer logs, network evidence, and client behavior. I also verify whether the business transaction committed, because the client timeout does not prove the operation failed.

## Scenario 114 — Error rate drops after restart
**Question:** Error rate becomes normal immediately after restart. Can you say the restart fixed the root cause?

**Answer:** No. It proves the restart restored service temporarily, not why the failure occurred. I compare resource and dependency metrics before and after restart and continue RCA to identify the underlying condition.

## Scenario 115 — Multiple APIs fail simultaneously
**Question:** Five unrelated APIs fail at the same time. Where do you start?

**Answer:** I look for a shared dependency: platform/runtime, network, DNS, authentication service, certificate, gateway, database, MQ, or common downstream service. Simultaneous failures across unrelated flows often point to a shared infrastructure or dependency layer.

## Scenario 116 — Only one downstream endpoint fails
**Question:** Multiple APIs use the same application, but only one downstream endpoint fails. What does that suggest?

**Answer:** I narrow the investigation to that endpoint's URL, authentication, certificate, routing, policy, payload contract, and downstream availability. The application-wide runtime is less likely to be the primary issue if other endpoints remain healthy.

## Scenario 117 — Incident resolved but backlog remains
**Question:** The application is healthy again, but thousands of messages remain queued. What next?

**Answer:** I monitor drain rate and downstream capacity, then use controlled recovery processing. I verify successful consumption, failures, duplicates, and ordering requirements. Recovery is complete only after the backlog and affected business transactions are reconciled.

## Scenario 118 — A fix resolves one customer but breaks another
**Question:** A production fix solves one customer's issue but creates failures for another. What does that indicate?

**Answer:** The fix may have addressed a customer-specific symptom rather than the underlying generalized behavior. I compare both customer paths, revert or contain the risky change if necessary, and design a solution that preserves existing valid behavior.

## Scenario 119 — Business asks for root cause immediately
**Question:** Stakeholders demand an RCA while the incident is still active. What do you communicate?

**Answer:** I clearly separate confirmed facts, current hypothesis, and unknowns. During recovery I focus on service restoration and provide a preliminary cause only when supported by evidence. The final RCA follows after logs, timelines, and dependency evidence are reviewed.

## Scenario 120 — Interviewer asks what makes a strong L2/L3 engineer
**Question:** What is the difference between a basic support engineer and a strong L2/L3 MuleSoft support engineer?

**Answer:** A strong engineer does more than restart applications and forward tickets. They correlate transactions across systems, isolate the failing layer using evidence, understand Mule flows and connectors, protect against duplicate processing, communicate clearly during P1/P2 incidents, validate recovery, and drive RCA and preventive improvements.
