<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the java domain part alone. The review charter lives in the
spine artifact (spine.md) and appears in no domain artifact, so this file on its
own carries none of it. Apply the spine artifact alongside this one.
-->

Prioritise security and correctness over style. This pack is scoped to the java domain.

- Defects specific to java: the rules this organisation enforces for java code are listed under "Domain rules" below.

Domain rules — this organisation's own standards for java code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- Do not log authentication tokens, passwords, secrets, certificate contents, PII, or session identifiers
- Do not hardcode secrets in source; resolve all secrets from external configuration
- Do not silently coerce invalid inbound data; reject on any constraint violation at the trust boundary
- Do not leak internal details (paths, credentials, stack internals) in error messages returned to callers
- Externally-sourced data (deserialized payloads, file inputs, CLI arguments, message-queue bodies) must be validated at the trust boundary before use
- Security configuration must be validated fail-fast at startup, not lazily at runtime
- Security events are logged; sensitive data is masked or omitted
