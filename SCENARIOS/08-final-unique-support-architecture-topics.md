# Q251–Q280 — Final Unique MuleSoft Support Topics

## Q251 — What is the difference between SLA, SLO and SLI?
**Answer:** An **SLI** is the measured indicator, such as availability or latency. An **SLO** is the target for that indicator, such as 99.9% availability. An **SLA** is the externally agreed commitment, often with business consequences. In support, I use the SLI to measure the incident and the SLO/SLA to determine impact and urgency.

## Q252 — What are RTO and RPO?
**Answer:** **RTO** is the maximum acceptable time to restore service. **RPO** is the maximum acceptable amount of data loss measured in time. During a major outage, these help determine whether restoration, failover or recovery from a backup meets the business requirement.

## Q253 — What is the difference between high availability and disaster recovery?
**Answer:** High availability reduces service interruption through redundant runtime components and automatic or controlled recovery. Disaster recovery addresses restoration of service after a larger failure such as regional or infrastructure loss. HA is primarily about continuity; DR is about recovery from major disruption.

## Q254 — What is a DR failover test?
**Answer:** It is a controlled exercise that proves the documented recovery path actually works. I verify application availability, configuration, connectivity, secrets, certificates, persistent state, data integrity, DNS/routing and the ability to return to the primary environment.

## Q255 — What is a five-layer approach to network troubleshooting?
**Answer:** I isolate the path progressively: **DNS → TCP/connectivity → TLS → HTTP → application/business behavior**. This prevents jumping directly to Mule code when the failure is actually name resolution, network reachability or certificate validation.

## Q256 — What is the difference between a TCP timeout and an HTTP timeout?
**Answer:** A TCP/connect timeout means the connection could not be established within the configured time. An HTTP/read timeout generally means a connection exists but the expected response did not arrive in time. The distinction helps identify whether the issue is connectivity or downstream processing latency.

## Q257 — What is hostname verification in TLS?
**Answer:** Certificate trust answers whether the certificate chain is trusted. Hostname verification checks whether the certificate identity matches the hostname being contacted. A trusted certificate can still fail hostname verification.

## Q258 — What is OAuth token refresh?
**Answer:** Token refresh obtains a new access token using the supported refresh mechanism instead of repeatedly requesting a full user authorization. For production incidents, I distinguish expired access tokens, invalid refresh tokens, wrong scopes/audience and clock-skew problems before changing credentials.

## Q259 — What is the difference between authentication, authorization and scope?
**Answer:** Authentication establishes who the caller is. Authorization determines what that caller is allowed to do. A scope is a permission boundary carried by an authorization mechanism such as OAuth. A successfully authenticated client can still be denied because its scope or authorization is insufficient.

## Q260 — What is a database deadlock?
**Answer:** A deadlock occurs when concurrent transactions hold locks that each needs the other transaction to release. I check database deadlock diagnostics, transaction order, affected queries and timing. The fix should address transaction design or lock contention rather than simply increasing timeouts.

## Q261 — What is the difference between optimistic and pessimistic locking?
**Answer:** Optimistic locking assumes conflicts are uncommon and detects a conflicting update, often through a version value. Pessimistic locking acquires a lock before modifying data. Optimistic approaches can improve concurrency, while pessimistic approaches can provide stronger immediate exclusion but increase contention.

## Q262 — What is a pagination consistency problem?
**Answer:** If records are inserted, removed or updated while an offset-based extraction is running, page boundaries can shift and cause duplicates or gaps. I prefer a stable ordering plus a suitable cursor/watermark strategy when the source supports it.

## Q263 — What is an atomic file move pattern?
**Answer:** A producer writes to a temporary filename and moves/renames the completed file into the pickup directory only after writing finishes. The consumer watches for the final extension. This prevents Mule from reading a partially written file.

## Q264 — What is a file checksum validation?
**Answer:** A checksum can verify that the received file content matches the expected content. It is useful when transport succeeds but corruption or incomplete transfer is suspected. I compare the checksum according to the agreed source/target process before reprocessing.

## Q265 — What is the difference between binary data and Base64?
**Answer:** Binary data is the actual byte content. Base64 is a textual representation of those bytes and increases size. Converting large binary payloads unnecessarily can increase memory and bandwidth consumption.

