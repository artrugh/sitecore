## JavaScript Services JSS

Decoupling backend and frontend, enables to create **headless applications**.

> Headless architecture consists of a back end with a layer of services
> and APIs and a front-end/client/user-facing app.

### Sitecore JSS Features

Sitecore JavaScript Rendering SDK (JSS) comes with:

- **JSS CLI** - a Node-based command-line tool to help to create and maintain applications.

- A core JavaScript package for leveraging **Sitecore Headless Services and Sitecore Experience Edge endpoints** using **REST or GraphQL**.

- Abstractions for front-end developers that allow working with Sitecore declaratively.

- **Utility functions** and **front-end components** that abstract the complexities of fetching dynamic Sitecore data.

- Dedicated SDKs for popular front-end frameworks:
    - Next.js
    - React
    - Angular
    - Vue.js
    - React Native (experimental)

- **Workflows** and **applications modes** for working **disconnected from** or **connected** to Sitecore instance. Front-end and back-end development teams can work in parallel.
    - Workflows:
        - Code-first development.
        - Sitecore-first development.
    - Modes:
        - Disconnected.
        - Connected.
        - Integrated.

- **A limited set of opinions about framework-specific tooling**, allowing developers to leverage best-in-class, familiar tools for code optimization, theming and styling, display of dictionary data, search engine optimization, and so forth.

- **Quich setup of development environments** using officially supported application samples. The application samples include examples documenting how to use each framework-specific SDK.

- **Multiple rendering options**. Applications created with any framework-specific SDKs can be rendered server-side for improved search engine optimization using framework capabilities (Next.js) or tooling provided by JSS.

- Support for **integrating advanced Sitecore editors**, retaining content and layout management, and preview capabilities.

- Support for **multilingual applications**, taking advantage of Sitecore language versioning, localized routes, and language defaults.

- Support for Sitecore MVC applications, allowing developers to use JSS in existing Sitecore MVC implementation through **client-side embedding** or use JSS to **generate MVC applications as static HTML**. JSS does not lock the entire implementation into JavaScript. Jss applications can coexist with .NET Core or traditional MVC applications in the same Sitecore instance.

JSS supports:

- inline editing
- multi-language
- analytics
- personalization
- integration

| feature | description |
| --------- | -------- |
| JSS Library             | series of npm packages that facilitate working with Sitecore data and presentation in JS |
| Sitecore Layout Service | composition of pages and data needed for each component |
| Js veiw engine          | allows to perform server side rendering of js apps |
| Application Import      | allows to apply a code-first approach |

### Benefits

- It provides easy web app deployment and management as a nimble, self-contained JS bundle.
- Application integrations: JSS takes care of generating all necessary artifacts.
- Can use CDNs, proxies and Node.js server to scale your application.
- Cross-Platform support: Deploy the app to any platform that runs server-side js.
- you can use any service that support hosting Node.js applications for server-side rendering.
- You can build your app independently and disconneted from Sitecore, and by using any Framework (React, Vue, Angular, Next.js).

Once you deploy the app to Sitecore, you are able to manage the app in the Sitecore Experience Platform (XP) enterprise backend.

### Code first approach principle

It allows to create and deploy apps in differents frameworks.

- develop apps in your preferred OS.
- disconnect completely from Sitecore
- Working with JSS SDK without a Sitecore server install.

### JSS CLI

```sh
npm -i -g @sitecore-jss/sitecore-jss-cli
```

Node-based command line tool with development scripts. It is the base tool for the code-first workflow.

- create, maintain, and run JavaScript applications.
- Scaffold components.
- Deploy apps to Sitecore.

### Steps

1. Identify the framwork (React, Angular, View, Nextjs) you want to work with.
The jss cli icludes the mocked Sitecore Layout Service so you can develop without the need to connect to a Sitecore installation.

2. Create a Sample Application

jss create my-app angular
```sh
jss create <app-name> <framework-name>
```

3. Run it

In the root folders

```sh
jss start
```

### App Directory

sitecore/config: site definition for the route items and the database.

The app is a repository structure. In disconnected mode, use the manifest API to:

- define the structure of your JSS site.
- run the site with mock data.
- import the site into Sitecore.

Manifest:

- Includes content data and data schema with both components and routes from a set of files.

- Enables the JSS app to execute with local mock content, without a Sitecore instance.

