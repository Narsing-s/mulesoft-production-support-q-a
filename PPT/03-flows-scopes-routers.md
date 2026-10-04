# Slide 03 — Flows, Scopes & Routers

## Q16. What is a Choice Router?
**Answer:** The Choice Router evaluates conditions from top to bottom. The first condition that evaluates to true is selected, and the remaining routes are skipped.

**Production example:** If an API receives `type=customer`, one route can call customer processing, another can handle orders, and an Otherwise route can return a controlled response.

**Interview point:** Choice does not execute every matching route. It selects the first matching condition.

## Q17. What happens when no Choice condition matches?
**Answer:** The Otherwise route is used when it is configured. I always describe the actual configured behavior rather than assuming every Choice automatically throws an error.

## Q18. What happens if the selected Choice route fails?
**Answer:** The selected route's error is handled by the applicable error handler. Mule does not go back and try another Choice condition. A downstream failure is therefore not a reason to expect fall-through to another route.

## Q19. What is Scatter-Gather?
**Answer:** Scatter-Gather executes multiple routes in parallel and aggregates their results. It is useful when independent calls can happen concurrently.

**Production considerations:** I check downstream capacity, timeout behavior, route-level failures, response aggregation, and whether all branches are safe to execute concurrently.

## Q20. What is the output of Scatter-Gather?
**Answer:** Scatter-Gather produces an aggregated result containing the output from its routes. I inspect the actual Mule event structure rather than assuming the result is always a simple array.

## Q21. What if one Scatter-Gather route fails?
**Answer:** The overall behavior depends on the error-handling configuration and how the failure is handled inside the route. In production I identify the failed branch, determine whether other branches completed, and decide whether retrying is safe.

## Q22. What is For Each?
**Answer:** For Each iterates over a collection sequentially. During each iteration the current item becomes the payload inside the scope.

**Production use:** It is useful when ordering matters or when I need controlled pressure on a downstream system.

## Q23. For Each vs Parallel For Each
| Area | For Each | Parallel For Each |
|---|---|---|
| Execution | Sequential | Concurrent |
| Throughput | Lower | Potentially higher |
| Ordering | Easier to control | Do not assume business ordering |
| Downstream pressure | Lower | Higher |
| Risk | Lower | Higher if dependencies are sensitive |

## Q24. What is Until Successful?
**Answer:** Until Successful repeatedly executes a scope until it succeeds or the configured retry policy is exhausted. It is appropriate for transient failures when repeating the operation is safe.

**Production warning:** I first determine whether the first attempt may already have reached the downstream system.

## Q25. When should retries be avoided?
**Answer:** I avoid blind retries for non-idempotent operations, validation errors, authorization failures, permanent 4xx responses, and situations where repeated calls can create duplicate business transactions. Retries should be bounded and observable.

## Q26. What is a Scheduler?
**Answer:** Scheduler starts a flow based on a configured schedule. In production support I verify timezone, schedule configuration, application state, previous execution status, concurrency behavior, and whether the scheduler's downstream dependency was available.

## Q27. What is a Try scope?
**Answer:** Try isolates a block of processing so that error handling can be applied locally. This is useful when one operation has a different recovery or error response requirement from the rest of the flow.
