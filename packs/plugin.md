<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target pr-agent --output target/pr-agent
This artifact carries the plugin domain part alone. The review charter lives in the
spine artifact (spine.md) and appears in no domain artifact, so this file on its
own carries none of it. Apply the spine artifact alongside this one.
-->

Prioritise security and correctness over style. This pack is scoped to the plugin domain.

- Defects specific to plugin: the rules this organisation enforces for plugin code are listed under "Domain rules" below.

Domain rules — this organisation's own standards for plugin code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- Never read an environment variable (`os.environ.get(...)`) and construct a filesystem `Path`, a subprocess argv element, or a network target from it without validating it against a safe base or allow-list first. Environment is an untrusted boundary in a tool a consumer project drives.
- Never pass a value sourced from an extension's `get_skill_domains()` (a `domain` key, a profile name, a skill notation) into a downstream filesystem, subprocess, or import call without confirming it against the declared allow-list of known domains/profiles. Extension data is bundle-author-controlled, not core-controlled.
- Never add a new external-content ingestion surface (web page, GitHub issue/PR/comment body, Sonar message, or any other attacker-influenceable text) that consumes raw bytes in a write-capable or skill-loading context without routing the candidate struct through the deterministic `plan-marshall:untrusted-ingestion:validate_struct` gate.
- Never author skill/command/agent prose that interpolates untrusted external text into instructions the model will execute, nor that can be read as an instruction-injection vector.
- Strictly comply with all rules from `plan-marshall:persona-plan-marshall-agent`, especially tool usage and workflow step discipline.
- Every externally-sourced value (environment, CLI args, file contents read from a consumer project, extension-provided data, external web/issue/Sonar text) is untrusted at the boundary where the marketplace script or doc first consumes it.
- Reject untrusted input that fails a boundary check; never coerce it through. Fail closed.
