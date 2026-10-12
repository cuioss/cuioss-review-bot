<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the javascript code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the javascript domain of a code review.

- Defects specific to javascript: the code-review rules this organisation states for javascript code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for javascript code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- A promise that is neither awaited, returned nor given a `.catch`, so a rejection surfaces as an unhandled rejection and the caller carries on before the work has finished.
- An `await` inside an `Array.prototype.forEach` callback, so the loop does not wait for the iterations and the code after it runs before they complete.
- A loose `==` or `!=` comparison between values of different types, so type coercion (`0 == ''`, `null == undefined`) selects the wrong branch.
- A `||` default applied to a value that can legitimately be `0`, `''` or `false`, so the valid falsy value is replaced by the default where `??` keeps it.
- An event listener, timer or observer a web component registers in `connectedCallback` with no matching removal in `disconnectedCallback`, so a detached component keeps running its handlers and is never released.
- A function that mutates an array or object it received (`sort`, `splice`, property assignment) while the caller still holds it, so the caller's data changes behind its back.
- An async test that neither awaits nor returns the promise under test, including an un-awaited `expect(...).resolves` or `.rejects`, so the test finishes before the assertion runs and passes whatever the result.
- A test whose assertions sit inside a callback or a `catch` with no `expect.assertions(n)`, so the test passes when the callback never runs or nothing is thrown.
- A module mock, `jest.spyOn` or fake-timer switch with no restore in `afterEach` (`restoreAllMocks`, `useRealTimers`), so the mock leaks into later tests and they pass or fail by execution order.
- A test that waits with a fixed `setTimeout` instead of fake timers or `waitFor`, so it fails intermittently whenever the awaited update arrives later than the fixed delay.
