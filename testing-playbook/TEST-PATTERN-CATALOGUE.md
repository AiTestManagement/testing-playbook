<!-- PORTABLE TEMPLATE: a curated semantic map, not an exhaustive duplicate of source code. -->

# Test Pattern Catalogue

A curated index of high-value reusable entry points—fixtures, seeders, clients, builders, page
objects, and assertions. Search it and the code before writing. Keep it small enough to trust.

## Semantic-fit rule

- Reuse when intent, ownership, lifecycle, side effects, and failure semantics match.
- Do not add flags or widen an abstraction merely to eliminate local duplication.
- Small duplication is preferable to a misleading shared abstraction; extract once the stable
  repeated concept is clear.
- Link to the source of truth rather than reproducing implementation detail here.
- Before changing an entry, find its consumers and validate the blast radius.

## Entry format

| Intent / entry point | When to use—and not use | Source | Owner | Verified |
|---|---|---|---|---|

<!-- SETUP_REQUIRED: Replace this marker with real curated entries linked to source, or state that
the project has no catalogue entries yet. Do not retain neutral helpers that look real. -->

<!-- SETUP_OPTIONAL: Record how to search for consumers and how shared abstractions are reviewed. -->

<!-- GROWTH_POINT: Add a row only for a durable entry point that future authors otherwise would
struggle to discover or choose correctly. Review links and dates; prune stale rows. -->

## Adding or changing an entry

1. Confirm no semantically matching entry already exists.
2. Explain both its intended use and the nearest case where it should not be used.
3. Link a stable repository path or symbol and name an owner.
4. Run the direct test, affected area, and wider consumers as justified.
5. Add or update the verification date. The code remains authoritative if this index drifts.
