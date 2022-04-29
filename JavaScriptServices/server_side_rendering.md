## Server Site Rendering

Server-Side Rendering (SSR) is essential to enabling integration with Sitecore editors, such as the **Experience Editor** and **Horizon**. The Sitecore editors rely on finding the rendered markup of new components being added to the pages when they pre-render them.

To help you server-side render JSS applications, Sitecore provides rendering engines. Each JSS application you connect and deploy to Sitecore can be configured to use a different rendering engine.

### Rendering Engine

A rendering engine performs server-side rendering (SSR) of JSS applications by enabling the execution of the same JavaScript application you run in development within the Content Management environment running a Sitecore instance.

The Sitecore Headless Services module enables apps to use one of the following rendering engines:

- The Sitecore Node.js rendering engine is a Node.js instance running on your Sitecore Content Management (CM) Server and server-side renders JSS applications running in integrated mode. You must install Node.js on the CM server, but you can configure and debug the Node.js instance.

- The Sitecore HTTP rendering engine is a remote Node.js instance, or rendering host, that communicates through HTTP requests with the Sitecore Content Manager Server. To use it, you must set up the HTTP rendering engine-client and server-side. If you created your app based on the JSS sample for Next.js, your application is already configured to use this engine.