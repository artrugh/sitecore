## Architecture Overview

Applications created with JSS consume Sitecore content and personalization delivered by **Sitecore Headless Services** or **Sitecore Experience Edge for XM**.

Sitecore Headless Services include:

- .NET Core Rendering SDK.
    - Rendering Engine.
    - Media Handler.
    - GraphQL.
    - LayoutService.
- JavaScript Rendering SDK.
    - Rendering Engine.
    - Media Handler.
    - GraphQL.
    - LayoutService.
    - Dictionary Service.
    - Import Service.

The application can be:

- server-side rendered using Node.js rendering engine, provided by Headless Services.
- Sitecore-independent rendering host for a truly headless architecture.

The **manifest definitions** allows the JSS CLI, App configuration, and the Import Service to develop and deploy applications to Sitecore.

JSS feature:

- Core SDK functionality for retrieving Sitecore data from various Sitecore services and APIs.
- SDKs that facilitate building JavaScript applications with some of the most popular JavaScript framworks.

### Use cases supported by JSS applications

- Content Management using advanced Sitecore editors.
- Content Presentation, without compromising the Sitecore workflow.
- Content internalization.
- Experience management.

### JAMstack

Separete Application Runtime from HTTP Request Processing.

The Server doesn't wait for request to beggin rendering the app and to generate MarkUp.

- **Pre rendering** does it ahead of time. It generate MarkUp to be store in static files which are deployd to CDNs. The CDNs are responsibe to response to HTTP requests.

- **Static Side Generators** handel server side JavaScript tasks and reduce the number of backend services.

- **Client side JS** makes async call to the Server to fetch dynamic data base on user interactivity (Rehydration).

