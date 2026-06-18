# Architecture Diagram

This repository is a multi-module Spring Boot sample application suite that demonstrates progressively richer Spring HATEOAS patterns. The modules share a small commons library and pair REST controllers with JPA-backed entities, Spring Data repositories, and hypermedia assemblers.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        Browser["Browser or API Client"]
        Traverson["Traverson Clients"]
    end
    subgraph Apps["Application Layer - Spring Boot 2.3.4"]
        Basics["Basics and Simplified Modules"]
        Hypermedia["Hypermedia Module"]
        Affordances["Affordances Module HAL FORMS"]
        Evolution["API Evolution Clients and Servers"]
        Orders["Spring Data REST Orders Module"]
        Commons["Commons Assembler Library"]
    end
    subgraph Data["Data Layer"]
        SpringData["Spring Data JPA Repositories"]
        H2[("H2 In Memory Database")]
    end
    subgraph External["External Services"]
        None["No external services configured"]
    end

    Browser -->|"HTTP HAL requests"| Basics
    Browser -->|"HTTP HAL requests"| Hypermedia
    Browser -->|"HTTP HAL FORMS requests"| Affordances
    Browser -->|"HTTP REST requests"| Orders
    Traverson -->|"link relation traversal"| Evolution
    Basics -->|"shared assembler base"| Commons
    Hypermedia -->|"shared assembler base"| Commons
    Affordances -->|"shared assembler base"| Commons
    Evolution -->|"representation assembly"| Commons
    Basics -->|"CRUD and reads"| SpringData
    Hypermedia -->|"employee and manager queries"| SpringData
    Affordances -->|"CRUD operations"| SpringData
    Evolution -->|"employee persistence"| SpringData
    Orders -->|"order state transitions"| SpringData
    SpringData -->|"JPA persistence"| H2
    Apps -->|"none"| None
```

### Technology Stack Summary

| Layer | Technology | Version | Purpose |
|---|---|---:|---|
| Client | Browser plus Traverson | N/A | Exercises hypermedia APIs and demonstrates link-driven navigation |
| Application | Spring Boot | 2.3.4.RELEASE | Hosts the sample applications and auto-configures web plus JPA features |
| Hypermedia | Spring HATEOAS | via Spring Boot 2.3.4 | Produces HAL and HAL FORMS representations and link relations |
| Data Access | Spring Data JPA | via Spring Boot 2.3.4 | Repository abstraction for Employee, Manager, and Order persistence |
| Database | H2 | managed by Spring Boot | In-memory relational datastore for all example modules |
| Shared Library | commons module | repository local | Centralizes reusable representation assembler behavior |

### Data Storage & External Services

All runnable modules persist sample data in an embedded H2 database through Spring Data JPA repositories. The repository does not integrate with external APIs, queues, caches, or managed data services; the only networked interaction is the internal api-evolution client modules calling the companion server modules over HTTP.

### Key Architectural Decisions

- The repository is organized as independent example modules so each HATEOAS pattern can be demonstrated in isolation while reusing the shared commons assembler base.
- Hypermedia construction is centralized in representation model assemblers and processors instead of controller methods emitting raw links inline.
- The api-evolution and Spring Data REST modules demonstrate backward compatibility and state-driven affordances as architectural patterns, not just CRUD endpoints.

## Component Relationships

```mermaid
flowchart LR
    subgraph Presentation["Presentation"]
        RootCtrl["RootController"]
        EmpCtrl["EmployeeController variants"]
        MgrCtrl["ManagerController"]
        SupCtrl["SupervisorController"]
        HomeCtrl["HomeController clients"]
        OrderCtrl["CustomOrderController"]
    end
    subgraph Business["Business Logic"]
        EmpAsm["Employee assemblers"]
        MgrAsm["Manager assembler"]
        EmpMgrAsm["EmployeeWithManager assembler"]
        OrderProc["OrderProcessor"]
        StatusRule["OrderStatus rules"]
    end
    subgraph DataAccess["Data Access"]
        EmpRepo["EmployeeRepository"]
        MgrRepo["ManagerRepository"]
        OrderRepo["OrderRepository"]
        Entities["Employee Manager Order entities"]
    end
    subgraph Infra["Infrastructure"]
        DbLoad["DatabaseLoader and InitDatabase"]
        HyperCfg["HypermediaConfiguration"]
        Commons["SimpleIdentifiableRepresentationModelAssembler"]
    end

    RootCtrl -->|"navigation links"| EmpAsm
    EmpCtrl -->|"delegates representation"| EmpAsm
    EmpCtrl -->|"detailed views"| EmpMgrAsm
    MgrCtrl -->|"delegates representation"| MgrAsm
    SupCtrl -->|"legacy wrapper"| MgrRepo
    HomeCtrl -->|"follows links"| EmpCtrl
    OrderCtrl -->|"validates transitions"| StatusRule
    OrderCtrl -->|"updates orders"| OrderRepo
    OrderProc -->|"adds state links"| StatusRule
    EmpAsm -->|"uses base behavior"| Commons
    MgrAsm -->|"uses base behavior"| Commons
    EmpMgrAsm -->|"combines employee and manager"| MgrRepo
    EmpCtrl -->|"queries"| EmpRepo
    EmpCtrl -->|"lookups"| MgrRepo
    MgrCtrl -->|"queries"| MgrRepo
    EmpRepo -->|"persists"| Entities
    MgrRepo -->|"persists"| Entities
    OrderRepo -->|"persists"| Entities
    DbLoad -.->|"seeds sample data"| EmpRepo
    DbLoad -.->|"seeds sample data"| MgrRepo
    DbLoad -.->|"seeds sample data"| OrderRepo
    HyperCfg -.->|"enables HAL FORMS"| EmpCtrl
    OrderProc -.->|"intercepts representations"| OrderCtrl
```

### Component Inventory

| Component | Layer | Type | Responsibility |
|---|---|---|---|
| RootController | Presentation | REST Controller | Exposes the top-level discovery document for the hypermedia sample |
| EmployeeController variants | Presentation | REST Controller | Serve employee collection, item, and update workflows across modules |
| ManagerController | Presentation | REST Controller | Exposes manager resources and employee-to-manager navigation |
| SupervisorController | Presentation | REST Controller | Preserves a legacy supervisor representation for compatibility |
| HomeController clients | Presentation | MVC Controller | Uses Traverson to consume server-side hypermedia APIs from the client modules |
| CustomOrderController | Presentation | BasePathAwareController | Handles explicit pay, cancel, and fulfill transitions for orders |
| Employee assemblers | Business Logic | Representation Assembler | Add self, collection, detailed, and related-resource links |
| OrderProcessor | Business Logic | RepresentationModelProcessor | Adds transition links based on current order state |
| OrderStatus rules | Business Logic | Enum rule set | Encodes valid order lifecycle transitions |
| EmployeeRepository | Data Access | CrudRepository | Persists and queries Employee entities |
| ManagerRepository | Data Access | CrudRepository | Persists and queries Manager entities |
| OrderRepository | Data Access | PagingAndSortingRepository | Persists and exposes Order entities through Spring Data REST |
| DatabaseLoader and InitDatabase | Infrastructure | Startup seeders | Populate the in-memory database with sample records on startup |
| HypermediaConfiguration | Infrastructure | Configuration | Turns on HAL FORMS support for the affordances sample |
| SimpleIdentifiableRepresentationModelAssembler | Infrastructure | Shared base class | Provides reusable self and collection link assembly logic |
