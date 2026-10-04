# Slide 17 — 100+ Detailed Interview Question Bank

> Use these as speaking answers. Do not memorize every word. Understand the sequence, then explain in your own words.

## Q91. What is API-led connectivity?
**Answer:** API-led connectivity organizes integrations into reusable System APIs, Process APIs and Experience APIs. System APIs expose core systems such as SAP or databases, Process APIs apply business logic across systems, and Experience APIs shape data for a particular consumer.

**Production angle:** This separation helps support teams identify the failing layer and reduces duplicated point-to-point logic.

## Q92. What is a System API?
**Answer:** A System API provides controlled access to a system of record. It hides system-specific connectivity details from consumers. For example, an SAP System API can expose customer information without every consumer implementing SAP-specific connectivity.

## Q93. What is a Process API?
**Answer:** A Process API combines or orchestrates data from one or more System APIs and applies business rules. It represents a business process rather than exposing raw system details.

## Q94. What is an Experience API?
**Answer:** An Experience API presents data in the form required by a specific consumer such as a web application, mobile application or partner. It prevents each consumer from implementing its own transformation and orchestration.

## Q95. Flow vs sub-flow vs private flow?
**Answer:** A flow can contain a source and processors. A sub-flow is reusable logic invoked from another flow and has simpler error-handling behavior. A private flow can be invoked internally and is useful for reusable implementation logic where a source is not required.

## Q96. What is Flow Reference?
**Answer:** Flow Reference invokes another flow or reusable processing path. It is useful for keeping implementations modular and avoiding duplicated processors.

**Support benefit:** When a common flow fails, I can trace the calling flow and the referenced flow separately.

## Q97. What is APIkit?
**Answer:** APIkit helps implement APIs from an API specification such as RAML or OAS. It can generate routing and scaffolding so implementation aligns with the contract.

## Q98. RAML vs OpenAPI?
**Answer:** Both describe APIs using machine-readable contracts. RAML is commonly associated with MuleSoft/Anypoint API design, while OpenAPI is a widely adopted industry specification. The important production concept is that the contract defines endpoints, methods, parameters, request/response structures and expected behavior.

## Q99. What is an API policy?
**Answer:** An API policy applies runtime governance or security controls to an API. Examples include client enforcement, rate limiting, authentication-related controls and traffic policies.

## Q100. How do you troubleshoot an API policy issue?
**Answer:** I determine whether the request reaches the Mule application. If it is rejected before Mule, I inspect API Manager/gateway policy behavior, credentials, client configuration and policy limits. If it reaches Mule, I continue with application-level tracing.

## Q101. What is CloudHub?
**Answer:** CloudHub is MuleSoft's managed application deployment platform. Production support commonly involves checking application state, workers, logs, properties, deployment history and runtime behavior.

## Q102. What is Runtime Manager?
**Answer:** Runtime Manager provides operational visibility and management for Mule applications and runtimes. I use it to inspect deployment status, logs, application state and runtime information according to the organization's setup.

## Q103. What is Runtime Fabric?
**Answer:** Runtime Fabric is MuleSoft's deployment/runtime technology for running Mule applications on infrastructure controlled by the organization, commonly using Kubernetes-based environments. Support responsibilities include application health, runtime behavior and coordination with platform teams.

## Q104. What is a worker?
**Answer:** A worker is a runtime unit used to execute a Mule application in CloudHub-style deployments. Worker sizing and count affect available processing capacity and resilience.

## Q105. How do you troubleshoot an application that will not start?
**Answer:** I inspect deployment status and startup logs first. Then I check missing properties, invalid configuration, connector versions, dependency issues, certificates, credentials and incompatible runtime settings. I identify the first startup error rather than focusing on every cascading message.

## Q106. What is a deployment smoke test?
**Answer:** A smoke test is a small set of high-value checks performed after deployment to confirm that the application is running and critical paths work. It normally includes health/listener validation, authentication, a representative API request and important dependency connectivity.

