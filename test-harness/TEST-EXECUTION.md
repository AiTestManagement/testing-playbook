<!-- PORTABLE TEMPLATE: scope, environment, result states, and observable reliability policy. -->

# Test Execution

How tests are invoked, where they run, and how a trustworthy result is classified. Test craft
lives elsewhere; this document owns runner and CI policy.

## Scope—run the narrowest proof, then widen by risk

| Scope | Typical use | Command |
|---|---|---|
| One test/case | authoring or diagnosing one claim | <!-- SETUP_REQUIRED: exact command/selectors --> |
| Area/pack | neighbouring behaviour or area-shared code changed | <!-- SETUP_REQUIRED: exact command/selectors and project term --> |
| Complete suite | release/pre-merge or broad shared change | <!-- SETUP_REQUIRED: exact command and relationship to CI --> |

A narrow pass proves only its scope. Use
[`TEST-AUTHORING.md`](TEST-AUTHORING.md#validate-by-blast-radius) to decide how far to widen.

## Environments

<!-- SETUP_REQUIRED: Replace with the real environments. For each, record prerequisites, exact
invocation, identity, authoritative result location, and artifact location. Delete inapplicable
categories. -->

- **Local:** project-specific details.
- **CI:** workflow/trigger and result location.
- **Dedicated runner/VM:** host lifecycle and access constraints.
- **Remote/queued:** dispatch, correlation ID, and authoritative completion signal.

## Result model

Classify each run explicitly:

- **Pass:** the intended tests executed and their assertions passed.
- **Valid failure:** the run was capable of judging the contract and one or more tests failed.
- **Invalid run:** infrastructure or environment prevented a trustworthy verdict. Preserve the
  reason and evidence; an invalid run is neither pass nor product failure.

Report executed, passed, failed, expected-failed, unexpectedly-passed, skipped, and invalid counts
separately. An authored test, queued job, green wrapper step, or silent skip is not a pass.

After an invalid run, recover or wait for the environment and start a separately identified fresh
run. Do not repeatedly rerun a valid failed assertion until it happens to pass.

## Reliability policy

- **Allowed retry boundaries:** bounded, observable retry may protect an explicitly classified
  infrastructure/launch operation or exercise retry behaviour promised by the subject. Record the
  attempts and terminal result. Never retry an assertion or replace a valid failed result.
- **Condition waits:** poll a meaningful condition to a justified deadline; do not inflate a fixed
  sleep or timeout to conceal a race.
- **Reset before the run:** a prior crash can bypass cleanup, so restore owned runner state before
  starting and record reset failure as invalid.
- **Publish on failure:** retain safe logs, reports, and artifacts even when tests or setup fail.
- **Make non-execution loud:** selected-versus-executed and skip/expected-failure counts must be
  visible in the authoritative result.
- **Pin and update dependencies:** pin actions/tools for reproducibility and supply-chain control;
  assign an owner and cadence or automation for reviewed updates.

CI-only failure is a differential, not an owner. Compare order, concurrency, resources, locale,
clock, filesystem, dependencies, build output, identity, configuration, and artifacts before
classifying it as test, harness, subject, or environment.

<!-- SETUP_REQUIRED: Record retry boundaries and limits, condition-wait defaults, pre-run reset,
artifact/report handling, result counts, and dependency-update ownership. -->
