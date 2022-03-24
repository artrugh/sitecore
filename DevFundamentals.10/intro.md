## Sitecore 10

New features in Sitecore 10.

- Containers
- Sitecore Content Serialization
- ASP.NET Core Rendering SDK

### Containers

[official-docu](https://containers.doc.sitecore.com/)

You can develop the **Sitecore product** with containers regardless of the  environment's deployment method.

Development: Docker
Production: Kubernetes

- You don't need to install Sitecore locally on your development workstation.

- You can **avoid** using the **Sitecore Install Framework (SIF)** by utilizing the base images provided with **Docker Compose files** from Sitecore.

- Faster onboarding new Developers to a team or project, just cloning the code repository and run a **docker-compose up**.

- More control over the build environment and continuos integration pipeline.

### Sitecore Content Serialization

[official-docu](https://doc.sitecore.com/xp/en/developers/100/developer-tools/sitecore-content-serialization.html)

Content serialization allows developers:

- to **serialize** any Developer-owned or demo **content** to migrate or sync between Sitecore instances.

- to **push and pull data**, such as **content items, templates, and renderings**, from a controlled shared area when needed.

- to share **artifacts** through **source control** and for **deploying changes to production**.

Tools for serialization:

- **comand-line-interface (CLI)**: login, manage, publish.

- **Visual Studio Plugin (Graphical User Interface)**


### ASP.NET Core Rendering SDK

[official-docu](https://doc.sitecore.com/xp/en/developers/100/developer-tools/sitecore-headless-development.html)

It allows developers to rapidly develop **independently running ASP.NET Core web applications** against the **headless APIs** first introduced with Sitecore JSS.

#### Features

1. **Client API** for Sitecore Layout Service. It provides classes for involking Layout Service.
2. **Tag helpers** to render Sitecore placeholders, including mapping to specific component implementations in the ASP.NET Core (partials views, view components) 
3. **Tag helpers** for rendering Sitecore fields.
4. **Mapping requests** to the Layout Service Client.
5. Extensions to the **model binding** within Microsoft ASP.NET Core.
6. Integratoin enabling the **full Sitecore Experience Platform functionality**, including the **Experience Editor, analytics, and personalization features**.
7. Proxing cookies to the **Layout Service Client**, including **Sitecore analytics cookies**, as well as **Sitecore visitor indetification**.

#### Benefits

You don't build code into the Sitecore instance.

You don't longer have to recycle the entire application pool when you build a new rendering.

Additional headless rendering option for Developers.

Allows developers to rapidly develop independently running ASP.NET Core web applications against the headless APIs first introduced with Sitecore JSS.

Using Sitecore Layout Service to obtain content and layout.