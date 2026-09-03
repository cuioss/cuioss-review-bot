<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target pr-agent --output target/pr-agent
This artifact carries the javascript domain part alone. The review charter lives in the
spine artifact (spine.md) and appears in no domain artifact, so this file on its
own carries none of it. Apply the spine artifact alongside this one.
-->

Prioritise security and correctness over style. This pack is scoped to the javascript domain.

- Defects specific to javascript: the rules this organisation enforces for javascript code are listed under "Domain rules" below.

Domain rules — this organisation's own standards for javascript code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- Do not assign untrusted data to `innerHTML`, `outerHTML`, or `insertAdjacentHTML` — these parse and execute injected markup
- Do not hand-roll HTML sanitization with regex; use a vetted allow-list sanitizer
- Do not render untrusted data into the DOM without choosing a text-treating sink or sanitizing first
- Untrusted data rendered into the DOM is an XSS trust boundary; the safe default is a text-treating sink (`textContent`, `createElement` + `textContent`)
- When rendering untrusted HTML is a genuine requirement, sanitize with a vetted library (DOMPurify) and prefer Trusted Types where the platform supports it
- DOMPurify is a third-party dependency — adding it is a user-approval step
