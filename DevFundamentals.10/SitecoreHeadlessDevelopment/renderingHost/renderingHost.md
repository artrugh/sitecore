## Sitecore Rendering Host

Headless development in Sitecore introduces further **separation of data and presentation** in Sitecore environment.

It introduces the **Sitecore Rendering Host** that operates outside of the **Content Delivery** instance and provides the tools for faster development interations.

Sitecore Rendering Host is the frontend section that through the **Layout Server Client** requests data from the **Layout Service**.

The Layout Service retrieves data from the **Content Delivery instance** and returns the content data in **JSON** format to the Rendering Host.

It is extremely useful for **multi-channel scenarios**, cause the backend can serve the same data to all the channels without having to manipulate the content.

### Process

HTTP Request from browser =>  ASP.NET Core Sitecore Rendering Host => Layout Service => Content Delivery instance

Content Delivery instance (JSON Data) => Layout Service => Sitecore Rendering Host (combines content data with the .NET Core / rendering context and model) => HTML

The **Layout Service Response** is a content in JSON format. The Rendering Host combines the **content data** received with the **.NET Core code** and returns it as ****HTML** to the browser.

CONTENT DATA + .NET CORE CODE = HTML

Benifits to Developers:

- Build a small, light-weight, .NET Core application that does not require a full restart of the Sitecore environment to preview code changes.

- You can run the Rendering Host application directly in Visual Studio with the debugging functionality of Visual Studio.

- Seamless interaction between the .NET Core application and your existing architecture.

[more info about the Layout Service](/DevFundamentals.10//SitecoreHeadlessDevelopment/sitecoreLayoutServices.md)

### Prerequisites

- Powershell 5.1
- Docker
- .Net Core 3.1 SDK

### Configuration Requeriments

Site definitions are configured in a patch file to the *sitecore.config*.

- Configure Root Path
    A single Sitecore instance uses **multiple websites** to manage content delivery, content management, and many other features. However there is only one published website.

    ```xml
    <site name="website"/>
    ```

- Configure Host Names
    Configure hostName or targetHostName URL as the external-facing host name of your Content Delivery (CD) server.

- Configure Experience Editor support

    - JSON Renderings
        Sites based on ASP.NET Core require the **rendering components** to be created as **JSON renderings** within the Sitecore environment, instead of view or controller renderings, because the **Layout Service** serializes the data for ASP.NET components when the Sitecore component is a JSON rendering.
    
    - Dynamic Placeholders
        The **Layout Service** assumes all placeholders are **dynamic**, exception being root placeholders such as main, header, and footer.

        In the *appsetings.json*

        ```xml
        <EnableExperienceEditor="false">
        ```
        If using docker, there is a (Sitecore_EnableExperienceEditor="true") in the *docker-compose.override.yml*