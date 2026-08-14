<!-- PORTABLE TEMPLATE: durable failure shapes with evidence and discriminators. -->

# Test Failure and Fix Patterns

A catalogue of recurring failure shapes: how to recognise them, distinguish look-alikes, confirm
ownership, and design out recurrence. Specific currently affected tests belong in
[`TESTS-WITH-KNOWN-ISSUES.md`](TESTS-WITH-KNOWN-ISSUES.md); diagnostic procedures belong in
[`TEST-DIAGNOSTIC-METHODS.md`](TEST-DIAGNOSTIC-METHODS.md).

## Principles

- **Same symptom, opposite fix:** always identify the strongest look-alike and the evidence that
  separates it.
- **Convenient signals can lie:** a bare status code, toast, spinner, wrapper job, or missing
  confirmation may disagree with the promised contract. Prefer the most authoritative practical
  observation.
- **Assertions should diagnose:** include safe observed values and correlation context.
- **A condition wait is not timeout padding:** wait for an observable condition to a bounded,
  justified deadline; never lengthen a delay merely to reduce failures.
- **Environment interruption invalidates; it does not pass:** retain evidence, classify the run
  invalid, recover, and execute a fresh run. Do not rerun repeatedly until green.

## Starter map

These are neutral shapes, not claims about the host project:

| ID | Layer | Mechanism | Shape and discriminator |
|---|---|---|---|
| C1 | harness/subject | timing | present-but-not-actionable versus never enabled; observe actionable state |
| C2 | harness/environment | shared state | leaked client/session versus wrong scenario data; compare clean isolated run |
| C3 | subject/data | propagation | confirmed write with lagging read versus absent write; inspect authoritative write evidence |
| C4 | environment/subject | identity | one identity fails versus general defect; compare equivalent known-good provisioning |
| C5 | harness/subject | rendering | virtualised/off-screen versus never created; inspect source collection and rendered window |
| C6 | harness/subject | signal | proxy reports success/failure contrary to the contract; inspect authoritative result |

Remove or replace starter rows during setup if they do not fit the project. Do not cite a neutral
row as a diagnosed project failure without evidence.

## Pattern entry

```markdown
## <ID>—<short name>
**Essence:** one sentence; name the strongest look-alike.
**Owner/layer:** specification | harness | subject | environment; affected layer.
**Mechanism:** timing | state | data | identity | rendering | signal | other.
**Symptom:** directly observed evidence, not the inferred cause.
**Distinguish from:** the observation that separates the look-alike.
**Confirm:** reproducible procedure or linked diagnostic method.
**Response:** fix/triage, or classify invalid and recover if environmental.
**Design out:** how to prevent or expose recurrence.
**Provenance:** source/run/ticket and last-verified date.
```

<!-- GROWTH_POINT: Add only confirmed recurring classes. Merge duplicates and remove stale or
project-irrelevant entries; version control preserves their history. -->
