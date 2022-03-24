## Sitecore ASP.NET Core Rendering SDK

### Headless architecture

Headless architecture consists of a **back end** with a layer of services and APIs and a front-end/client/user-facing app.

The Frontend app retrieves data from the CMS using **API endpoints** and uses that data to populate, or hydrate, the markup it generates.

Three types of CMSs: traditional, headless, and Sitecore Omni.

Headlees CMS decouples the CMS's back-end content functions (creation, management and storage) from frontend functions (presentation and delivery). Multi-channel set up, knows as omnichannel (web-sites, mobile-apps, softwares).

Sitecore Omni is a headless CMS architecture that includes tradictional CMS but also offers personalization on any device or application.

### Headless development in Sitecore

### Output Caching for Layout Services

The main role of HTML Caching is to improve a website's performance by storing data on pages that may otherwise be slow to load.

ASP.NET Core uses JSON rendering with the Layout Service. When a call is made to the Layout Service, isntead of reserializing the data source items, or re-executing a custom rendering contents resolver, the cached JSON is returned.

- Factors:

    1. Performance: Caching increases performance by storing capies of data accessed frequently from external systems in a high-performance subsystem.

    2. Functionality: Web caches improve functionality by reducing latency and network traffic and thus lessening the time needed to represent a resource.

    3. Security: Sitecore ensures security by maintaining several caches containing security information.

- Sitecore Headless Services
    it includes the **Sitecore Layout** and it is install:
    - on-premises: as a Sitecore Package zip.
    - in Cloud Sitecore installation as a Sitecore Azure Toolkit.
    - in Sitecore container, using Dockerfile.

- Layout Service
    It is important to understand whether the content is being manipulated at the Layout-Service level.

- Rendering Host
    When the Rendering Host calls the Layout Service, it grabs published items from the content tree. The **Sitecore Rendering Host** operates outside of the **Content Delivery instance** and is the front-end application that requests data from the **Layout Service** and renders the site

Examples:

- Never catch **sensitive data**.
- Catch a rendering when the content of a rendering is directly edited and published in Content Editor.

- Options:

    - per-usage basis: Allows to catch a rendering when it is used. It is done by accesing the specific instance of the rendering on the content item. /home/ presentation / content
    - global default setting: cach the rendering definition item so that every instance of that rendering will carry the same default caching settings. sitecore/Layout/Renderings/Project folder. Select the rendering definition item, scroll to he caching section.

### Scaling Sitecore environment

Scaling a Sitecore environment with the ASP.NET Core Rendering Host requires specific scaling considerations for the ASP.NET Core Rendering Host itself and the Content Delivery instance.

Because the Rendering Host scales in a linear fashion, it's important to consider the size of the content coming from the Layout Service to the Rendering Host as it has a huge impact on performance. Performance Testing allow to determine where and how to best scale Sitecore.

### Differences between Scaling a Sitecore XP and XM Environment

The Rendering Host and Layout Service supports both horizontal and vertical scaling. Horizontal scaling is when additional instances are created to support the load and is also known as scaling out.

Vartical scaling is when other resources are added to a single instance to support the load and is also known as scaling up.

When the Content Delivery instance is scaled, be aware of overloading the other items' capabilities in the Sitecore environment.

Performance testings cover the scope of your entire build. Every implementation has different properties, settings, adn content, so it is cretical that performance testing is completed before implementing any caching anc scaling within the Sitecore environment.

### Container and Roles

Each container hosts a service or role in the Sitecore platform architecture.

docker-compose.yml

1. Traefik: Reverse proxy needed to manage requests to and from the browser ant the Sitecore environment. Default port is 8079. To access the Traefik dashboard type localhost:8079. You can view the HTTP values for the identity server, the rendering host, and the content management containers.
2. MSSQL: It houses the Microsoft SQL databases needed for the proper operationn of the Sitecore instance.
3. Solr: It is for the Sorl indexes for the Sitecore environment. The default port is 8984. On the localhost you can search and manage the indexes directly.
4. Id: It is for the authentication component of a Sitecore deployment, the Identity Server. As you access various points of the Sitecore environment, you will be redirect to the Identity Server to authenticate your access, including if you choose to use the Sitecore Content Seralization CLI.
5. CM: Content Manager role of the environment, which is the adminitrative interface for Sitecore, including the Content Editor, Experience Editor and the Sitecore Launchpad. The Content Management role also acts as the Content Delivery service.

docker-compose.override.yml

Some container and configurations are not included, such as the container for the Rendering Host> They are included in the docker-compose.override.yml file.

6. Rendering: It is a container for ASP.NET Core Rendering Host that support headless development with Sitecore.
    If it is set to **debug**, it used the image includes **ASP.NET Core Rendering SDK** and will run **dotnet watch**. The associated **Visual Studio** project source is mounted into the rendering container, so **dotnet watch** will recompile and restart the rendering host process when changes are saved to the source folder.

.env

It stores settings and default variables.

### Visual Studio projects and serialization

The Solution in Visual Studio has two projects:
- Platform
    Running Content Management environment. Any Publishes from this project may cause the Content Management environment to refresh. It changes are made to the Platform project. I the caseo of an Sitecore Explorer Platform environment, the Content Manager container host both, the Content Manager and Content Delivery roles.
- RenderingHost
    Corresponds to the Rendering Host.
    It is the **primary project** and the **start up project**. Model and Views are created there.

`dotnet watch`runs on the rendering container with the RenderingHost project source mounted into the container. When changes are made to the renderingHost project, `dotnet watch` will automatically recompile and restart the rendering host.

#### Content Serialization

It allows to easily put items into source control, build deployment scripts that push items to various environments, and create packages for later deployment.

You can pull a templete (templete, section and fields) from the Sitecore Content Management environment to the local workstation environment.

`dotnet sitecore ser pull`

If you remove a serilized template from the conten Editor, those changes are not populate to the Rendering Host.