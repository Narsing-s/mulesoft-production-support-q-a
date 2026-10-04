# 04 — Error Handling

## Slide 1 — Continue vs Propagate
On Error Continue handles the error and allows successful completion from the caller perspective.

On Error Propagate handles or enriches the error and propagates failure upward.

## Slide 2 — Troubleshooting
Timestamp → correlation ID → application → flow → error type → stack trace → dependency → recent changes → mitigation → verification.

## Slide 3 — HTTP Codes
400 bad request; 401 authentication; 403 authorization; 404 resource/path; 409 conflict; 429 throttling; 500 server failure; 502/503/504 gateway/upstream/service availability.

## Questions
26. What is a Mule error type?
27. How do you handle HTTP errors?
28. How do you troubleshoot a failed transaction?
29. API unavailable — what do you do?
30. API running but requests fail?
31. Latency suddenly increases?
32. Database connection fails?
33. SFTP file is not processed?
34. MQ queue has backlog?
35. What is RCA?
36. What should an RCA contain?
