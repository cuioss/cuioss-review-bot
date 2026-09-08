<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target pr-agent --output target/pr-agent
This artifact carries the python domain part alone. The review charter lives in the
spine artifact (spine.md) and appears in no domain artifact, so this file on its
own carries none of it. Apply the spine artifact alongside this one.
-->

Prioritise security and correctness over style. This pack is scoped to the python domain.

- Defects specific to python: the rules this organisation enforces for python code are listed under "Domain rules" below.

Domain rules — this organisation's own standards for python code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- Do not pass untrusted input to `subprocess` with `shell=True`; use an argv list
- Do not `pickle.load`/`pickle.loads` untrusted bytes, nor `yaml.load` without a safe loader
- Do not `eval`/`exec`/`compile` externally-sourced strings; use `ast.literal_eval` for literals
- Do not interpolate user values into SQL query strings; use DB-API placeholders with a params tuple
- Every externally-sourced value (request data, file contents, environment, CLI args) is untrusted at stdlib boundaries
- User-supplied paths must be validated against a safe base to prevent traversal
- Reject untrusted input that fails a boundary check; never coerce it through
