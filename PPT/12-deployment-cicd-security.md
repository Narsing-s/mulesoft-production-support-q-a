# 12 — Deployment, CI/CD & Security

## Slide 1 — CI/CD
A typical pipeline is:

**Build → unit/API tests → package → security/config checks → deploy → smoke test → monitor.**

Production support should understand what was deployed, which version is running and what validation was completed.

## Slide 2 — POM
The Maven POM defines project metadata, dependencies, plugins, build behavior and deployment configuration.

For Mule applications, the mule-maven-plugin can support packaging and deployment.

## Slide 3 — Secrets
Never hardcode:
- passwords
- client secrets
- private keys
- access tokens

Use approved secure/environment-specific configuration and restrict access.

## Slide 4 — Secure Properties
Environment-specific secrets should be injected securely rather than committed to Git.

When troubleshooting, confirm:
- correct environment
- correct property name
- expected secret version
- runtime has loaded the new value
- no secret is exposed in logs

## Slide 5 — Certificate Troubleshooting
For TLS failures check:
1. expiry
2. certificate chain
3. hostname/SAN
4. keystore/truststore
5. alias
6. protocol/cipher compatibility
7. environment configuration

## Slide 6 — Keystore vs Truststore
**Keystore:** commonly contains the application's private key and certificate identity.

**Truststore:** contains certificates/CA certificates the application trusts.

For mutual TLS, both client identity and server trust requirements may be involved.

## Slide 7 — Rollback Decision
Rollback is appropriate when:
- impact is significant
- release correlation is strong
- known-good version exists
- rollback will not create data inconsistency

Fix-forward can be better when rollback would worsen compatibility or data problems.

## Slide 8 — Post-Deployment Validation
Do not stop at “deployment successful.”

Validate:
- application state
- startup logs
- listener/API endpoint
- authentication/policies
- key dependencies
- representative business transaction
- monitoring/error rate
- queues/files/backlog where applicable

## Slide 9 — Questions 75–80
75. Explain CI/CD for MuleSoft.
76. What is the POM?
77. What is mule-maven-plugin?
78. How do you manage secure properties?
79. How do you troubleshoot certificate expiry/TLS?
80. Rollback vs fix-forward?

## Slide 10 — Interview Takeaway
Production deployment is complete only when the application is **running, reachable, functionally validated and monitored**.
