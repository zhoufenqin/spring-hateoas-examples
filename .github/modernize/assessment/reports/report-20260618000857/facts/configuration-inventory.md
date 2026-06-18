# Configuration & Externalized Settings Inventory

The repository has a deliberately small configuration surface made up of Maven build metadata, a few Spring Boot YAML files, and CI scripting. There are no external config servers, secret stores, or complex environment overlays in the current sample applications.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| Parent Maven POM | Build configuration | `/pom.xml` | Defines modules, Java version, parent BOM, shared dependencies, and build plugins |
| API evolution original server YAML | Spring Boot runtime config | `/api-evolution/original-server/src/main/resources/application.yml` | Sets `server.port` to 9000 |
| API evolution new server YAML | Spring Boot runtime config | `/api-evolution/new-server/src/main/resources/application.yml` | Sets `server.port` to 9000 |
| Spring Data REST YAML | Spring Boot runtime config | `/spring-hateoas-and-spring-data-rest/src/main/resources/application.yml` | Sets Spring Data REST base path to `/api` |
| Maven wrapper properties | Tooling config | `/.mvn/wrapper/maven-wrapper.properties` | Pins Maven wrapper distribution |
| Jenkins pipeline | CI configuration | `/Jenkinsfile` | Defines multi-JDK build and test pipeline |
| Test shell script | CI helper | `/ci/test.sh` | Runs Maven clean, dependency list, and tests |
| Assessment config | Assessment configuration | `/.github/modernize/assessment/reports/assessment-config.yaml` | Sets target runtime, domains, and target compute services for AppCAT |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| spring52-next | Manual `-Pspring52-next` | Tests the examples against a Spring 5.2 snapshot line | Overrides `spring.version` and enables `spring-libs-snapshot` repository |
| default build | Automatic | Standard multi-module Maven build | Inherits Spring Boot parent, uses `maven-surefire-plugin` configuration |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| default | Spring Boot default startup | implicit defaults plus module `application.yml` where present | Embedded H2, default port 8080 unless overridden |
| api-evolution server runtime | Module startup | `api-evolution/original-server/application.yml`, `api-evolution/new-server/application.yml` | Overrides port to 9000 |
| spring-data-rest runtime | Module startup | `spring-hateoas-and-spring-data-rest/application.yml` | Sets base path to `/api` |

## Properties Inventory

### Shared Build and Assessment Properties

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `java.version` | `1.8` | all | `/pom.xml` |
| `evo.version` | `1.2.2` | all | `/pom.xml` |
| `analysisCoverage` | `full` | assessment only | `/.github/modernize/assessment/reports/assessment-config.yaml` |
| `java.targetRuntime` | `openjdk25` | assessment only | `/.github/modernize/assessment/reports/assessment-config.yaml` |
| `java.targetComputeServices` | `azure-aks` | assessment only | `/.github/modernize/assessment/reports/assessment-config.yaml` |
| `java.targetOS` | `linux`, `windows` | assessment only | `/.github/modernize/assessment/reports/assessment-config.yaml` |

### Module Runtime Properties

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `server.port` | `9000` | api-evolution original-server | `/api-evolution/original-server/src/main/resources/application.yml` |
| `server.port` | `9000` | api-evolution new-server | `/api-evolution/new-server/src/main/resources/application.yml` |
| `spring.data.rest.base-path` | `/api` | spring-hateoas-and-spring-data-rest | `/spring-hateoas-and-spring-data-rest/src/main/resources/application.yml` |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| All modules | No explicit JVM flags in repository sources | Not specified | 1 local sample instance expected |
| CI test runs | `MAVEN_OPTS=-Duser.name=jenkins -Duser.home=/tmp/jenkins-home` | Not specified | One Maven process per Jenkins stage |

## Startup Dependency Chain

1. Each Spring Boot sample starts independently and does not wait on external infrastructure because H2 is embedded and sample data is seeded locally.
2. The api-evolution client modules assume that their companion server module is already available on port 9000 before the client attempts Traverson navigation.
3. Jenkins CI runs the Maven wrapper through `ci/test.sh`; no additional health-check or orchestrated readiness logic is configured in the repository.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| None detected | N/A | N/A |

### Secrets Provisioning Workflow

No secrets provisioning workflow is defined. The repository does not reference environment-backed credentials, vault paths, secret managers, or encrypted property values; all current sample configuration is non-sensitive and local-development oriented.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| None detected | N/A | N/A |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Spring Boot parent | 2.3.4.RELEASE | `/pom.xml` |
| Java target | 1.8 | `/pom.xml` |
| Maven wrapper distribution | 3.5.0 | `/.mvn/wrapper/maven-wrapper.properties` |
| Spring Framework line | 5.2.x via Boot 2.3.4 | dependency management in `/pom.xml` |
| Evo Inflector | 1.2.2 | `/pom.xml` |
| CI JDK coverage | 8, 11, 13 | `/Jenkinsfile` |
