# test-harness

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

Current version: **0.1.0**

## What's in it

The self-contained [`test-harness/`](test-harness/) distribution contains eight short operating
documents, led by [`TEST-HARNESS.md`](test-harness/TEST-HARNESS.md), plus
[`SETUP.md`](test-harness/SETUP.md), a one-time adoption and reconfiguration guide.
Project-specific slots are marked separately from places intended to grow over time.

## What this does not do

test-harness is a playbook, not tooling. It deliberately does not:

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

1. Copy the `test-harness/` folder into your repository. Keep the folder name so these files
   do not collide with project-level documentation.
2. Add this snippet to the instruction file your agent reads (`AGENTS.md`, `CLAUDE.md`, or
   `.github/copilot-instructions.md`):

```markdown
## Testing—use the test-harness playbook

For automated test work, start at `test-harness/TEST-HARNESS.md` and follow its router.
Apply its core Definition of Done and any relevant test-type profile. Treat a retry,
timeout increase, skip, or exclusion as a controlled decision that must remain visible;
never turn a failed assertion into a pass by rerunning it. Write durable lessons back into
the relevant playbook document.
```

Then ask an agent to run [`test-harness/SETUP.md`](test-harness/SETUP.md). It discovers
repository facts, asks only about genuine gaps, fills required setup markers, removes neutral
examples, and reports the result. A project can be **usable** while optional setup remains; the
setup guide defines the statuses precisely.

## Grow it

Write back durable knowledge: a reusable entry point, a proven failure pattern, a diagnostic
procedure, or a live known issue. Keep observations linked to evidence and prune entries when
they stop helping. The feedback loop—not the starter text—is the product.

## Licence

Released under the [MIT License](LICENSE).

## Release readiness

Before publishing or copying the kit, run the document-maintenance check in
[`test-harness/TEST-HARNESS.md`](test-harness/TEST-HARNESS.md#playbook-maintenance). It covers
links, unresolved setup, neutral examples, known-issue reviews, and catalogue drift without adding
dependencies. The check distinguishes release of this portable template from release of an
adopted, project-configured copy.
