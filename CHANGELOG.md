# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions **track the Spring Boot release** this project builds against, as
`<boot-version>.<revision>` — see [Versioning](README.md#versioning--one-branch-per-spring-boot-line).

## [Unreleased]

## [4.1.1.1] - 2026-08-22

Spring Boot **4.1.1** line (branch `main`).

### Added

- Initial release from the dedicated `gotmpl4j-spring-boot` repository. `gotmpl4j-spring` and
  `gotmpl4j-spring-boot-starter` were split out of the `gotmpl4j` monorepo so the Spring
  integration can be released per Spring Boot line while the engine keeps plain semver.
  Commit history for both modules is preserved.
- Per-Boot-line branch layout: `main` tracks the newest Spring Boot release, with a
  `<major>.<minor>` maintenance branch per older maintained line.

### Changed

- Spring Boot **4.0.7 → 4.1.1**. No source changes were required; all 52 tests pass unchanged.
- Version scheme for these two artifacts: plain semver (`1.3.0` and earlier, released from the
  monorepo) → Boot-tracking `4.1.1.1`. Coordinates (`org.alexmond:gotmpl4j-spring`,
  `org.alexmond:gotmpl4j-spring-boot-starter`) are unchanged.
- The engine (`gotmpl4j-core`, `gotmpl4j-sprig`) is now an external released dependency rather
  than a reactor sibling.

## [4.0.8.1] - 2026-08-22

Spring Boot **4.0.8** line (branch `4.0`).

### Added

- Same split-out as `4.1.1.1`, for applications still on the Spring Boot 4.0 line.

### Changed

- Spring Boot **4.0.7 → 4.0.8** (patch bump within the 4.0 line).

[Unreleased]: https://github.com/alexmond/gotmpl4j-spring-boot/compare/4.1.1.1...HEAD
[4.1.1.1]: https://github.com/alexmond/gotmpl4j-spring-boot/releases/tag/4.1.1.1
[4.0.8.1]: https://github.com/alexmond/gotmpl4j-spring-boot/releases/tag/4.0.8.1
