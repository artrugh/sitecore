## Launch Strategy

Develop, test, deploy lifecycle.

The key of deployment is automation, deployment should be a repetable process that include a few custom mechanical or developer steps as possible.

### 301 redirect

One keep detail to keep in mind as you move towards launch is the impact that publishing can have on a **user's experience** and **search engine optimization** (SEO).

A **301 redirect** is a **permanent server-side redirect** from one URL to another and will ensure that site visitors and search engines are sent to the URL of the new site.

Strong **301 redirect** will prevent any potencial confusion on the new location of your site content and ensure thet your new build is optimized for maintaining, and potentially increasing, the power of your original site.

### Strong Rollback Plan

Set a stron rollback plan as a **blue-green deployment**. IT will reduce downtime through the use of two identical production environments.

Only one of the environments will be live at any given time.

### Deployment

Some **data and configuration** is owned by the **development process** while others are owned by the **production environment**.

**Ownership** means that a change in th given environment will take precedence and will always **overwrite changes** in other environments.

General parts of a deployed in Sitecore:

- Items.
    - Content Items.
        - They are displayed on a website or other digital channel.
        - Ownership: production environment.
    - Definition Items
        - **Sitecore data items** that configure the implementation. They are **data items** that configure the implementation and have a direct relationship with the presentation and business logic in the code.
        - Ownership: development environment.
- Files.
    - Implementation files.
        - Assemblies, views, css and js files.
        - Ownership: development environment.
    - Platform Files.
        - Vendor specific files that are isntalled as part of a standard module.
        - Ownership: development environment.
    - Configuration files.
        - Implementation configuration files are configuration that set up application-wide functionality.
            - Ownership: development environment.
        - Configuration Role files are those that set up the instance as a particular Sitecore instance.
            - Ownership: deployment environment.
        - Configuration Environment Files.
            - They are configuration files changes relating to specific running server or environment.
             - Ownership: deployment environment.      
- Environment.
    - Configuration. It is the server or environment-specific configurations.
    - Services.
    - Infrastructure.
