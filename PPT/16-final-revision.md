# 16 — Final Revision

## Slide 1 — First 10 Questions to Practice
1. Explain your MuleSoft production-support responsibilities.
2. Walk through a P1/P2 incident.
3. How do you trace a transaction?
4. An API returns intermittent 500 — how do you troubleshoot?
5. Explain Choice, Scatter-Gather, For Each and Parallel For Each.
6. Continue vs Propagate?
7. How do you troubleshoot DB/SFTP/MQ?
8. Explain a DataWeave transformation problem.
9. How do you safely reprocess a failed transaction?
10. Why should we hire you?

## Slide 2 — Your Production Incident Structure
Use this sequence:

**Impact → Scope → Timestamp/Correlation ID → Logs/Metrics → First failing boundary → Recent changes → Safe mitigation → Verification → Reconciliation → RCA.**

Do not jump directly to a fix.

## Slide 3 — Strong Choice Router Answer
“Choice evaluates routes from top to bottom and executes the first condition that evaluates to true. Once a route is selected, the other routes are not executed. If no condition matches and an otherwise route exists, otherwise executes. If the selected route fails, normal Mule error handling applies; Choice does not automatically try another route.”

## Slide 4 — Strong Scatter-Gather Answer
“Scatter-Gather sends the Mule event through multiple routes concurrently and aggregates their results. I would consider route-specific failures, timeouts, downstream capacity and whether the operations are safe to run in parallel. If one branch fails, I would inspect the configured error-handling behavior and identify exactly which branch failed before deciding on mitigation.”

## Slide 5 — Strong Reprocessing Answer
“Before reprocessing, I confirm the affected scope and whether the original attempt partially succeeded. I check business IDs, target-side state and idempotency controls. Then I reprocess only the approved scope, monitor the result and reconcile source versus target counts.”

## Slide 6 — Strong P1 Answer
“For a P1, I first confirm business impact and scope and establish the incident bridge. I collect timestamps and correlation IDs, divide investigation by system boundary, communicate facts and apply the safest approved mitigation. After recovery I verify service, reconcile affected transactions and contribute evidence to the RCA.”

## Slide 7 — Strong ‘Mule or Downstream?’ Answer
“I prove the boundary rather than assuming ownership. I check whether Mule received the request, whether the flow processed it, what Mule sent downstream, what the downstream system returned and whether timestamps/correlation IDs match. That evidence tells us where the failure actually occurred.”

## Slide 8 — Strong ‘Why Change?’ Answer
“I am looking for stronger growth and more challenging MuleSoft responsibilities. I want to deepen my L2/L3 production-support and integration skills and take ownership of more complex incidents.”

## Slide 9 — Final Interview Rules
- Answer the question first.
- Explain reasoning when asked.
- Use production examples without confidential client details.
- Never claim experience you do not have.
- Do not invent metrics or timelines.
- Say what evidence you would check.
- Mention safe mitigation and verification.
- Distinguish mitigation from root cause.

## Slide 10 — Final Mindset
**Detect → Isolate → Mitigate → Verify → Reconcile → Prevent.**

If you get stuck, return to this sequence and explain what evidence you would collect next.
