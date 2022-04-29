## Application modes

Applications created with the **Sitecore JavaScript Rendering SDK** can run in several modes:

- Development:
    - **Disconnected mode**: does not require a running Sitecore instance. You host the application in your local environment, and you use local content data (used with **code-first development workflow**).
    - **Connected mode**: running Sitecore instance. You host the application in your local environment, and you use content data from the Sitecore instance. 
    - **Integrated mode**: running Sitecore instance, which hosts the application, provides content data, and renders your application server-side.

- Production:
    - **Headless server-side rendering mode**: server-side rendering performed on the Node server, data from Sitecore Content Delivery.
    - **Integrated mode**: server-side rendering performed on the Sitecore Content Manager server (for compatibility with Experience Editor only).


### Disconnected mode

You must mock content data using local files using the YAML or JSON formats.

Developers can import applications developed in disconnected mode to Sitecore, creating all necessary Sitecore items for the application to run in connected mode later.

All JSS applications created with a framework-specif SDK using JSS CLI command `jss create` include a script in the *package.json* file to start the application in disconnected mode.

### Connected mode

When running the JSS application in connected mode, the rendering of the application is preformed by the **browser**. The Sitecore databases hold the **content**, **layout data** and **content registrations**, so any mock data is necessary.

All JSS applications created with a framework-specif SDK using JSS CLI command `jss create` include a script in the *package.json* file to start the application in connected mode. `jss: start:connected`.

### Integrated mode

It allows to server-side render the application and integrate applications with advanced Sitecore editors: Manage content, presentation, marketing features; Experience Editor or Horizon.

The JSS app is host within a Sitecore instance. The app is SSR by a **Node.js instance hosted** and orchestrated by Sitecore or by a **remote rendering host** leveraging the **HTTP rendering engine**.

Complete HTML is delivered to the user without any initial **Javascript execution on the client**.

Data comes from **Sitecore Layout Service**, passed from Sitecore to Node with no extra HTTP call.

In an JSS application built with `jss create` command based on official application samples, you can find the hostname in the application's configuration files located at */sitecore/config/<YOUR_APP_NAME>.config`.

### Headless server-side rendering mode

It allows to **deploy** and **run** the application on any platform that supports Node.js and Express.

The rendering is performed by a **Node.js server** using platforms such as Azure App Service, Vercel, Netlify, or Heroku.

The application retrieves the data from Sitecote Content Delivery server ussing HTTP requests to various **Headless Services and APIs**.

A headless server-side rendered JSS applicaction has full **Sitecore marketing and personalization support**.