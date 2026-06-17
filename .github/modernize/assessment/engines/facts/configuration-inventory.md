# Configuration & Externalized Settings Inventory

This project has a minimal configuration footprint — only three modules declare explicit `application.yml` files, with all other modules relying entirely on Spring Boot auto-configuration defaults. There are no runtime profiles, external config servers, or secret stores.

## Configuration Sources

| Source | Type | Path / Location | Notes |
|--------|------|----------------|-------|
| application.yml | YAML config | api-evolution/original-server/src/main/resources/application.yml | Sets server.port=9000 |
| application.yml | YAML config | api-evolution/new-server/src/main/resources/application.yml | Sets server.port=9000 |
| application.yml | YAML config | spring-hateoas-and-spring-data-rest/src/main/resources/application.yml | Sets spring.data.rest.base-path=/api and server.port=9000 |
| Spring Boot auto-configuration | Built-in defaults | N/A | All other modules (basics, hypermedia, affordances, simplified) rely fully on auto-config defaults |
| pom.xml | Maven build config | pom.xml (root) | Parent POM; declares java.version, evo.version, module list, spring52-next build profile |
| maven-wrapper.properties | Build tool | .mvn/wrapper/maven-wrapper.properties | Pins Maven 3.5.0 via Maven Wrapper |

No external config server (Spring Cloud Config, Azure App Configuration, AWS AppConfig, Consul KV) is used. No Kubernetes ConfigMaps, Docker Compose environment sections, or secret stores (Vault, KeyVault, Secrets Manager) are referenced.

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---------|-----------|---------|--------------------------|
| (default) | Automatic — active always | Standard build with all declared dependencies | spring-boot-starter-hateoas, spring-boot-starter-data-jpa, H2, Lombok, Evo Inflector, spring-boot-devtools, spring-boot-starter-test |
| spring52-next | Manual — `-Pspring52-next` | Overrides Spring Framework version to 5.2.6.BUILD-SNAPSHOT for bleeding-edge compatibility testing | Adds spring-libs-snapshot repository; overrides spring.version property |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---------|-----------------|-------------|--------------|
| (default) | Active when no explicit profile is set | Spring Boot auto-config defaults | All modules run against embedded H2 in-memory database |
| (none defined) | N/A | N/A | No `application-dev.yml`, `application-prod.yml`, or `@Profile`-annotated beans are present in any module |

No runtime profiles are defined. All configuration is either in the default `application.yml` or in Spring Boot auto-configuration. There is no `spring.profiles.active` setting in any configuration file.

## Properties Inventory

### api-evolution/original-server

| Property Key | Value | Profile | Source |
|-------------|-------|---------|--------|
| server.port | 9000 | default | application.yml |

### api-evolution/new-server

| Property Key | Value | Profile | Source |
|-------------|-------|---------|--------|
| server.port | 9000 | default | application.yml |

### spring-hateoas-and-spring-data-rest

| Property Key | Value | Profile | Source |
|-------------|-------|---------|--------|
| spring.data.rest.base-path | /api | default | application.yml |
| server.port | 9000 | default | application.yml |

### All other modules (basics, hypermedia, affordances, simplified)

| Property Key | Value | Profile | Source |
|-------------|-------|---------|--------|
| server.port | 8080 | default | Spring Boot auto-config default |
| spring.datasource.url | jdbc:h2:mem:testdb | default | Spring Boot H2 auto-config default |
| spring.jpa.hibernate.ddl-auto | create-drop | default | Spring Boot H2 auto-config default |
| spring.h2.console.enabled | false | default | Spring Boot auto-config default |

No properties are sourced from environment variables. No placeholder references (`${ENV_VAR}`) are present in any configuration file.

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---------|-------------------|--------|---------------|
| All modules | None specified (JVM defaults) | Not configured | 1 (standalone Spring Boot jar) |

No `-Xms`/`-Xmx` heap settings, no Docker `mem_limit`, no Kubernetes resource requests/limits, and no scaling configuration are defined. All modules run as standalone Spring Boot JARs with default JVM settings.

## Startup Dependency Chain

There are no automated startup dependency mechanisms (Kubernetes readiness probes, `dockerize`, Docker Compose `depends_on` with health checks, or Spring Cloud Config retry) configured for any module.

The api-evolution client modules (`original-client`, `new-client`) make HTTP calls to their respective servers at `http://localhost:9000` on the first user request. If the server is not already running, the first request will fail with a connection error. There is no built-in wait or retry mechanism.

Recommended startup order for the api-evolution pair:
1. Start `api-evolution/original-server` (port 9000)
2. Start `api-evolution/original-client` (port 8080)

Or for the evolved pair:
1. Start `api-evolution/new-server` (port 9000)
2. Start `api-evolution/new-client` (port 8080)

All other modules (basics, hypermedia, affordances, simplified, spring-data-rest) are fully self-contained and have no startup dependencies.

## Secrets & Sensitive Configuration

No secrets or sensitive configuration values are present in any configuration file. There are no database passwords (H2 in-memory requires no credentials), no API keys, no OAuth2 client secrets, no connection strings with credentials, and no external secret store references.

| Secret Reference | Type | Storage |
|----------------|------|---------|
| (none detected) | — | — |

### Secrets Provisioning Workflow

No secrets provisioning workflow exists. The project uses H2 in-memory databases that require no authentication credentials. No external services requiring API keys, tokens, or connection strings are integrated. No secret manager, vault, or encrypted property mechanism is needed or configured.

## Feature Flags

No feature flag framework (LaunchDarkly, Unleash, Spring Feature Flags, .NET FeatureManagement) is used. No `@ConditionalOnProperty` or `@ConditionalOnExpression` beans that act as feature toggles are present. The `spring52-next` Maven build profile is the only mechanism for toggling behavior (at build time, not runtime).

| Flag Name | Default | Controlled By |
|-----------|---------|--------------|
| (none detected) | — | — |

## Framework & Runtime Versions

| Component | Version | Source |
|-----------|---------|--------|
| Spring Boot | 2.3.4.RELEASE | pom.xml parent BOM |
| Spring Framework | 5.2.x (Boot-managed) | spring-boot-starter-parent BOM |
| Spring HATEOAS | Boot-managed | spring-boot-starter-hateoas |
| Spring Data JPA | Boot-managed | spring-boot-starter-data-jpa |
| Spring Data REST | Boot-managed | spring-boot-starter-data-rest (spring-data-rest module only) |
| Hibernate ORM | Boot-managed | spring-boot-starter-data-jpa |
| H2 Database | Boot-managed | com.h2database:h2 |
| Lombok | Boot-managed | org.projectlombok:lombok |
| Evo Inflector | 1.2.2 | pom.xml (explicit version) |
| Jackson Databind | Boot-managed | transitive via spring-boot-starter-hateoas |
| Java (source/target) | 1.8 | pom.xml java.version property |
| Maven | 3.5.0 | .mvn/wrapper/maven-wrapper.properties |
| Maven Wrapper | 3.5.0 | .mvn/wrapper/maven-wrapper.properties |

No Docker base images, Kubernetes manifests, or container configurations are present in this repository. All applications are run as standard executable Spring Boot JARs.
