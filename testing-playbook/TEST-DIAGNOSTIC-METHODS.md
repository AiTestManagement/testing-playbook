<!-- PORTABLE TEMPLATE: ownership hypotheses, evidence methods, and a local toolkit. -->

# Test Diagnostic Methods

How to confirm a diagnosis against the relevant system and context before changing code.
[`TEST-FAILURE-AND-FIX-PATTERNS.md`](TEST-FAILURE-AND-FIX-PATTERNS.md) catalogues recurring
shapes; this document explains how to prove one.

## Form an ownership hypothesis

Treat these as hypotheses, not mutually infallible labels:

1. **Specification/test:** the claim, expected behaviour, or scenario data is wrong.
2. **Automation/harness:** the mechanism that drives, seeds, observes, or adapts the subject is
   wrong—for example a locator, wait, fixture, client, or result parser.
3. **Subject:** the application, service, or library violates the relevant contract.
4. **Environment:** hosts, dependencies, configuration, identity provisioning, or runner state
   prevent a trustworthy verdict.

A fault may cross boundaries. Name the leading hypothesis, its strongest alternative, and the one
observation that would separate them. Broad correlated failure raises the priority of shared
causes; it does not prove “environment.”

<!-- SETUP_OPTIONAL: Map project triage labels, commands, or ticket ownership to these terms. -->

## Evidence methods

- **Preserve the original context.** Capture the failed run's identity, inputs, environment,
  timestamps, logs, and artifacts before reproducing it.
- **Read the subject's own I/O.** Logs and traffic from the failing context can reveal state,
  routing, and identity. Redact secrets and personal data.
- **Use controlled comparative probes.** A request from another session or identity can isolate
  cache, routing, or provisioning differences, but label it as a different context and never treat
  its success as proof that the original context succeeded.
- **Add temporary in-code probes.** Log the state immediately before the failing action and dump
  what exists when an expected item is absent. Mark temporary probes and remove them before commit.
- **Use controlled fault injection.** Reproduce remote-only conditions locally with a stub, test
  double, or approved fault-injection mechanism. Never modify a shared/live service merely to force
  a diagnostic condition.
- **Commit durable diagnostics when justified.** If failures occur only where attach is impossible,
  retain safe, bounded ground-truth diagnostics in the harness or product until the class is
  designed out.

## Two high-value habits

- **Return to the contract.** When subject and harness appear correct, verify that the test asserts
  the behaviour it was intended to protect.
- **Report observed values.** `expected X, got <old>` suggests stale state; `<nothing>` suggests
  not-found; `<different>` suggests wrong-target. These are leads to confirm, not diagnoses.

## Project diagnostic toolkit

Keep concrete, copy-pasteable procedures here. Record provenance and verify that each tool sees the
intended target before trusting its output.

```markdown
### <name>—<what it lets you prove>
- **Method:** original-I/O | comparative-probe | temporary-probe | fault-injection | durable-diagnostic
- **How:** exact command, script, or steps
- **Context:** environment and identity represented; important differences from the failed run
- **Gotchas:** paths, auth, policy, privacy, per-machine configuration
- **Confirm:** how to verify the diagnostic tool itself is attached to the intended target
- **Verified:** YYYY-MM-DD; source or owner
```

<!-- SETUP_REQUIRED: Replace this marker with real diagnostic procedures or an explicit statement
that the project currently has none. Do not leave neutral examples that look executable. -->

<!-- GROWTH_POINT: Add a procedure only after it has proved useful; review and prune stale ones. -->
