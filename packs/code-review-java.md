<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the java code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the java domain of a code review.

- Defects specific to java: the code-review rules this organisation states for java code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for java code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- An `Optional.get()` (or `orElseThrow()` with no message) reached on a path where the value can be absent, so an ordinary empty result throws `NoSuchElementException` instead of taking the absent branch.
- A class that overrides `equals` without `hashCode`, or computes them over different fields, so two equal instances land in different hash buckets and a `HashMap` or `HashSet` lookup misses the entry.
- A stream, reader, channel or connection opened outside try-with-resources, so an exception before the close leaks the resource.
- A `catch` block that is empty, or logs and continues with a `null` or default value, so the caller receives that value as if the operation had succeeded.
- A check-then-act on shared state (`containsKey` then `put`, a null check then lazy assignment) with no lock and no atomic method such as `computeIfAbsent`, so two threads both pass the check and one write is lost.
- A test of an exception path written as `try` / `catch` with no `fail()` after the call under test, so the test passes when no exception is thrown at all.
- A `@Test` method that calls the code under test and asserts nothing about its result, so it passes whatever the code returns.
- A test that depends on state another test left behind (a static field, a shared file, a declared method order), so it passes or fails by execution order instead of by the behaviour under test.
- A test that waits with `Thread.sleep` for an asynchronous result instead of an Awaitility condition, so it fails intermittently whenever the result arrives later than the fixed sleep.
- A `@param` tag whose name no longer matches a parameter of the method, or a parameter the change added with no `@param`, so the documented contract describes an argument the method does not take.
- A `@throws` tag for an exception the method no longer throws, or a newly thrown checked or documented exception with no `@throws`, so a caller handles the wrong failure.
- A JavaDoc nullness or return claim ("never returns null", "returns an empty list when …") that the implementation contradicts, so a caller omits the check the actual return value needs.
- A `{@link}` or `@see` reference to a class or member the change renamed or removed, so the reference points nowhere and the JavaDoc build fails under doclint.
