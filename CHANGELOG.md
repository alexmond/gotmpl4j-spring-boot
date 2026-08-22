# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions **track the Spring Boot release** this project builds against, as
`<boot-version>.<revision>` — see [Versioning](README.md#versioning--one-branch-per-spring-boot-line).

## [Unreleased]

## [4.0.8.1] - 2026-08-22

Spring Boot **4.0.8** line (branch `4.0`).

### Added

- Initial release from the dedicated `gotmpl4j-spring-boot` repository, for applications
  still on the Spring Boot 4.0 line. `gotmpl4j-spring` and `gotmpl4j-spring-boot-starter` were
  split out of the `gotmpl4j` monorepo; commit history is preserved.
- Per-Boot-line branch layout; this is the `4.0` maintenance branch (`main` tracks Boot 4.1).

### Changed

- Spring Boot **4.0.7 → 4.0.8** (patch bump within the 4.0 line).

[Unreleased]: https://github.com/alexmond/gotmpl4j-spring-boot/compare/4.0.8.1...4.0
[4.0.8.1]: https://github.com/alexmond/gotmpl4j-spring-boot/releases/tag/4.0.8.1