## Q266 — What is CORS?
**Answer:** Cross-Origin Resource Sharing is a browser security mechanism controlling whether a web page can call a resource hosted on another origin. A backend may be healthy while a browser client fails because the required CORS response headers or preflight handling are missing.

## Q267 — What is a preflight OPTIONS request?
**Answer:** A browser may send an OPTIONS request before the actual cross-origin request to verify permitted methods, headers and origin. If OPTIONS is rejected, the business request may never reach the Mule API.

## Q268 — What is the difference between POST, PUT and PATCH?
**Answer:** POST commonly creates or triggers an operation and is generally not inherently idempotent. PUT commonly replaces a resource representation at a known identifier and is designed to be idempotent. PATCH partially modifies a resource. The exact business contract still determines the correct behavior.

## Q269 — What is graceful shutdown during deployment?
**Answer:** Graceful shutdown allows an application to stop accepting new work while giving in-flight processing an opportunity to finish or reach a safe recovery point. It reduces lost or duplicated work during restarts and rolling deployments.

## Q270 — What should you verify for in-flight transactions during a deployment?
**Answer:** I verify whether work is transactional, queued, acknowledged, persisted or recoverable. I identify what happens to in-flight messages when a worker drains or terminates and confirm the recovery mechanism before approving the deployment.

## Q271 — What is a canary deployment?
**Answer:** A canary deployment sends a small portion of production traffic to the new version before broader rollout. Support validates error rate, latency, resource usage and business outcomes against the existing version before expansion.

## Q272 — What is the difference between canary and blue-green deployment?
**Answer:** Canary gradually exposes a new version to a subset of traffic. Blue-green maintains two environments and switches traffic between them. Canary reduces exposure gradually; blue-green provides a cleaner environment-level switch and rollback path.

## Q273 — What is deployment change failure rate?
**Answer:** It measures the proportion of deployments that result in a production failure requiring remediation, rollback or other recovery. It helps teams assess release quality rather than looking only at whether CI/CD completed successfully.

## Q274 — What is a DORA-style lead-time metric?
**Answer:** Deployment lead time measures how long it takes a change to move from its starting point in the delivery process to production. It helps evaluate delivery flow and bottlenecks when combined with deployment frequency and change-failure measures.

## Q275 — What is the difference between an incident commander and a technical lead?
**Answer:** The incident commander coordinates the overall response, priorities and decisions. The technical lead directs technical investigation and mitigation. Separating these responsibilities helps prevent technical troubleshooting from being neglected while stakeholder communication is happening.

## Q276 — What should a good shift handover contain?
**Answer:** It should include active incidents, impact, current state, evidence, actions already taken, pending actions, risks, owners, escalation status and exact next checkpoint. A handover should let the next engineer continue without repeating investigation.

## Q277 — What is a blameless post-incident review?
**Answer:** It focuses on system conditions, decisions, controls and process gaps rather than assigning personal blame. The objective is to identify actionable improvements that reduce recurrence and improve detection and recovery.

## Q278 — How do you distinguish a symptom, trigger and root cause?
**Answer:** A **symptom** is what users observe, such as 500 errors. A **trigger** is the event that immediately initiated the failure, such as a certificate expiry. The **root cause** explains why the condition occurred or why controls failed to prevent/detect it, such as missing certificate-expiry monitoring and ownership.

## Q279 — What is the first meaningful error principle?
**Answer:** In a cascading failure, many later errors may be consequences. I establish the timeline and locate the earliest meaningful failure that changed system behavior, then verify it with evidence. This is usually more useful than investigating the largest volume of downstream error messages.

## Q280 — How do you isolate a failure across a multi-system integration?
**Answer:** I divide the transaction into boundaries: client/gateway, Mule listener, transformation, outbound connector, network/security, downstream service, acknowledgement and business persistence. I compare correlation IDs, timestamps, status codes and payload/business identifiers at each boundary to determine exactly where the transaction stopped or changed behavior.

## Final interview rule
For advanced support questions, answer with **definition → distinction → evidence → production example → safe action → verification**.