<!-- PORTABLE TEMPLATE: known data state plus a compact environment/identity contract. -->

# Test Data and Environments

How a suite reaches a known state and how it identifies the environment in which a verdict is
valid. Apply only the practices relevant to the test level; pure tests may need none of the
external-data guidance.

## Part A—test data

- **Use the lowest suitable setup layer outside the behaviour under test.** Prefer an API or
  fixture for a UI test, but use the UI when UI creation is the behaviour being proved.
- **Confirm asynchronous setup.** When a successful write is not immediately readable, poll the
  authoritative read condition to a bounded deadline and retain the final observation.
- **Prefer explicit inputs.** Clone an immutable template and override scenario-relevant values;
  avoid mutable global defaults and unexplained symbolic fixtures.
- **Capture produced identifiers.** Read generated identifiers from the creating operation and
  carry them by handle rather than assuming stable values.
- **Prevent collisions.** Give generated mutable data a run-unique identity when parallel or
  interrupted runs can overlap.
- **Control time.** Use a controllable clock or relative value for moving scenarios; use a fixed
  date when that exact date is part of the contract.
- **Distinguish reference from generated data.** A single stale-looking reference value is a
  diagnostic lead, not permission to refresh it blindly—confirm whether it is stale or exposes a
  legitimate edge case.
- **Own cleanup or reset.** State who deletes generated state, when reset occurs, and what happens
  after an interrupted run. Avoid an implicit “probably clean” assumption.

<!-- SETUP_REQUIRED: Record applicable seeders/fixtures, immutable templates, uniqueness scheme,
time control, and cleanup/reset ownership. Mark non-applicable items explicitly. -->

## Part B—environment, identity, and secrets

Keep hostnames, credential formats, and detailed recovery procedures in a project-local
environment guide; link it here.

- **Attach versus launch:** if a run attaches to an existing app or session, record inherited
  state and lifecycle ownership.
- **Identity chain:** login success does not prove downstream provisioning. Record every identity
  boundary relevant to the verdict.
- **Failure breadth is evidence, not proof:** a whole class failing similarly makes shared
  environment, configuration, fixture, harness, or product code the first comparison set. Use a
  preflight and a known-good comparison to discriminate them.
- **Unavailable dependencies invalidate a run:** preserve the evidence, mark the run invalid, wait
  for recovery, then start a fresh run. Do not loop until green or weaken the test.
- **Never commit secrets:** document logical variable/secret names and stores, never values. Do not
  echo values during setup or diagnostics.

<!-- SETUP_REQUIRED: Link the project-local environment/debug guide or state that none is needed;
list applicable execution environments and identity boundaries. -->

<!-- SETUP_OPTIONAL: Record safe preflight commands and secret-name/schema documentation. -->

Runner retry, reset, artifact, and result-counting policy belongs in
[`TEST-EXECUTION.md`](TEST-EXECUTION.md).
