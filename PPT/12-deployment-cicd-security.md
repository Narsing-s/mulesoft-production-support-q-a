# 12 — Deployment, CI/CD & Security

## Slide 1 — Secrets
Never hardcode passwords, tokens or private keys. Use secure/environment-specific configuration.

## Slide 2 — Certificates
Check expiry, alias/truststore, certificate chain and hostname validation.

## Slide 3 — CI/CD
Build → test → package → deploy → smoke test → monitor.

## Slide 4 — Maven
POM defines dependencies/plugins/build configuration. mule-maven-plugin supports Mule packaging/deployment.

## Slide 5 — Rollback
Use a known-good version when impact is high and rollback is safe. Fix-forward when controlled and safer.

## Questions
75. CI/CD?
76. POM?
77. mule-maven-plugin?
78. Secure properties?
79. Certificate expiry?
80. Rollback vs fix-forward?
