# 03 — Flows, Scopes & Routers

## Slide 1 — Choice
Evaluates conditions in order. First true route wins. Otherwise runs when none match.

Scenario: if a matched route fails, later Choice routes are not evaluated.

## Slide 2 — Scatter-Gather
Runs multiple routes in parallel and aggregates results. Investigate route-level failures before retrying.

## Slide 3 — For Each
Sequentially processes collection items. Current item becomes payload during iteration.

## Slide 4 — Parallel For Each
Processes items concurrently. Check downstream capacity, ordering and duplicate risk.

## Slide 5 — Other Scopes
Try, Async, Until Successful, Scheduler and Batch.

## Questions
16. Choice Router?
17. What if all conditions fail?
18. What if selected route errors?
19. Scatter-Gather?
20. Scatter-Gather output?
21. What if one route fails?
22. For Each vs Parallel For Each?
23. Until Successful?
24. When should retries be avoided?
25. Scheduler?