## Q107. What is rollback?
**Answer:** Rollback returns the application to a known-good version when the new release causes unacceptable impact and rollback is approved. Before rollback I preserve evidence and understand whether the problem is code, configuration or dependency related.

## Q108. Rollback vs fix-forward?
**Answer:** Rollback is useful when the previous version is known to be stable and immediate restoration is required. Fix-forward is appropriate when the old version is not viable or the issue can be corrected safely in the new version.

## Q109. How do you validate a production deployment?
**Answer:** I verify deployment status, startup logs, application/listener availability, environment properties, credentials/certificates, key downstream connections and critical business transactions. I also check monitoring after the deployment for unexpected errors or latency.

## Q110. What is idempotency?
**Answer:** An operation is idempotent when repeating the same logical request does not create unintended additional business effects. In integration systems, idempotency can be implemented using business keys, message IDs, processed-state tables or downstream support.

## Q111. Why is idempotency important in production support?
**Answer:** Retries, timeouts, acknowledgements and manual reprocessing can create uncertainty about whether a transaction completed. Idempotency reduces the risk of duplicate business effects during recovery.

## Q112. How do you investigate duplicate records?
**Answer:** I compare business keys, message IDs, timestamps, source events and downstream records. I determine whether duplication occurred at the source, during retry/replay, because of a lost acknowledgement, or because the downstream operation is not idempotent.

## Q113. What is a poison message?
**Answer:** A poison message is a message that repeatedly fails processing because of its content or a persistent business/technical condition. Retrying it indefinitely can block or overload the consumer.

**Production response:** isolate or route it according to the approved dead-letter/error-handling process, then investigate and reconcile.

## Q114. How do you troubleshoot MQ backlog?
**Answer:** I inspect queue depth, producer rate, consumer count/state, consumer errors, processing time, connection status and downstream latency. I determine whether the consumer is stopped, slow or repeatedly failing.

## Q115. How do you troubleshoot SFTP file-not-found?
**Answer:** I verify the remote directory, filename pattern, case sensitivity, permissions, polling configuration, file arrival time and whether another process moved the file. I compare with a known successful file.

## Q116. How do you troubleshoot database connection failures?
**Answer:** I check database availability, DNS/network path, credentials, TLS, connection-pool behavior, connection limits and the exact database error. I distinguish authentication failure from network timeout and database capacity issues.

## Q117. How do you troubleshoot a database query timeout?
**Answer:** I determine whether all queries or one query are slow. I inspect query parameters, database load, locks, execution plan information available to the DB team, network latency and connection-pool usage. I avoid repeatedly increasing timeouts without understanding the bottleneck.

## Q118. What is connection pooling?
**Answer:** Connection pooling reuses database connections instead of creating a new connection for every operation. Incorrect pool sizing can cause waiting, exhaustion or excessive database load.

## Q119. What is a timeout?
**Answer:** A timeout means an operation did not complete within the configured time. I identify which boundary timed out: client-to-Mule, Mule-to-downstream, database, SFTP, MQ or gateway. The correct fix depends on the boundary.

## Q120. Timeout vs connection refused?
**Answer:** A timeout usually means no response was received within the allowed period, while connection refused generally means the destination actively rejected the connection or no service was listening on the target endpoint/port. Network and platform evidence should confirm the exact cause.

## Q121. What is TLS?
**Answer:** TLS protects data in transit and validates the identity of the remote endpoint through certificates. Production troubleshooting includes checking certificate validity, trust chain, hostname, protocol/cipher compatibility and keystore/truststore configuration.

## Q122. What is the difference between keystore and truststore?
**Answer:** A keystore commonly contains the application's private key/certificate identity used for presenting identity, while a truststore contains certificates the application trusts when validating remote identities. Exact usage depends on one-way or mutual TLS configuration.

## Q123. What is mutual TLS?
**Answer:** In mutual TLS, both sides authenticate each other using certificates. Mule must present its client certificate and also trust the server certificate chain.

