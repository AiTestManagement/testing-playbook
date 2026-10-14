<!-- PORTABLE TEMPLATE: live ledger, reporting semantics, fingerprint matching, and retirement. -->

# Tests with Known Issues

The live ledger of tests that are expected to fail, quarantined, or excluded now, with evidence
and removal criteria. Durable failure knowledge belongs in
[`TEST-FAILURE-AND-FIX-PATTERNS.md`](TEST-FAILURE-AND-FIX-PATTERNS.md).

## Match before relying on a row

A listed test is not automatically “accounted for.” Confirm that the current symptom, failure
fingerprint, environment, and affected scope match the row. A known issue and a new regression can
coexist in the same test. If the fingerprint differs or the scope grows, diagnose it as new.

## Mechanisms are not interchangeable

Document both spelling and reporting semantics. Depending on the framework:

- **Expected failure (`xfail`-like):** usually executes and can expose an unexpected pass.
- **Quarantine:** executes separately or does not gate, but must still publish a result.
- **Skip/disabled:** does not exercise the contract and provides little health evidence.
- **Capability gate:** runs only where a declared capability exists; it is not a defect tier.

Prefer the mechanism that preserves the most useful evidence. Do not label a transient
environmental interruption as a test defect; classify that run invalid under
[`TEST-EXECUTION.md`](TEST-EXECUTION.md). Record recurring environment limitations in the linked
project environment guide or incident/run system so they remain operationally visible.

<!-- SETUP_REQUIRED: Record the project's exact expected-failure, quarantine, skip/disabled, and
capability-gate mechanisms that apply. For each, state whether the test executes, whether an
unexpected pass is visible, whether it gates, and how it is counted. -->

## Cause classes

Use one cause per entry; map the label to the project's configured mechanism.

| Cause | Meaning | Remove when |
|---|---|---|
| test/specification defect | expectation or scenario data is reproducibly wrong | corrected and proven |
| harness defect | driver, fixture, client, wait, locator, or result parsing is wrong | corrected and proven |
| unstable/race | outcome changes with no intended input change | cause fixed and stress/repeat evidence meets the stated bar |
| subject defect | the test correctly exposes a known product/library bug | subject fix is deployed in the tested environment and the test passes |

Do not keep “retired” tests in the active tree merely for history. Delete them with a linked reason;
version control preserves the record. A time-bounded quarantine pending a concrete reactivation
decision must have an owner and review date.

## Ledger discipline

- Every marker has one ledger row and every row has a marker; audit both directions.
- Re-check a row when its `review-by` date arrives and whenever its fingerprint changes.
- Remove the marker and row as soon as the retirement condition is proven.
- A long or old ledger is a release risk, not background documentation.

## Entry template

```markdown
### <marker>—<short title>
- **What:** exact tests/area and stable identifiers.
- **Fingerprint:** expected symptom, error/observation, environment, and affected scope.
- **Cause/status:** specification | harness | unstable | subject; current evidence.
- **Evidence/pattern:** run, artifact, reproduction, and optional durable pattern link.
- **Mechanism semantics:** executes? gates? unexpected pass visible? result count?
- **Owner/ticket:** accountable person/team and issue link.
- **Added / last observed / review-by:** dates.
- **Remove when:** exact condition that removes both row and marker.
```

## Current entries

<!-- GROWTH_POINT: Add live entries grouped by cause. Empty is valid. -->
