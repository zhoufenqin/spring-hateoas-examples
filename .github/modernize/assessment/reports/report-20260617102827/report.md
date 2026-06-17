# spring-hateoas-examples

## Summary

| Metric | Value |
|--------|-------|
| Total Issues | 5 |
| Mandatory Blockers | 4 |
| Potential Issues | 0 |

## Component Information

| Property | Value |
|----------|-------|
| Language | Java, Python |
| Frameworks | Spring Boot, Spring |
| Build tools | Maven |
| JDK version | 1.8 |

## Cloud Readiness Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| Use of unsecured network protocols or URI libraries | Mandatory | 3 | [34](#Use_of_unsecured_network_protocols_or_URI_libraries) |
| Local HTTP Calls | Mandatory | 3 | [34](#Local_HTTP_Calls) |
| No Dockerfile found | Mandatory | 3 | 1 |
| Avoid using hardcoded URLs (HTTP protocol) in source code | Optional | 3 | [34](#Avoid_using_hardcoded_URLs_HTTP_protocol_in_source_code) |

### Issue Details

<details id="Use_of_unsecured_network_protocols_or_URI_libraries">
<summary><b>Use of unsecured network protocols or URI libraries</b> — affected files</summary>

- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 50)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 51)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 58)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 59)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 60)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 61)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 64)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 65)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 66)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 67)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 68)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 69)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 112)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 113)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 114)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 72)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 84)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 85)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 93)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 117)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 118)`
- `api-evolution/new-client/src/main/java/org/springframework/hateoas/examples/HomeController.java (line 43)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 67)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 68)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 74)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 75)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 65)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 66)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 71)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 72)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`
- `api-evolution/original-client/src/main/java/org/springframework/hateoas/examples/HomeController.java (line 43)`

</details>

<details id="Local_HTTP_Calls">
<summary><b>Local HTTP Calls</b> — affected files</summary>

- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 50)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 51)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 58)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 59)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 60)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 61)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 64)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 65)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 66)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 67)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 68)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 69)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 112)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 113)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 114)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 72)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 84)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 85)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 93)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 117)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 118)`
- `api-evolution/new-client/src/main/java/org/springframework/hateoas/examples/HomeController.java (line 43)`
- `api-evolution/original-client/src/main/java/org/springframework/hateoas/examples/HomeController.java (line 43)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 67)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 68)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 74)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 75)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 65)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 66)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 71)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 72)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`

</details>

<details id="Avoid_using_hardcoded_URLs_HTTP_protocol_in_source_code">
<summary><b>Avoid using hardcoded URLs (HTTP protocol) in source code</b> — affected files</summary>

- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 50)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 51)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 58)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 59)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 60)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 61)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 64)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 65)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 66)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 67)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 68)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 69)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 112)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 113)`
- `spring-hateoas-and-spring-data-rest/src/test/java/org/springframework/hateoas/examples/OrderIntegrationTest.java (line 114)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 72)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 84)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 85)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 93)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 117)`
- `affordances/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 118)`
- `api-evolution/new-client/src/main/java/org/springframework/hateoas/examples/HomeController.java (line 43)`
- `api-evolution/original-client/src/main/java/org/springframework/hateoas/examples/HomeController.java (line 43)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 65)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 66)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 71)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 72)`
- `simplified/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 67)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 68)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 73)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 74)`
- `basics/src/test/java/org/springframework/hateoas/examples/EmployeeControllerTests.java (line 75)`

</details>

## Upgrade Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| Java Version Has Reached the End of Support | Mandatory | 8 | [1](#Java_Version_Has_Reached_the_End_of_Support) |

### Issue Details

<details id="Java_Version_Has_Reached_the_End_of_Support">
<summary><b>Java Version Has Reached the End of Support</b> — affected files</summary>

- `pom.xml (line 73)`

</details>

---

## Codebase Insights

> **Note:** These documents are generated by AI and may contain inaccuracies or incomplete information. Please review carefully.

1. **[Architecture Diagram](facts/architecture-diagram.md)** — Understand the big picture: system layers and component relationships
2. **[Dependency Map](facts/dependency-map.md)** — Know what the project depends on and where the risks are
3. **[API & Service Contracts](facts/api-service-contracts.md)** — See how services communicate and what contracts they expose
4. **[Data Architecture](facts/data-architecture.md)** — Explore data models, storage, and data flow patterns
5. **[Configuration Inventory](facts/configuration-inventory.md)** — Review how the application is configured across environments
6. **[Business Workflows](facts/business-workflows.md)** — Trace end-to-end business processes and domain logic

[Share feedback](https://aka.ms/ghcp-appmod/feedback)
