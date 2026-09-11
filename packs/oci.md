<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target pr-agent --output target/pr-agent
This artifact carries the oci domain part alone. The review charter lives in the
spine artifact (spine.md) and appears in no domain artifact, so this file on its
own carries none of it. Apply the spine artifact alongside this one.
-->

Prioritise security and correctness over style. This pack is scoped to the oci domain.

- Defects specific to oci: the rules this organisation enforces for oci code are listed under "Domain rules" below.

Domain rules — this organisation's own standards for oci code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- Do not run containers as root; always use non-root USER instruction
- Do not mount Docker daemon socket into containers
- Do not skip vulnerability scanning in CI/CD pipelines
- Do not load all standards at once; load progressively based on current task
- All containers must drop all capabilities (`--cap-drop=ALL`) and selectively add required ones
- Read-only filesystems required with tmpfs for write directories
- Images must be signed and verified before deployment
- SBOM must be generated and attached to images
