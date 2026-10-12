<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the java-cui code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the java-cui domain of a code review.

- Defects specific to java-cui: the code-review rules this organisation states for java-cui code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for java-cui code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- A logging call that passes the exception after the message or `LogRecord` instead of first, so the exception is consumed as a format argument and its stack trace is never logged.
- An INFO, WARN, ERROR or FATAL call that logs a string literal instead of a `LogRecord` from a LogMessages class, so the message carries no identifier and cannot be asserted in a test or looked up in the documentation.
- A `CuiLogger` message that uses an SLF4J-style `{}` placeholder instead of `%s`, so the argument is never substituted and the logged line shows the literal braces.
- Two `LogRecord` constants in one LogMessages class that share an identifier number, so the identifier no longer names exactly one message and a log search returns both.
- A `LogRecord` the change adds or edits with no `LogAsserts` check in a test, so a changed message text, level or identifier ships without any test turning red.
