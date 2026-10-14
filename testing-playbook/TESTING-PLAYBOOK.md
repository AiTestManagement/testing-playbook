<!-- PORTABLE TEMPLATE: front door, router, sequence, gate, and maintenance contract. -->

# Testing Playbook

The operating guide for authoring, running, and debugging automated tests in this repository.
It governs testing work under `testing-playbook/`, not the wider project. This directory is the whole
installed kit: its operating documents do not depend on the source repository's root files.

> **Adopting the kit?** Follow [`SETUP.md`](SETUP.md). If a `SETUP_REQUIRED` marker remains,
> the affected workflow is unconfigured. `SETUP_OPTIONAL` can remain in a usable installation;
> `GROWTH_POINT` marks living content and is not a setup failure.

## Scope and force of the guidance

The **core** guidance applies broadly. UI/API and behavioural-test guidance is an
**applicable profile**, not a universal requirement. Apply a profile only when it matches the
test's level and purpose.

Words such as **must** and **never** state the kit's safe default. A host project may override a
default deliberately when the exception, reason, owner, and visibility are documented. A rule
must not be weakened merely to make a run green.

## Document router

| Document | Use it for |
|---|---|
| **TESTING-PLAYBOOK** (this file) | Orientation, sequence, gate, glossary, maintenance |
| [`TEST-AUTHORING.md`](TEST-AUTHORING.md) | Test scope, abstraction boundary, decomposition, reuse, blast radius |
| [`TEST-PATTERN-CATALOGUE.md`](TEST-PATTERN-CATALOGUE.md) | Curated reusable entry points and semantic-fit decisions |
| [`TEST-DATA-AND-ENVIRONMENTS.md`](TEST-DATA-AND-ENVIRONMENTS.md) | Known data state, environment, identity, and secrets |
| [`TEST-EXECUTION.md`](TEST-EXECUTION.md) | Scope, environments, result states, and observable reliability policy |
| [`TEST-DIAGNOSTIC-METHODS.md`](TEST-DIAGNOSTIC-METHODS.md) | Confirming whether specification, harness, subject, or environment owns a failure |
| [`TEST-FAILURE-AND-FIX-PATTERNS.md`](TEST-FAILURE-AND-FIX-PATTERNS.md) | Durable recurring failure shapes and discriminating evidence |
| [`TESTS-WITH-KNOWN-ISSUES.md`](TESTS-WITH-KNOWN-ISSUES.md) | Live exclusions, expected failures, quarantine, and retirement |

## Example prompts

You do not need special commands or agent skills. Ask your agent for the testing outcome you need
and point it at the relevant playbook document. These are the authoritative installed-copy
examples; the source repository README mirrors them for people evaluating the kit.

If you are unsure which document applies, start here:

> Read `testing-playbook/TESTING-PLAYBOOK.md`, route this request through the appropriate playbook
> documents, and tell me which guidance you applied: `<describe the test task>`.

### Review against the Definition of Done

> Read `testing-playbook/TESTING-PLAYBOOK.md`. Review the tests changed on this branch against the core
> Definition of Done and any applicable test-type profile. Report specific gaps with file evidence,
> and fix them if they are within the scope of this change.

### Author a test

> Read `testing-playbook/TEST-AUTHORING.md` and the related project-specific guidance. Add a test for
> `<behaviour>`. First find its correct test level and home, check for duplicate coverage and
> semantically matching helpers, then implement and validate it at the appropriate blast radius.

### Find or create a reusable pattern

> Read `testing-playbook/TEST-PATTERN-CATALOGUE.md`. Before creating a helper for `<need>`, search the
> catalogue and code for an existing semantic match. Recommend reuse, a local implementation, or a
> new shared abstraction, with the consumers and blast radius that support your decision.

### Prepare test data and environments

> Read `testing-playbook/TEST-DATA-AND-ENVIRONMENTS.md`. Work out how this project should establish the
> prerequisite state for `<scenario>`, including identity, uniqueness, time, and cleanup. Use
> repository evidence, identify any missing configuration, and do not expose secret values.

### Run tests

> Read `testing-playbook/TEST-EXECUTION.md`. Run the narrowest scope that proves `<change>`, widen
> according to its blast radius, and report the authoritative result as pass, valid failure, or
> invalid run. Keep skips, expected failures, retries, and non-execution visible.

### Diagnose a failure

> Read `testing-playbook/TEST-DIAGNOSTIC-METHODS.md`. Diagnose this failure without changing code first:
> `<failure or run link>`. Preserve the original context, identify the leading ownership hypothesis
> and strongest alternative, then gather the evidence that distinguishes them.

### Capture a recurring failure pattern

> Read `testing-playbook/TEST-FAILURE-AND-FIX-PATTERNS.md`. Determine whether `<failure>` matches an
> existing pattern. If it is a genuinely new recurring class, confirm the cause and look-alike
> discriminator, then add a concise evidence-backed entry. Do not record an unconfirmed one-off
> symptom as a pattern.

### Handle a known issue

> Read `testing-playbook/TESTS-WITH-KNOWN-ISSUES.md`. Check whether `<failure>` genuinely matches a
> current ledger fingerprint. If it is a confirmed live issue, use the project's evidence-preserving
> mechanism and add or update the ledger entry with owner, evidence, review date, and exact removal
> condition.

### Configure it

