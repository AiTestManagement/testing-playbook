# Changelog

All notable changes to this project will be documented here.

The project uses [Semantic Versioning](https://semver.org/).

## [0.2.0] - 2026-10-14

### Changed

- Renamed the project and public repository from **test-harness** to **Testing Playbook**.
- Renamed the installed folder from `test-harness/` to `testing-playbook/` and its front door
  from `TEST-HARNESS.md` to `TESTING-PLAYBOOK.md`.
- Updated installation instructions, prompts, links, release assets, and publishing guidance to
  use the new identity.

### Migration

- Rename an existing installed folder and front door in place to preserve project-specific
  customisations, then merge the v0.2.0 upstream text changes.
- Replace the complete Testing Playbook snippet in the host project's agent instructions and
  search its documentation, CI, and saved prompts for old product paths.
- Do not rerun `SETUP.md` solely because of the rename.

## [0.1.1] - 2026-08-15

### Added

- Copy-paste prompts for each playbook area in the repository README and installed
  `TEST-HARNESS.md` front door.

### Changed

- Repeat configuration now checks existing setup state, preserves valid completed areas, and
  changes only unresolved or demonstrably stale content.

## [0.1.0] - 2026-08-14

### Added

- Initial public release of the portable `test-harness/` playbook.
- Guides for setup, authoring, data and environments, execution, diagnostics, recurring
  failure patterns, reusable test patterns, and known issues.
- Core and behavioural/integration/API/UI Definitions of Done.
- Explicit setup markers, result classification, anti-masking policy, and playbook
  maintenance checks.

[0.2.0]: https://github.com/AiTestManagement/testing-playbook/compare/v0.1.1...v0.2.0
[0.1.1]: https://github.com/AiTestManagement/testing-playbook/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/AiTestManagement/testing-playbook/releases/tag/v0.1.0
