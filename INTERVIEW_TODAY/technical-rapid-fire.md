# Technical Rapid-Fire — Customer Interview

## API-led connectivity
**Q:** What are the common API layers?  
**A:** Experience, Process and System APIs. The exact layering depends on the organization's architecture.

## Flow vs Sub-flow
**Q:** Difference?  
**A:** A flow has a source such as an HTTP Listener and can have its own error handling. A sub-flow is reusable processing invoked from another flow and does not have its own event source or error handler.

## Flow Reference
**Q:** Why use Flow Reference?  
**A:** To invoke reusable flow logic while keeping the application modular.

## Try scope
**Q:** Why use Try?  
**A:** To isolate a section of processing and apply local error handling or transactional behavior.

## Scatter-Gather
**Q:** What does it do?  
**A:** Executes routes in parallel and collects their results. It is useful when independent calls can run concurrently.

## Choice router
**Q:** Purpose?  
**A:** Routes processing based on conditions.

## For Each
**Q:** Purpose?  
**A:** Iterates over items in a collection and processes each item.

## Batch
**Q:** When useful?  
**A:** For processing large datasets in records/chunks rather than treating the entire dataset as one synchronous event.

## Object Store
**Q:** Why might support teams care about it?  
**A:** It can persist application state or values such as tokens, watermarks or other operational state, depending on the design.

## Watermark
**Q:** What is it?  
**A:** A value representing the last successfully processed point, commonly used to support incremental processing and avoid repeatedly reading the same data.

## Idempotency
**Q:** What does it mean?  
**A:** Repeating the same operation does not create an unintended additional business effect. It is important for retries and message redelivery.

## Backpressure
**Q:** What does it mean?  
**A:** Preventing an overloaded consumer/downstream system from being overwhelmed by controlling or slowing incoming work.

## Throttling vs Rate Limiting
**Q:** Difference?  
**A:** Both control traffic. Rate limiting restricts requests to a defined rate/window; throttling can dynamically control or reject traffic to protect a service.

## Round Robin
**Q:** What is it?  
**A:** A load-balancing approach that distributes requests sequentially across available instances/endpoints.

## Circuit Breaker
**Q:** What problem does it solve?  
**A:** It stops repeated calls to an unhealthy dependency after failures cross a threshold, then tests recovery after a cooldown. Typical states are Closed, Open and Half-Open.

## Retry
**Q:** What should you consider before retrying?
**A:** Whether the error is transient, retry count/backoff, downstream capacity and idempotency. Blind retries can worsen an outage.

## 429
**Q:** What does it indicate?
**A:** Too many requests/rate limiting. Check API policy, client traffic and retry-after behavior where provided.

## 502 / 503 / 504
**A:** 502 commonly indicates a bad gateway/upstream response; 503 indicates service unavailable; 504 indicates gateway/upstream timeout. Always confirm the actual source of the response in logs.

## Authentication vs Authorization
**A:** Authentication establishes who/what is calling. Authorization determines what that authenticated caller is allowed to access.

## SLA
**Q:** What does SLA mean in support?
**A:** The agreed service-level target for response/resolution or related support commitments. Incident handling should be driven by severity and SLA.

## MTTR
**Q:** What is MTTR?
**A:** Mean Time To Repair/Restore, a measure of how quickly service is restored after incidents. Organizations may define the exact metric differently.

## Health check vs business validation
**A:** A health check confirms technical availability. Business validation confirms the actual integration/business transaction works.

## Smoke test
**Q:** What is it?
**A:** A focused set of checks after deployment or recovery to confirm critical functionality works before considering the change successful.

## Rollback
**Q:** When use it?
**A:** When an approved release causes a critical issue and returning to a known-good version is the safest recovery option.

## Hotfix
**Q:** What is it?
**A:** A targeted production fix for a specific defect, deployed through the organization's change/emergency process.

## RCA vs problem management
**A:** RCA identifies why an incident occurred. Problem management uses recurring incidents and RCA findings to reduce or eliminate future incidents.
