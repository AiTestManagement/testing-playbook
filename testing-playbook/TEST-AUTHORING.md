<!-- PORTABLE TEMPLATE: abstraction boundary, semantic reuse, data, and blast radius. -->

# Test Authoring

How to write a test at an intentional level without creating avoidable maintenance burden.
Read this before authoring; configure it with patterns actually observed and confirmed here.

## How tests are authored here

<!-- SETUP_REQUIRED: Record the framework and test structure; file locations; base
classes/fixtures; naming and identity conventions; how prerequisite state is created; and one
minimal real example linked to its source. Label facts observed/inferred/team-confirmed. -->

<!-- SETUP_OPTIONAL: Record project-specific tolerated vocabulary, sanctioned exceptions, and
common abstraction leaks. Remove this marker if none are needed. -->

## Choose the test level first

Name what contract this test protects: a function, component, protocol, API, user journey, or
cross-system behaviour. The right vocabulary follows from that choice. A parser unit test may
properly mention tokens; a protocol test may properly mention headers; an acceptance test usually
should not mention selectors or HTTP verbs.

Avoid duplicating a claim already proven more cheaply at a lower level unless the higher-level
integration is itself the risk.

## The abstraction boundary

Keep mechanics below the level the test is intended to describe:

- **At the readable level:** use the precise language of the chosen contract.
- **Below it:** isolate incidental driving and observation mechanics in an appropriate adapter,
  fixture, helper, page object, or client.

> **Litmus test:** can the intended reader understand exactly what contract failed without first
> decoding incidental plumbing? Do not hide contract-relevant detail merely to sound more
> “business readable.”

For behavioural/API/UI tests, common leaks include:

| Leak | Avoid when incidental | Prefer |
|---|---|---|
| Mechanics nouns | “the Columns panel”; `POST /orders` | “the visible fields”; “create the order” |
| Literal actions | “click Documents”; “send a PUT” | “attach the document”; “amend the order” |
| Positional coupling | “row 2”; field `[3]` | the captured entity; the named contract field |

A data-heavy operation may accept a record of values in one call. Keep the operation intentional
and assertions focused on behaviour. If a UI control, endpoint, or layout is the contract under
test, name it directly and document that level rather than abstracting it away.

## Reuse by semantic fit

1. Search [`TEST-PATTERN-CATALOGUE.md`](TEST-PATTERN-CATALOGUE.md), neighbouring tests, and code.
2. Reuse an existing block only when its intent, ownership, lifecycle, and failure semantics match.
3. Do not add flags or discriminators to a shared abstraction solely to avoid small local
   duplication.
4. Allow a little local duplication while the right abstraction is uncertain; extract when a
   stable repeated concept is visible.
5. Before editing shared code, find its consumers and validate the resulting blast radius.

<!-- SETUP_OPTIONAL: Name the project's reuse mechanisms and any routing/discriminator convention,
including where each is defined. -->

## Data and setup

Establish prerequisites through the lowest suitable layer outside the behaviour under test. A UI
journey normally seeds through an API or fixture; a test of UI creation must use the UI. Clone
templates rather than mutating shared defaults. See
[`TEST-DATA-AND-ENVIRONMENTS.md`](TEST-DATA-AND-ENVIRONMENTS.md).

## Validate by blast radius

1. Run the changed test at the narrowest useful scope.
2. Run its project-defined area/pack when nearby or shared behaviour could be affected.
3. Widen further when shared harness or product code changed.

A new run after an invalid environment is a fresh, recorded run. Repeating a failed assertion
until it passes is masking, not validation.

## Authoring checklist

- [ ] The protected contract and test level are explicit.
- [ ] The test makes one coherent claim and does not duplicate cheaper equivalent coverage.
- [ ] Contract-relevant detail is precise; incidental mechanics stay below the chosen boundary.
- [ ] Existing abstractions were searched and reused only where their semantics fit.
- [ ] Preconditions use an appropriate layer and shared defaults remain immutable.
- [ ] Assertions use authoritative practical evidence and report observed values.
- [ ] Validation scope matches the change's blast radius.
