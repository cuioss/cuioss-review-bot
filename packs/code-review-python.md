<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the python code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the python domain of a code review.

- Defects specific to python: the code-review rules this organisation states for python code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for python code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- A local assignment, loop variable, or `with … as` / `except … as` target that rebinds a name the module imports at top level, so later code in the same scope that expects the imported object reads the rebound value instead.
- A function whose default argument is a mutable object (a list, dict or set) that the body mutates, so state written on one call is visible to every later call.
- A bare `except:` or an `except Exception:` that neither re-raises nor narrows to the failure it handles, so an unexpected error — a programming bug included — is swallowed and the function carries on with partial state.
- A value that can be `None` (an `X | None` annotation, a `dict.get`, a `re.match` result) dereferenced without a `None` check, so an absent entry raises `AttributeError` or `TypeError` on an ordinary input.
- A file, socket or process opened outside a `with` block or `try`/`finally`, so an exception before the close leaks the handle or leaves a partially written file behind.
- A `match` statement over a closed set of variants with no `case _` arm, so a value outside the handled cases falls through and the function returns `None` as if it had handled it.
- An `asyncio.create_task` result that is neither awaited nor kept, so the task can be garbage-collected mid-run and its exception is never observed.
- A test that changes the working directory, an environment variable, a module attribute or other process-global state by direct assignment instead of through `monkeypatch`, so the change leaks into later tests in the same worker and they pass or fail by collection order.
- A test that reads or writes a real path outside `tmp_path`, so parallel workers or a second run collide on the same file and the result depends on whatever is already on disk.
- A test for a guard, refusal or classifier that supplies the triggering input but no matched negative control — the same input with only the triggering condition removed — so a guard that fires on every input still passes.
- A `conftest.py` placed below the test root, so tests that `import conftest` for the shared helpers resolve the nearer file instead, or collection fails on a second module named `conftest`.
- A test that builds command arguments as a hand-written `argparse.Namespace` instead of through the real parser, so a parser default or a renamed flag the production call depends on is never exercised.
