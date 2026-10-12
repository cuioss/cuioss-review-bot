<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the plan-marshall-plugin-dev code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the plan-marshall-plugin-dev domain of a code review.

- Defects specific to plan-marshall-plugin-dev: the code-review rules this organisation states for plan-marshall-plugin-dev code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for plan-marshall-plugin-dev code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- A component whose frontmatter `description` still advertises behaviour, a mode or a mechanism the body no longer implements, so a caller that selects the component by its description loads the wrong one.
- A `SKILL.md` whose frontmatter declares no `mode`, or a value outside `knowledge`, `workflow`, `script-executor` and `manifest`, so an agent loading it cannot tell whether to read it as reference or execute it as steps.
- A relative link, `Read:` target or skill notation in a component that names a file, section or skill that does not exist, so a reader following it reaches nothing.
- A lesson id quoted in skill prose, so the instruction depends on a record that is archived or removed while the prose stays.
- An index table (a rules card, a command table, a step-dispatch table) that lists fewer rows than the set it indexes, so a reader takes the omitted member for absent.
- A canonical-invocation block whose subcommand, flags or flag position differ from the script's argparse declaration, so a caller who copies it gets an argparse rejection.
- A documented call that runs a marketplace script by its file path instead of through `python3 .plan/execute-script.py {bundle}:{skill}:{script}`, so it bypasses the executor's notation resolution and logging and breaks when the bundle is installed elsewhere.
- A script that exits non-zero on an operation failure (an unknown plan, a missing file, an input it validated itself) instead of exiting 0 with `status: error`, so a caller branching on the TOON `status` never reaches its error branch.
- A script that writes its result as JSON or free text instead of TOON on stdout, or a TOON payload whose `[N]` count or `{fields}` header disagrees with its rows, so the caller's parser misreads the result.
- An argparse `help=` string that advertises more than one accepted input form while the handler passes the raw value through with no normalization, so every advertised form but one fails at run time.