- Assing the JSS app as the master copy of all artifacts.

### Directory Elements

- Arbitrary Content:
    - /data/content
    - not pages, neither data sources
    - "lookups" or "list items"
    - they can not be view directly in browsers because they don't have any layout data.
    - use to restricting values of route-level or component-level fields to a limited set of options such as sharing content across routes.

- Routes
    - /home/route-name
    - Pages which has a unique URLs. They content route-level fields and instructions for how to lay out the route's components.
    - Site implementations may need multiple **route types** to capture route-level fields. Those route types are called **templates**.

- Components
    /home/route-name/page-components
    - **Rendering datasources** where a datasource is comprised of component name plus its field.
    - They contain component-level-fields. They can be viewed in browsers directly because they don't have any layout data, simply building blocks for route presentation.

### Routes

JSS extends Sitecore's dynamic, **component-based layout model** to the frontend.

With JSS's layout model, you create routes so the components can display content.

- the disconnected data defines a route's components and their data when applicable.

- JSS extends Sitecore's dynamic, **component-based layout model** to the frontend.

#### Process

Route data is typically retrieved from static **YAML or JSON files or simple JavaScript files** (data/routes).

After importing the app to Sitecore, Sitecore then defines the data dynamically.

The route data is retrieved using calls to the Sitecore Layout Service, via HTTP or in-process for integrated mode server-side rendering (SSR).

SRR is the process of taking a client-side JavaScript framework website and rendering it to HTML and CSS on the server.

Features:

- JSS library: series of npm packages that facilitate working with Sitecore data and presentation in JS.

- Presentation layer that provides the composition of pages and the data needed for each component.

**Mock Layout Service**

It emulates the data you receive from the **Layout Service**.

It provides a consistent API to create a single-page JSS application that includes components, routes, and custom route types as well as the needed data for each component.

It provides integration with Sitecore.

### Templates

/data/component-content
static component data which is reusable.

Routes are items in a page that map, to a route. The page-level items that conrrespond to the route are expected to have conventional presentation details set on them.

Templates do not have presentation as they are arbitrary content. They're just used for datasources or to populate fields.

Every file under routes becomes a page.

**routes.sitecore.js** file is a **default route template** which automatically set as a base template for any route types defined in the app's manifest.

When should **fields** be added to  **routes** or **components**?

- To components:
    - when they are generic fields. You can have component datasource items shared by multiple components on multiple pages.
- To routes:
    - when you need filtering and searching in order to more easily query your pages.

### Create a Route

- browse to sitecore/definitions/
- create a folder called routes
- add a file called *<route-name>Route.sitecore.js*
- create a function and add the `addRouteType`.

### Rendering a component

1. The router requests the content of the component from the corresponding **item** in the **mock or Sitecore Layout Service**. These fields are stored in a **database**. Then the Layout Services processes the request.
2. View Output Data
3. Add the component to the page.
4. Add content into fields on the component. JSS SDK provides framework-specific field helper to render fields.

### Register a Component

- Scaffolding creates the framework component and disconnected component definition files first.
*/scripts/generate-component-factory.js*

It is use to indicate that your are using JSS and points to an empty Razor view. Whereas in traditional Sitecore, the layout is pointing to a cshtml file, which contains the scaffolding of the presentation.

```sh
jss scaffold NewComponentName
```
- Add a field to the component: data/routes
    - define field values in placeholders.
    - define a text string.
    - define text string options.
    - render parameters.
        - when data is not stored as fields on a data source item.
        - define parameters values in the route data as any JS object type.
        - components receive and render all parameters values as strings.
        - components receive a params object via props (props.params.paramName)
        - as part of the manifest generation process, you can map parameters data to component objects you add to the manifest.
        - add the component to a type event page to render the description route field.

```js
import { withSitecoreContext } from "@sitecore-jss/sitecore-jss-react";

const NewComponent = ({ sitecoreContext: { routes: { fields: { descriptions }}}}) => {
    return <div>{description}</div>
}

export default withSitecoreContext()(NewComponent)
```

### Mockup data

Mockdata by copying files, images fields, and other items into the file system.
When the app runs disconnected, it does not have data from Sitecore using HTTP data calls.

The Styleguide is used to add items into the file system.

You can add three types of mock content:

1. route-level fields data.
2. Image field.
3. Item link.
