# gotmpl4j-spring-boot

[![Maven Central](https://img.shields.io/maven-central/v/org.alexmond/gotmpl4j-spring-boot-starter.svg?label=Maven%20Central)](https://central.sonatype.com/artifact/org.alexmond/gotmpl4j-spring-boot-starter)
[![Javadoc](https://img.shields.io/badge/Javadoc-API-blue)](https://javadoc.io/doc/org.alexmond/gotmpl4j-spring-boot-starter)
[![Build](https://img.shields.io/github/actions/workflow/status/alexmond/gotmpl4j-spring-boot/maven.yml?branch=main)](https://github.com/alexmond/gotmpl4j-spring-boot/actions)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-17%2B-blue.svg)](https://openjdk.org/)

Spring Boot integration for [gotmpl4j](https://github.com/alexmond/gotmpl4j) — the pure-Java
implementation of Go's [`text/template`](https://pkg.go.dev/text/template) engine. Render the
same templates Helm, Hugo, and countless Go CLIs use, straight from a Spring Boot app.

📖 **Documentation:** <https://www.alexmond.org/gotmpl4j-spring-boot/current/index.html>

## Modules

| Artifact | Description |
|---|---|
| `org.alexmond:gotmpl4j-spring-boot-starter` | Spring Boot auto-configuration: a ready-to-inject template engine, configuration properties, a compile cache, function beans, and optional MVC / WebFlux `ViewResolver`s. |
| `org.alexmond:gotmpl4j-spring` | Spring-context template functions — `msg` (i18n), `env` (config), `bean`, and Spring Security (`hasRole`/`isAuthenticated`/…) plus web (`param`/`csrf`/…) helpers. Auto-configured; ships with the starter. |

The Spring-free engine itself — `gotmpl4j-core` and `gotmpl4j-sprig` — lives in the separate
[**gotmpl4j**](https://github.com/alexmond/gotmpl4j) repository and is consumed here as a
released dependency.

## Versioning — one branch per Spring Boot line

The artifact version **tracks the Spring Boot release it builds against**, as
`<boot-version>.<revision>`. `main` always tracks the newest Spring Boot release; older lines
get their own maintenance branch.

| Branch | Spring Boot | Version |
|---|---|---|
| `main` | 4.1.x | `4.1.1.1` |
| `4.0`  | 4.0.x | `4.0.8.1` |

Pick the version matching your application's Boot line. The engine dependency
(`gotmpl4j-core` / `-sprig`, plain semver) is the same across lines.

> **Moved here in 2026-08:** these two artifacts were previously released from the `gotmpl4j`
> monorepo on plain semver (up to `1.3.0`). The coordinates are unchanged — only the version
> scheme moved to Boot-tracking, so `4.1.1.1` / `4.0.8.1` supersede `1.3.0` for these two
> artifacts.

## Quick start

```xml
<dependency>
    <groupId>org.alexmond</groupId>
    <artifactId>gotmpl4j-spring-boot-starter</artifactId>
    <version>4.1.1.1</version>
</dependency>
```

```java
@Service
class GreetingService {

    private final GoTemplateService templates;

    GreetingService(GoTemplateService templates) {
        this.templates = templates;
    }

    String greet(String name) {
        return templates.render("greeting", Map.of("name", name));
    }
}
```

Add `org.alexmond:gotmpl4j-sprig` alongside the starter to make the Sprig function library
available inside your templates.

## Samples

Runnable examples under `gotmpl4j-samples/` (built by the `default` profile, never published):

| Sample | Shows |
|---|---|
| `web-mvc` | A Spring MVC controller returning a view name, rendered by the servlet `ViewResolver`. |
| `web-flux` | The same for WebFlux, via the reactive `ViewResolver`. |
| `spring-context` | `msg`/`env` plus the security and web functions, varying by role and locale. |

```bash
./mvnw -pl gotmpl4j-samples/web-mvc -am spring-boot:run -Pdefault
```

## Build

```bash
./mvnw clean install -Pdefault   # build + test + format/PMD/checkstyle gates + samples
./mvnw test                      # tests only
```

Requires JDK 17.

## License

Apache License 2.0 — see [LICENSE](LICENSE).
