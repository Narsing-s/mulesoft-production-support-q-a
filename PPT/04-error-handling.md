# Slide 04 — Error Handling & HTTP Failures

## Q28. What is a Mule error?
**Answer:** A Mule error represents a failure during event processing and includes information such as error type, description and cause. Error types help identify whether the problem is application logic, connectivity, HTTP, database, validation, or another category.

**Production approach:** I start with the error type and timestamp, then correlate it with the application, flow, request, downstream dependency and recent changes.

## Q29. On Error Continue vs On Error Propagate
**Answer:** **On Error Continue** handles the error and allows processing to complete from the caller's perspective. It is appropriate only when the business design intentionally converts the failure into a handled outcome.

**On Error Propagate** handles the error but keeps the transaction failed to the calling scope. It is appropriate when the failure must remain visible to the caller.

**Production warning:** I never use Continue just to make monitoring look healthy.

## Q30. How do you troubleshoot a failed Mule transaction?
1. Confirm timestamp and environment.
2. Capture correlation ID.
3. Identify application and flow.
4. Read the first meaningful error and nested cause.
5. Check the connector/downstream call immediately before failure.
6. Compare with successful transactions.
7. Check recent deployments, configuration, certificates and credentials.
8. Apply the safest approved mitigation.
9. Verify recovery.
10. Reconcile affected transactions and document RCA.

## Q31. What does HTTP 400 mean?
**Answer:** 400 generally indicates an invalid request. I check required fields, datatype, schema, query/path parameters and request structure before treating it as an infrastructure problem.

## Q32. What does HTTP 401 mean?
**Answer:** 401 normally indicates authentication failure. I verify token/API-key/credential presence, validity and expiry, and confirm the request is reaching the expected security layer.

## Q33. What does HTTP 403 mean?
**Answer:** 403 normally means the caller is authenticated but is not authorized. I check roles, scopes, policies, client permissions and gateway configuration.

## Q34. What does HTTP 404 mean after deployment?
**Answer:** I verify listener configuration, host/port, base path, APIkit/router configuration, environment properties, gateway route and exact requested URL. An application can be running while the requested resource still returns 404.

## Q35. What does HTTP 409 mean?
**Answer:** 409 generally represents a conflict, often caused by the resource state or a duplicate business operation. I check the business key and downstream state before retrying.

## Q36. What does HTTP 429 mean?
**Answer:** 429 indicates rate limiting or throttling. I identify whether the limit is imposed by API Manager, gateway, consumer policy, or downstream service. Controlled backoff is preferable to a retry storm.

## Q37. What does HTTP 500 mean?
**Answer:** HTTP 500 indicates an unexpected server-side failure. I trace the correlation ID and determine whether the actual cause is transformation, business logic, connector failure, configuration, or a downstream dependency.

## Q38. How do you handle a downstream 503?
**Answer:** I confirm whether the downstream service is unavailable for all calls or only this application. I check dependency health, timeout/retry behavior and recent changes. If approved, I use controlled recovery rather than unlimited retries.

## Q39. What is the difference between technical and business errors?
**Answer:** A technical error is usually infrastructure/integration related, such as timeout, DNS, TLS, connection refusal or unavailable dependency. A business error is a valid request that cannot be processed because of a business rule.

The distinction matters because retry strategy, alerting, ownership and customer response can be different.

## Q40. What should an RCA contain?
**Answer:** A strong RCA includes timeline, business impact, detection method, technical root cause, contributing factors, recovery actions, affected transactions, why existing controls did not prevent/detect it, and preventive actions with owners.
