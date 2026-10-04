# 08 — CloudHub, Runtime Manager & Runtime Fabric

## Slide 1 — Runtime Manager
Runtime Manager provides operational control and visibility for deployed Mule applications.

For production support, use it to inspect:
- application status
- deployments
- workers/replicas
- logs
- runtime information
- operational behavior

It is an important starting point, but downstream systems may need separate investigation.

## Slide 2 — CloudHub
CloudHub is MuleSoft-managed application hosting.

When troubleshooting a CloudHub application, check:
1. deployment state
2. runtime/startup logs
3. worker/replica health
4. listener availability
5. environment properties
6. downstream connectivity
7. application metrics

## Slide 3 — Runtime Fabric
Runtime Fabric (RTF) allows Mule applications to run on infrastructure controlled by the organization, commonly using Kubernetes-based infrastructure.

Support engineers may need to understand both:
- Mule application/runtime behavior
- platform/container/infrastructure health

## Slide 4 — Worker / Replica
A worker or replica is an execution instance of the application.

More instances can improve capacity or availability, but scaling does not automatically fix:
- slow downstream systems
- bad queries
- connection limits
- incorrect configuration
- poison messages

## Slide 5 — vCore
A vCore represents a unit of compute capacity used for Mule runtime resources.

For production incidents, correlate resource pressure with:
- traffic
- payload size
- deployment changes
- transformation complexity
- concurrency
- downstream latency

## Slide 6 — Application Won't Start
Check startup logs for:
- missing properties
- invalid configuration
- dependency/version issues
- certificate/keystore problems
- connector initialization failures
- invalid XML/configuration

Fix the actual startup cause rather than repeatedly restarting.

## Slide 7 — Deployment Validation
After deployment:

**Deployment status → startup logs → listener/health → dependencies → smoke test → critical business transaction → monitoring.**

A green deployment is not enough. Prove the application is actually usable.

## Slide 8 — Rollback vs Fix-Forward
**Rollback:** return to a known-good version when the new release causes unacceptable impact and rollback is safe.

**Fix-forward:** correct the defect and deploy a controlled fix when that is safer or faster.

Consider data changes, partial processing, compatibility and business impact before either action.

## Slide 9 — Questions 63–68
63. CloudHub vs Runtime Fabric?
64. What is a worker/replica?
65. What is a vCore?
66. How do you validate a deployment?
67. What is rollback?
68. Rollback vs fix-forward?

## Slide 10 — Interview Takeaway
Always distinguish:

**Application health ≠ platform health ≠ dependency health.**

A Mule application can be running while SAP, DB, SFTP, MQ or another downstream dependency is failing.