## Q124. How do you troubleshoot an SSL handshake failure?
**Answer:** I check certificate expiry, hostname/SAN, trust chain, correct alias, keystore/truststore contents, protocol compatibility and whether the correct environment configuration is deployed. I compare with a known working environment when possible.

## Q125. How do you handle a production credential expiry?
**Answer:** I confirm the impacted integrations, obtain the approved replacement securely, update the environment-specific secret/configuration, and validate authentication. I never paste credentials into source control or normal incident communication.

## Q126. What is secure configuration?
**Answer:** Secure configuration keeps secrets outside application source code and controls access by environment. Values such as passwords, tokens and private keys should be managed through approved secure mechanisms.

## Q127. How do you troubleshoot a configuration issue after deployment?
**Answer:** I compare the deployed environment configuration against the expected environment-specific values. I check property names, resolved values where safe, secrets, endpoints, certificates and deployment variables.

## Q128. What is a correlation ID vs a business transaction ID?
**Answer:** A correlation ID helps trace a technical request across logs and services. A business transaction ID identifies the business operation, such as an order or invoice. One business transaction may generate multiple technical correlation IDs across systems.

## Q129. How do you trace a transaction across multiple APIs?
**Answer:** I start with the business ID or originating correlation ID, then follow timestamps and propagated headers across System, Process and Experience APIs. I map each hop, response, error and downstream call until the failure boundary is identified.

## Q130. What is reconciliation?
**Answer:** Reconciliation compares expected business transactions with actual completed transactions. It is especially important after incidents involving queues, files, retries or partial failures because technical recovery alone does not prove business completion.

## Q131. What is a partial failure?
**Answer:** A partial failure occurs when part of a multi-step operation succeeds and another part fails. For example, one downstream update may complete while a second call fails. Recovery must determine what already happened before replaying anything.

## Q132. How do you handle a downstream API that is slow but not completely down?
**Answer:** I compare latency with normal behavior and inspect timeout, connection-pool and concurrency metrics. I avoid increasing concurrency blindly because it can increase downstream load and make the incident worse.

## Q133. What is retry storm?
**Answer:** A retry storm happens when many failing requests repeatedly retry at the same time, increasing load on an already unhealthy dependency. Controlled retry count, backoff, circuit-breaking patterns and queue-based buffering can reduce this risk.

## Q134. What is circuit breaker thinking?
**Answer:** Circuit-breaker design prevents an unhealthy dependency from receiving unlimited traffic. When failures exceed a threshold, calls can be temporarily stopped or degraded, allowing the dependency and integration to recover.

## Q135. How do you troubleshoot high latency with no errors?
**Answer:** I compare normal and incident latency across each boundary: inbound gateway, Mule processing, DataWeave, connector calls and downstream response. A transaction can be technically successful while still violating performance expectations.

## Q136. How do you handle a deployment that passes CI but fails in production?
**Answer:** I compare environment differences: properties, secrets, certificates, endpoint access, runtime version, network routes and external dependencies. A successful build proves the artifact can be built; it does not prove production configuration and dependencies are correct.

## Q137. What is a regression?
**Answer:** A regression is a previously working behavior that becomes incorrect after a change. I compare the release diff, affected flow, configuration and before/after test results.

## Q138. How do you decide whether an issue is caused by a recent release?
**Answer:** I correlate the incident start time with deployment time and compare affected behavior before and after release. I also look for unrelated dependency changes so that timing alone is not treated as proof.

## Q139. How do you communicate technical findings to business stakeholders?
**Answer:** I translate technical details into impact, current status, recovery action and next update. Instead of saying "the MQ consumer thread is blocked," I can say "file processing is delayed because the consumer is not progressing; we are validating the approved recovery and will reconcile the delayed files."

## Q140. What is your standard incident lifecycle?
**Answer:** Detect → assess impact → isolate the failing boundary → mitigate safely → verify service → reconcile business transactions → document RCA → implement prevention.

This sequence keeps recovery focused while preserving evidence and data integrity.
