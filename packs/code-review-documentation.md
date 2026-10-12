<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the documentation code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the documentation domain of a code review.

- Defects specific to documentation: the code-review rules this organisation states for documentation code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for documentation code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- A list with no blank line before it, so AsciiDoc renders the items as a continuation of the preceding paragraph instead of a list.
- A link to another document written as a Markdown link (`[text](file.adoc)`) instead of an `xref:`, so AsciiDoc renders the literal brackets and no link.
- An `xref:` whose target file or anchor does not exist after the change, so the rendered link leads nowhere.
- A delimited block (`----`, `====`, `|===`) whose closing delimiter is missing or does not match the opening one, so the rest of the document renders inside the block.
- A section heading that skips a level (`==` followed directly by `====`), so the renderer warns and the table of contents places the section under the wrong parent.
- A document that describes a feature, option, command or behaviour the code does not have — removed, renamed or never built — so a reader who follows it gets an error or a silent no-op.
- A code or configuration example whose API, flags or keys no longer match the current code, so a reader who copies it gets a failure the document does not mention.
- A changelog, dated update section or account of superseded behaviour inside documentation of the current state, so a reader cannot tell which statements still hold.
- A factual claim (a performance figure, a conformance statement, a standard or RFC citation) with no source or verifiable reference, so the reader acts on a statement nobody checked.
- A `TODO`, placeholder or empty section in published documentation, so the reader reaches a gap exactly where the needed instruction should be.
- One term used for two different concepts, or two terms used for one concept, across a document set, so a reader conflates the concepts or searches for the wrong name.
