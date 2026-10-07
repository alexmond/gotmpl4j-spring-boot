# CLAUDE.md — gotmpl4j-spring-boot

## What this is

The **Spring Boot integration** for [gotmpl4j](https://github.com/alexmond/gotmpl4j) (the
pure-Java Go `text/template` engine). Split out of the gotmpl4j monorepo in 2026-08 so the
Spring half can be released **per Spring Boot line** while the engine keeps plain semver.

**Tech stack:** Java 17, Spring Boot, Maven. Published to Maven Central.

## Modules

```
gotmpl4j-spring-boot-parent (pom)
├── gotmpl4j-spring                — Spring-context functions: msg/env/bean + security/web helpers
├── gotmpl4j-spring-boot-starter   — auto-config, GoTemplateService, compile cache, MVC/WebFlux ViewResolvers
└── gotmpl4j-samples               — runnable examples (default profile only, never published)
    ├── web-mvc  ├── web-flux  └── spring-context
```

The engine (`gotmpl4j-core`, `gotmpl4j-sprig`) is an **external released dependency**, pinned by
the `gotmpl4j.version` property in the root POM — never a reactor sibling. Do not vendor engine
code here; fix engine bugs in the gotmpl4j repo and bump the pin.

## Versioning & branches — per Spring Boot line

This repo follows the sibling Boot-extension standard (`spring-boot-config-json-schema`,
`spring-boot-actuator-extensions`):

- **Version = `<boot-version>.<revision>`** (e.g. `4.1.1.1` on Boot 4.1.1). The revision starts
  at **1** and advances for repo-only changes on the same Boot version.
- **`main` is always the latest Spring Boot line.** Maintenance branches are named
  `<major>.<minor>` (currently `4.0`).
- When `main` moves to a new Boot **minor** (4.1 → 4.2), cut the outgoing line to its own
  `<major>.<minor>` branch **first**, from the pre-bump head. Every Boot minor gets a branch,
  not only a new major.
- A fix that applies to every line goes to each branch, one PR each.

Use the **`boot-upgrade` skill** to survey branches vs the latest Boot patch and drive bumps.

## Build & test

```bash
./mvnw clean install -Pdefault   # build + test + spring-javaformat + PMD + checkstyle + samples
./mvnw test                      # tests only
./mvnw spring-javaformat:apply   # auto-format (tabs)
```

JDK 17. `-Pdefault` adds the sample apps — CI uses it, so a sample that stops compiling is a
red build.

> **`versions:set` must be run with `-Pdefault`**, or the sample modules keep a stale parent
> version and the next build breaks. The release workflow already does this.

## Coding standards

- Tabs (enforced by spring-javaformat). Run `spring-javaformat:apply` before committing.
- Java 17 only — **no Java 21 features** (no pattern-matching `switch`, no `SequencedCollection`).
- Imports, never inline FQNs (PMD `UnnecessaryFullyQualifiedName`).
- `@code true`/`@code false` in Javadoc; `Locale.ROOT` on case conversions; `.append('c')` for
  single chars. File ≤800 lines, method ≤80 (checkstyle).

## Releasing

**Before triggering a release, run the `release-prep` skill.** The Maven release only runs
`versions:set` on the POMs — it does not touch the README version table or the docs.

`.github/workflows/maven_release.yml` (manual dispatch) takes `branch` / `releaseVersion` /
`nextVersion`: it sets the version, builds, deploys to Maven Central via the `release` profile
(GPG sign + central-publishing-plugin), tags (**no `v` prefix**), and opens a GitHub release.
Release the current line **from `main`**; older lines from their `<major>.<minor>` branch.

After a release, run **`update-docs-hub`** — the hub lists this repo as one content source with
a `tags:` array holding **one tag per Boot line**, so a per-line release is an in-place swap of
that line's element (not a whole-list replace).

Secrets (`OSSRH_*`, `GPG_*`, `CODECOV_TOKEN`) are provisioned from infra via
`infra/scripts/gh-release-secrets.sh apply alexmond/gotmpl4j-spring-boot`.
