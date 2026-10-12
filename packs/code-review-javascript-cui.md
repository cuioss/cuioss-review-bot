<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the javascript-cui code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the javascript-cui domain of a code review.

- Defects specific to javascript-cui: the code-review rules this organisation states for javascript-cui code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for javascript-cui code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- A `package.json` without `"type": "module"` in a project whose sources use `import` / `export`, so Node and Jest load the files as CommonJS and fail on the module syntax.
- A required npm script (`lint`, `format`, `test`, `test:ci-strict`, `quality`) removed or renamed, so the Maven build step that runs it fails, or a check the build relies on no longer runs.
- A dependency change in `package.json` with no matching `package-lock.json` change, so `npm ci` in the build rejects the mismatch or installs versions other than the ones tested locally.
- A JavaScript source file placed outside the source directory of the project's type (standard Maven, Quarkus DevUI, NiFi extension, standalone), so it is linted and tested but never packaged into the built artifact.
- A Node.js version in `package.json` `engines` that differs from the version the frontend-maven-plugin installs, so the local build and the Maven build run on different Node versions.
