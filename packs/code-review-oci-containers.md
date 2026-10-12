<!-- GENERATED ARTIFACT — do not edit by hand.
Derived from the cuioss/plan-marshall marketplace (marketplace/bundles/**).
Regenerate with:
  ./pw generate --target cuioss-review-bot --output target/cuioss-review-bot
This artifact carries the oci-containers code-review rules alone. The code-review charter lives in
the code-review spine artifact (code-review-spine.md) and appears in no code-review domain
artifact, so this file on its own carries none of it. Apply the code-review spine artifact
alongside this one.
-->

This pack is scoped to the oci-containers domain of a code review.

- Defects specific to oci-containers: the code-review rules this organisation states for oci-containers code are listed under "Domain rules" below.

Domain rules — this organisation's own code-review standards for oci-containers code. A diff that breaks one of these is a finding, and the rule already names the mechanism:
- A `COPY --from=<stage>` whose source path the named build stage no longer produces (a renamed artifact, a moved build output directory), so the image build fails or copies the wrong file into the runtime stage.
- An `ADD` used to copy a local file, so an archive is unpacked into the image instead of copied as the file the next instruction expects.
- An `apt-get update` (or the equivalent package-index refresh) in a different `RUN` layer than the install that depends on it, so a cached, stale index layer makes the install fail or pull outdated packages.
- A `HEALTHCHECK` that runs `curl`, `wget` or a shell in a distroless or scratch image, so the command does not exist and the container is reported unhealthy however the application behaves.
- A Quarkus management-interface property (`quarkus.management.*`) set only at runtime when it is fixed at build time, so the native image has no management endpoint and every health probe against it fails.
- A `.dockerignore` that does not exclude local build output (`target/`, `node_modules/`, `dist/`), so a stale local artifact is copied into the image in place of the freshly built one.
- A multi-platform build whose `RUN` step downloads or copies a binary for a single architecture, so the image for the other platform carries a binary it cannot execute.
