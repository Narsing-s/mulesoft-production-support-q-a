# Slide 13 — Advanced L2/L3 Questions

## Q81. Mule CPU is suddenly high. What do you check?
**Answer:** I compare CPU with deployment time and traffic volume. Then I inspect payload sizes, transformation complexity, loops, concurrency, repeated processing, logging and downstream latency.

I determine whether one flow or the whole application is affected. The objective is to identify the workload causing CPU consumption rather than simply restarting the worker.

## Q82. What causes memory pressure?
**Answer:** Common causes include large payload materialization, high concurrency, retaining large objects in variables, inefficient transformations, large logging statements and unusually large files.

I correlate memory behavior with traffic and releases and check whether garbage collection is recovering memory. Resizing alone is not a complete fix for a recurring leak or inefficient processing pattern.

## Q83. What is thread starvation?
**Answer:** Thread starvation occurs when execution threads are occupied or blocked long enough that other work cannot progress normally. Slow synchronous dependencies, blocking operations, excessive concurrency and contention can contribute.

I investigate thread activity together with dependency latency, connection pools and CPU.

## Q84. Restart temporarily fixes the issue. What next?
**Answer:** I treat the restart as mitigation, not root cause. I compare the system before and after restart and identify the state that gradually returns: connection exhaustion, memory growth, stuck consumers, thread blockage, queue buildup or dependency instability.

A recurring restart requirement is evidence that permanent corrective action is needed.

## Q85. How do you handle an issue you cannot reproduce?
**Answer:** I preserve production evidence: correlation IDs, exact timestamps, payload shape, response codes, dependency responses, metrics and configuration at the time of failure. I compare failed and successful transactions.

If it is intermittent, I add targeted observability rather than making broad production changes.

## Q86. How do you give an ETA during an incident?
**Answer:** I do not invent a time. I communicate current impact, what is confirmed, what is being investigated, the next action and the next update time.

A strong update is evidence-based and gives stakeholders confidence without making an unsupported promise.

## Q87. L2 vs L3 support?
**Answer:** L2 generally performs operational diagnosis, log analysis, configuration checks, recovery, reprocessing and coordination.

L3 goes deeper into code, architecture, performance, complex defects, permanent fixes and resilience improvements. Both levels require evidence, controlled changes and clear documentation.

## Q88. What makes a good production-support engineer?
**Answer:** Technical knowledge is necessary, but production support also requires judgment. A strong engineer understands impact, communicates clearly, protects data integrity, avoids risky actions, restores service safely and converts incidents into preventive improvements.

## Q89. How do you isolate whether Mule or SAP is failing?
**Answer:** I trace the transaction boundary by boundary. I verify whether Mule received the request, whether the outbound SAP call was attempted, the response/error returned, and whether SAP shows the same transaction.

This prevents assigning blame based only on where the alert appeared.

## Q90. What is safe reprocessing?
**Answer:** Safe reprocessing means confirming the original transaction state before replaying it, identifying the business key/message ID, understanding retry semantics, and ensuring the downstream operation is idempotent or otherwise protected from duplicates.

After replay, I verify the business result rather than assuming a successful HTTP response means the full business process completed.
