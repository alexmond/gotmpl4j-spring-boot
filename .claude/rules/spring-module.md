# Spring integration module rules

This repo is the **Spring Boot half** of gotmpl4j. The engine lives elsewhere.

- The engine (`gotmpl4j-core`, `gotmpl4j-sprig`) is an **external released dependency**, pinned
  by the `gotmpl4j.version` property in the root POM. Never vendor or fork engine code here —
  fix engine issues in https://github.com/alexmond/gotmpl4j and bump the pin.
- `gotmpl4j-spring` depends on `gotmpl4j-core` only (not on Sprig). The starter depends on
  core + sprig + `gotmpl4j-spring`.
- Function providers here register as **Spring beans** via
  `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`, at
  priority **300** — not via `META-INF/services` (that is Sprig's ServiceLoader path, priority
  100; Go builtins are 0). Keep both discovery paths independent.
- Every branch tracks one Spring Boot line; the project version is `<boot-version>.<revision>`.
  Never bump the Boot parent without also moving the project version and the README table.
- Java 17 only — the Boot 4.x lines keep the Java 17 baseline.
