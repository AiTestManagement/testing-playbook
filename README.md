# Testing Playbook

*A testing playbook your AI agent reads—and grows.*

```text
                    ┌──────────────────────┐
        read how-to │   the playbook docs  │  write back
          ┌─────────►    (you grow these)  ◄─────────┐
          │         └──────────────────────┘         │
          │                                          │
   change ─►   AUTHOR   ───►   RUN   ───►   DEBUG ────┘
```

A lean, framework-agnostic playbook for authoring, running, and debugging automated
tests. It provides universal testing discipline plus concrete guidance for behavioural,
integration, API, and UI/acceptance tests. Plain Markdown, zero dependencies, compatible
with any test framework and any AI coding agent—or no agent at all.

Current version: **0.2.0**

## What's in it

The self-contained [`testing-playbook/`](testing-playbook/) distribution contains eight short operating
documents, led by [`TESTING-PLAYBOOK.md`](testing-playbook/TESTING-PLAYBOOK.md), plus
[`SETUP.md`](testing-playbook/SETUP.md), a one-time adoption and reconfiguration guide.
Project-specific slots are marked separately from places intended to grow over time.

## What this does not do

Testing Playbook is a playbook, not tooling. It deliberately does not:

- **Set up your test framework.** You bring the framework, runner, and language; this adds
  testing discipline on top.
- **Track test state or report results.** It holds know-how, not the current pass/fail or
  coverage state. Use your test-management system for that (for example, `gtms`).
- **Configure or drive CI.** It documents how runs should work but does not modify workflows.
- **Fix failing tests automatically.** You diagnose and fix them, then write durable lessons
  back into the playbook.
- **Enforce its gate.** The Definition of Done is a review checklist unless the host project
  deliberately wires it into automation.
- **Arrive complete.** It is a configured starter that gains value through use and review.

## Adopt it

1. Copy the `testing-playbook/` folder into your repository. Keep the folder name so these files
   do not collide with project-level documentation.
2. Add this snippet to the instruction file your agent reads (`AGENTS.md`, `CLAUDE.md`, or
   `.github/copilot-instructions.md`):

```markdown
## Testing—use the Testing Playbook

For automated test work, start at `testing-playbook/TESTING-PLAYBOOK.md` and follow its router.
Apply its core Definition of Done and any relevant test-type profile. Treat a retry,
timeout increase, skip, or exclusion as a controlled decision that must remain visible;
never turn a failed assertion into a pass by rerunning it. Write durable lessons back into
the relevant playbook document.
```

Then ask an agent to run [`testing-playbook/SETUP.md`](testing-playbook/SETUP.md). It discovers
repository facts, asks only about genuine gaps, fills required setup markers, removes neutral
examples, and reports the result. A project can be **usable** while optional setup remains; the
setup guide defines the statuses precisely.

## Upgrade from v0.1.x

Existing installations contain project-specific knowledge and must be renamed in place:

1. Rename `test-harness/` to `testing-playbook/`.
2. Rename `testing-playbook/TEST-HARNESS.md` to
   `testing-playbook/TESTING-PLAYBOOK.md`.
3. Merge the v0.2.0 upstream text changes into the renamed files; do not replace the
   configured folder with a fresh copy.
4. Replace the complete Testing Playbook instruction snippet in `AGENTS.md`, `CLAUDE.md`, or
   `.github/copilot-instructions.md`, and update saved prompts.
5. Search the host repository case-insensitively for `test[- ]harness` and update product paths
   or names in documentation, CI, and other integrations. Retain legitimate generic references
   to executable test harnesses.

The rename alone does not require `SETUP.md` to be rerun. Run setup again only when the normal
reconfiguration guidance calls for it or the merge exposes a genuine configuration gap.

## Configure it

> Read `testing-playbook/SETUP.md` and configure the playbook for this repository. Discover facts from
> the repository first. Check its setup markers and existing project-specific content before making
> changes; preserve areas that are already valid, and configure only applicable gaps or facts that
> are demonstrably stale. Distinguish observed facts from inferences, ask only about genuine gaps,
> never reproduce secret values, and report the resulting setup status.

## Use it

You do not need special commands or agent skills. Ask your agent for the testing outcome you need
and point it at the relevant playbook document.

If you are unsure which document applies, start at the front door:

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

## Grow it

Write back durable knowledge: a reusable entry point, a proven failure pattern, a diagnostic
procedure, or a live known issue. Keep observations linked to evidence and prune entries when
they stop helping. The feedback loop—not the starter text—is the product.

## Licence

Released under the [MIT License](LICENSE).

## Release readiness

Before publishing or copying the kit, run the document-maintenance check in
[`testing-playbook/TESTING-PLAYBOOK.md`](testing-playbook/TESTING-PLAYBOOK.md#playbook-maintenance). It covers
links, unresolved setup, neutral examples, known-issue reviews, and catalogue drift without adding
dependencies. The check distinguishes release of this portable template from release of an
adopted, project-configured copy.
