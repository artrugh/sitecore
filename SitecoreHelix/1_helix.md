## Helix

Helix is a set of **recommended practices** and **convetions** for the **solution architecture** of Sitecore implementations, that help developers to build solutions that are adaptable and easily to maintain.

It is based on the principle of modular architecture (package design).

Helix offers a framework that describes how you can isolate domain logic and better ensure that an implementation or solution remains durable.

It reduces the amount of technical debt that tends to develop in large solutions over time.

### Principles

Sitecore Heliz is specifically based on the "Priciples of Package and Component Design".

#### Cohesion (Boundering) and Coupling (Interrelation)

Package Cohesion:
    - What defines a module?
    - How do you make modules manageable?

Package Coupling:
    - How do the modules connect?
    - How do you control the dependencies of your solution?

##### Cohesion Principles

- The reuse-release equivalence
    - All classes in a reusable module should be reusable by the same audience.
    - You should consider the content of a module from the point of view of potential consumers.
- The common reuse
    - Classes that are tightly bound to each other with class relationships should be in the same module.
- The common Closure
    - A change that affects a module affects all the classes in that module and no other module.
    - Single-Responsibility Principle, module should only have one reason to change.

##### Coupling Principles

- The acyclic Dependencies
    - There should not be circular dependencies between modules.
- The Stable dependency
    - The importance of conforming to the common-closure principle:
        - Modules are created that are sensitive to certain kinds of change.
        - any module that is volatile should not be dependend on by a module that is difficult to change.
    - Use stability metrics based on the number of dependecies entering and leaving a module.
- Stable Abstractions
    - A stable module should be abstract so its stabilitydoes not prevent it from being extended.
    - An unstable module should be concrete since its instability allows the concrete code inside to be easily changed.

### Terminology

| Term | Description |
| -- | -- |
| Dependency | how a feature and functionality in the solutioln relate to each other |
| Implementation or Solution | total number of modules, features, and functionalities developed and deployed to solve a customer's businnes problem |
| Module | Conceptual grouping of assets that relates to a particular business requirement |
| Solution | It can refer for Implementation or to the Visual Studio Solution |
| Stability | the number of its incoming and outgoing dependencies. The more external dependencies a module has, the more stable it must be |


### High Cohesion and low Coupling

High Cohesion means: to break down into the right number of aprts with the logic biding them together.

Low Cohesion means to keep the number of dependencies between different parts down to the absolute minimum.

This approach reduces the amount of efford spent on stability and testing.

### Dependencies

- Explicit: using in C#
- Implicit: references to sitecore fields by name.

Avoid implicit dependencies and ensure explicit ones.

### Layers

They ensure a **clear flow for dependencies** throughout the solution (coupling), between the unstable and stable modules and the direction of relationships.

They are not only conceptual constructs in the architecture, they are aldso physically described in the implementation folders in the filesystem, Visual Studio, and Sitecore, as well as in places such as namespaces.

A Sitecore solution based on the Helix principles will typically have its modules laid out in three layers: 

1. Foundation
2. Feature
3. Project

Dependencies between modules in these layers flow in only one direction. Projects (Concrete context) => Feature (Concrete features) => Foundation (Abstract)

#### Project layer

- It is a composition layer where Feature modules are aggregated and integrated.
- It provides the context of solution, meaning the actual cohesive website or channel output from the implementation, including the page type, layout, or graphical design.
- It typically contains few modules and is determined by number of tenants or sites.

#### Feature layer

- It contains concrete features of the solution as understood by the business owners. It also implement the business capabilities (News, Articles, Promotions, or Search).
- It is based on the concept of *functionality over technology*.
- The classes in the Feature layer should be closed together against the same kinds of changes.

#### Foundation layer

- It is the lowest lavel in Helix.
- There are two types: Templates:
    - Technology-specific: These modules are tied to a a specific technology.
        - Ex: indexing shared between search and other modules.
    - Solution-domain-specific: These modules cover solution-wide responsability. They might also share functionality between feature modules that are abstracted out into separate frameworks.
        - Ex: shared customer business logic.
- One Foundation layer module can depend on another in the solution, as long as they don't create a dependency cycle.

### Modules

Modules define the isolation of feature and functionality. Modules should be business-centric.
It means that they relate to business objectives and are grouped together with multiple technology entities that refer to the relevant objective.

Principles:

- Single Responsability
- Module names: they should reflect the business domain (things that change together) responsability
- Stability metrics: Based on the number of dependencies entering and leaving a module.
- Stable Modules:
    - Stable module should be abstract, so that their stability does not prevent them from being extended.
    - Unstable modules should be concrete since their instability allows the specific code inside to be easily changed.


#### Conventions

- A module can consist of one or more Visual Studio projects.
- Manage all module files in a single folder on a disk.
    - serialize all modules definition items below the same folder.
- In Sitecore, code, views, config files, templates, and renderings are referred to as objects. Objects aer divided by their type, and a module in Sitecore contains everything related to the module's responsability.
    - structuring a module to make it easy to maintain can be done by grouping objects that change together.

##### Responsability

- If a responsability changes, it will cause a change in all objects that are related to that reponsability.
- Responsabilities originate from requirement.
- Responsabilities evolve during development.
- The name of module should always clearly indicate its responsability.

Projects responsability: Particular context.
Feature responsability: Concrete business-domain.
Foundation responsability: one abstract business domain or technical responsability(authentication or indexing).

- Change or removing a Feature layer module never impacts other Feature or Foundation. It can only has a potential impact on Project layer modules.
- When responsability is shared between two features, abstract the shared responsability of a module in the Foundation layer.
- A change that affects a module affects all the objects in that module and no other modules.

Avoid:

- Atom design
- Naming by technology or type
- Vague names



