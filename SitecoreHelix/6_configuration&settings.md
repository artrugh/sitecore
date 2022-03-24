## Configuration and Settings

Configuration 
- it is aimed at **developers or IT system administration roles**.
- it is managed as part of the **development and deployment** outside Sitecore.

Settings 
- they are aimed at **user roles** such as editors or administrators.
- they are managed as **part of the content** in Sitecore.

They are defined in your implementation relate to a specific module and should therefore be managed and versioned with that module.

### Solution-wide

They cover the entire implementation and are defined **one time within a solution** with values that will affect the implementation as a whole.

Ex: web.config or in Sitecore all the installed languages and aliases defined under `/sitecore/system`.

### Context-wide

They cover a given context that is defined by the business logic in the module.
It is recommended, mostly for multisite, multitenant, or multilanguages.

### Value Scope

The value scope of a configuration or setting is the circumstance in which values change.

### Environment-scope values

They are associated with a solution-wide configurations and they change depending the environment. They are managed in .config files.

### Role-scoped Values

They are defined based on server roles in a multiserve implementation.

App_Config/Include/Sitecore.Publishing.DedicatedInstance.config.example file.

Role-scope values are typically restricted to IT/developer managed configurations.

### Implementation-scope Values

They are associated with the module that required them.
Most configurations within psitecore.config include implementation scoped files.

### Recommendations

Isolate the implementation-specific changes and additions, you are able to make upgrades much easier by easily identifying changes.

Keep changes and additions to configuration with the related business logic, will make it easier to identify the issues to resolve.

A configuration that relates to a module should be included: /App_Config/Include/[Foundation-Feature-Project]/Model/.config