> Read `testing-playbook/SETUP.md` and configure the playbook for this repository. Discover facts from
> the repository first. Check its setup markers and existing project-specific content before making
> changes; preserve areas that are already valid, and configure only applicable gaps or facts that
> are demonstrably stale. Distinguish observed facts from inferences, ask only about genuine gaps,
> never reproduce secret values, and report the resulting setup status.

## Operating model

```text
  change ─► AUTHOR ─► RUN ── pass ───────────────► done
                       │
                       ├─ valid failure ─► DEBUG ─► fix/triage ─► fresh run
                       │
                       └─ invalid run ───► preserve evidence ─► recover ─► fresh run

  every durable lesson ─► write back to the relevant versioned document
```

Two invariants hold:

1. **Knowledge lives in versioned evidence, not heads.** Write back reusable, proven lessons;
   include provenance and remove them when stale.
2. **Never mask a failed assertion.** Do not convert a failure into a pass through a rerun,
   inflated timeout, silent skip, or weakened assertion. Bounded, observable retry can be valid
   at an explicitly classified infrastructure/launch boundary or as behaviour the product itself
   promises; it must not erase the original event.

## The three loops

### Author

1. Find the test's level, purpose, home, and nearest existing coverage.
2. Search the reuse catalogue and code; reuse only where the semantics and lifecycle match.
3. Keep mechanics below the test's chosen abstraction boundary.
4. Establish only the prerequisite data and environment relevant to the behaviour.
5. Clear the core Definition of Done and any applicable profile.
6. Add a catalogue entry only for a durable, high-value reusable entry point.

### Run

1. Use the narrowest scope that can prove the change, then widen by blast radius.
2. Select the environment and identity deliberately; invoke it per
   [`TEST-EXECUTION.md`](TEST-EXECUTION.md).
3. Classify the outcome as **pass**, **valid failure**, or **invalid run**. Count executed,
   passed, failed, expected-failed, skipped, and invalid distinctly.

### Debug

1. Check the known-issue ledger, then confirm the current failure fingerprint actually matches.
2. Form an ownership hypothesis: specification/test, automation/harness, subject, or environment.
3. Gather discriminating evidence before changing anything.
4. Fix or triage a valid failure. For an invalid environmental run, retain evidence, recover the
   environment, and start a fresh run; do not rerun repeatedly until green.
5. Write back only a durable new pattern, procedure, or live issue.

## Definition of Done

### Core—all automated tests

- [ ] **Purpose:** one clear claim at an intentional test level; stable identity where the
  project uses one; duplicate coverage checked.
- [ ] **Assertions:** observes the most authoritative practical signal, reports actual values,
  and has been shown capable of failing for the intended reason.
- [ ] **Isolation:** dependencies, time, randomness, order, identity, and shared state are either
  controlled or explicitly declared.
- [ ] **Readability:** mechanics do not leak above the abstraction level the test is meant to
  describe; precision is not hidden behind unnecessary abstractions.
- [ ] **Reliability:** no failed assertion is masked; skips, expected failures, retries, and
  invalid runs remain visible and separately counted.
- [ ] **Validation:** passes at the narrowest useful scope and at every wider scope justified by
  the change's blast radius.
- [ ] **Maintenance:** new shared abstractions have semantic fit, diagnostics, ownership, and a
  justified maintenance benefit.

### Behavioural/integration/API/UI profile—when applicable

- [ ] Reads as domain behaviour; selectors, positions, transport calls, and widget mechanics live
  below that boundary unless they are themselves the contract under test.
- [ ] Prerequisite state is established through the lowest suitable layer outside the behaviour
  under test; generated identifiers are captured rather than assumed.
- [ ] Generated data is collision-safe; mutable time is controlled; cleanup or reset ownership is
  explicit.
- [ ] Eventual consistency uses a condition-based bounded wait; UI presence, bare status codes,
  spinners, and toasts are not treated as authoritative without justification.

## Glossary

- **Specification/test:** the claim, expected behaviour, and scenario data.
- **Automation/harness:** code that drives, observes, seeds, or adapts the subject for the test.
- **Subject:** the application, service, library, or system behaviour being tested.
- **Environment:** hosts, dependencies, configuration, identity provisioning, and runner state.
- **Pack/area:** a project-defined group of related tests; use the project's actual term.
- **Authoritative signal:** the closest practical observation of the behaviour promised by the
  relevant contract—not merely a convenient proxy.
- **Invalid run:** a run whose environment or infrastructure prevented a trustworthy verdict.
- **Recognise:** classify with evidence and preserve visibility; it does not mean ignore.
- **Masking:** making a real failure disappear without correcting or explicitly classifying it.

## Playbook maintenance

At adoption, before a release, and periodically thereafter:

- [ ] Relative Markdown links resolve; the router matches the files shipped.
- [ ] The authoritative example prompts here and the source repository README remain aligned.
- [ ] **Portable-template release:** intended setup/growth markers remain well formed and no host
  values or secrets have leaked in. **Adopted-project release:** no applicable `SETUP_REQUIRED`
  marker or misleading neutral example remains.
- [ ] Optional setup gaps and documented policy exceptions are explicit.
- [ ] Catalogue entries still point to real, recommended code and show a verification date.
- [ ] Known-issue rows and test markers agree both ways; `review-by` dates are current.
- [ ] Failure patterns contain evidence and a discriminator, not unsupported folklore.
- [ ] Superseded guidance is pruned; version control retains its history.
