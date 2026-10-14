<!-- ADOPTION GUIDE. Keep this file: re-run it when the framework, runner, environments,
     identity model, or test conventions change. -->

# Setup—plug the kit into this project

This is a short, repeatable setup interview for an agent. Its goal is enough verified context
to run and grow tests here, not an exhaustive audit.

## Marker model

The operating documents use three markers:

- `SETUP_REQUIRED`—the playbook is not usable for the affected workflow until filled.
- `SETUP_OPTIONAL`—useful project context that may legitimately remain open.
- `GROWTH_POINT`—a maintained catalogue or ledger; an empty one can be correct.

Setup status is:

- **Unconfigured:** one or more `SETUP_REQUIRED` markers remain.
- **Usable:** all required markers are resolved; optional markers may remain and are reported.
- **Configured:** required and applicable optional markers are resolved; inapplicable optional
  markers have been removed or explicitly marked `Not applicable`.

Growth points do not affect setup status.

## How to run setup

1. **Discover first; ask only about gaps.** Inspect test and runner configuration, package or
   build scripts, CI workflows, test folders, fixtures/helpers, and environment-file schemas.
   When inspecting `.env*` files, record variable names and structure only: never reproduce,
   commit, or print secret values.
2. **Assess before changing.** Find the remaining setup markers and read the project-specific
   content already present around them. Preserve completed configuration that is still supported
   by repository evidence. Change only an applicable unresolved marker, a demonstrably stale fact,
   or content contradicted by the current project; do not reconfigure a completed area merely
   because setup was run again.
3. **Distinguish fact from convention.** Existing code can contain accidental practice. For
   each material conclusion, preserve its provenance as **observed** (with a path), **inferred**
   (and clearly labelled), or **team-confirmed**. Ask the user before turning an uncertain
   inference into a rule.
4. **Fill and clean.** Replace applicable setup markers with project facts, remove inapplicable
   prompts, and remove every neutral example that could be mistaken for a real capability.
5. **Report.** State the resulting status, what was already complete and preserved, what was
   filled or refreshed, what remains optional, and what needs confirmation. Do not claim
   configured status merely because text was inserted.

Keep the interview light: one or two questions per area, and group related gaps.

## Discovery map

| Find out | Destination |
|---|---|
| Framework; run one test, an area, and the complete suite | [`TEST-EXECUTION.md`](TEST-EXECUTION.md) → Scope |
| Local, CI, dedicated, or remote environments and invocation | [`TEST-EXECUTION.md`](TEST-EXECUTION.md) → Environments |
| Retry boundaries, reset, artifacts, reports, and skip visibility | [`TEST-EXECUTION.md`](TEST-EXECUTION.md) → Reliability |
| Data creation, templates, uniqueness, time, and cleanup | [`TEST-DATA-AND-ENVIRONMENTS.md`](TEST-DATA-AND-ENVIRONMENTS.md) → Data |
| Identity, secret names, and the environment-debug guide | [`TEST-DATA-AND-ENVIRONMENTS.md`](TEST-DATA-AND-ENVIRONMENTS.md) → Environment |
| Test structure, naming, tags, abstraction level, and a real example | [`TEST-AUTHORING.md`](TEST-AUTHORING.md) |
| Curated reusable entry points and where they live | [`TEST-PATTERN-CATALOGUE.md`](TEST-PATTERN-CATALOGUE.md) |
| Diagnostic commands, logs, launchers, and attach procedures | [`TEST-DIAGNOSTIC-METHODS.md`](TEST-DIAGNOSTIC-METHODS.md) |
| Known-issue mechanism and reporting semantics (`xfail`, skip, quarantine, etc.) | [`TESTS-WITH-KNOWN-ISSUES.md`](TESTS-WITH-KNOWN-ISSUES.md) |

## Completion check

- No applicable `SETUP_REQUIRED` marker remains.
- Commands and paths are copy-pasteable and traceable to repository evidence.
- Inferences are labelled or confirmed; observed accidents have not silently become policy.
- No secret value or misleading neutral example remains.
- Selected known-issue mechanisms document whether tests execute, whether unexpected passes
  are visible, and how the run is counted.
- The close-out says: **Status** · **Already complete** · **Filled/refreshed** ·
  **Optional/open** · **Needs confirmation**.

Hand the user back to [`TESTING-PLAYBOOK.md`](TESTING-PLAYBOOK.md). Keep this guide for later
reconfiguration.
