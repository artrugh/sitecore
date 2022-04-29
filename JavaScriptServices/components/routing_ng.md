## Routing in Angular

The JSS Angular sample application comes with a root placeholder. The placehoder is defined in *scr/app/routing/layout/layout.component.html*.

The sc-placeholder component is imported from Sitecore JSS for Angular.

```html
<sc-placeholder name="jss-main" [rendering]="route" (loaded)="onPlaceholderLoaded($event)"></sc-placeholder name="jss-main" [rendering]="route"></sc-placeholder>
```

Receiving the **route** data.

In production, the script for building the JSS Angular application builds:

- server bundle: located in dist/browser/
- client bundle: located at dist/server.bundle.js

The two bundles cannot run on their own.

They must be served and this requires a server, **JavaScript view engine for Node**, that runs the server bundle and export a **renderView function**.

To build the two bundles and serve them, the **JSS Angular app** defines two entry points for the application, with associated app modules and data services.

### Server Bundle

*src/main.server.js*

It defines the entry point for the **server bundle**.

It bootstrapps the **application module** for the server AppServerModule, defined in *src/app/app.server.module.ts*.

AppServerModule runs on the server and stores the context data for the JSS app.

- The AppServerModule uses the **JssContextServerService** from *jss-context.server-side.service.ts* which runs on the server and stores the **context data** from the JSS app.
    - The context data contains:
        - the data for the current route.
        - Sitecore context data.

### Client Bundle

*src/main.js*

It defines the entry point for the **client bundle**.

It bootstrapps the **application module** for the client rendering **AppModule**, defined in *src/app/app.module.ts*.

The **AppModule** uses the **JssContextService**, defined in *src/app/context.service.ts*, that runs on the client and stores the context data for the JSS App.

When the application runs in the browser, from the server bundle, the server invokes the **renderView** function that renders the **AppServerModule**, preparing the content data for the JSS app *server.bundle.ts*.

Both *context.service* and *ss-context.server-side.service*, use the Angular Platform Browser Class **TransferState**, a key value store that is transferred from the application module on the **server-side** to the application module on the **client-side**.

The **AppModule** bootstrapps the root application component **AppComponent** and imports the **RoutingModule** class, which is responsable for attaching the Angular router to the application root, allowing the JSS Angular app to use an Angular router outlet.

The **RoutingModule** defines which component renders in the router outlet placeholder. It uses the **JssRouteResolver** provider that, when resolving a route, sets the state for the active route.

Finally, the **LayoutComponent**, injected with both, **route** and **layout data**, can subscribe to the active route and extracting the route data from the Sitecore context.