<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the requirements code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the requirements domain of a code review.

- Defects specific to requirements: the code-review rules this organisation states for requirements code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for requirements code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- A requirement ID reused for a new requirement, or an existing requirement renumbered, so every specification, code comment and test that cites the ID now points at a different requirement.
- A requirement without a measurable acceptance criterion ("fast", "scalable", "user-friendly"), so no test can decide whether it is met.
- A specification section with no backtracking link to the requirement it implements, or a link whose anchor does not exist, so the requirement cannot be traced to its specification.
- A specification status (PLANNED, IN PROGRESS, IMPLEMENTED) that disagrees with the code — IMPLEMENTED with no implementation, or PLANNED for behaviour that ships — so a reader plans against the wrong state.
- A requirement removed or rewritten while specifications, code comments or tests still cite its ID, so those citations rest on a statement the requirement no longer makes.
- A requirement that prescribes an implementation (a class, library or data structure) instead of the required behaviour, so a valid alternative implementation is judged non-compliant.
