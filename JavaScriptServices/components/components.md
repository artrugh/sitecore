## Components

**JSS components** have properties that contain the content data.

They are dynamically bound to routes. They must never be instantiated or render because the JSS infrastructure handles instatiation based on layout data.

Every rendering in a Sitecore page must have a corresponding component in the JSS app. The component must be added to the route by name.

This enables JSS to register the component with Sitecore and provide appropriate infrastructure to give it the content that it needs to render.

### Create a Component

In connected mode:
1. deploy the component registration to Sitecore database.

```sh
jss deploy component <ComponentName> --allowedPlaceholders=[placeholderName]
```

2. Create the component in JSS and register it in the ComponentFactory.

3. Deploy the app's build artifacts to Sitecore.

```sh
jss deploy files
```
5. Log in the Experience Editor and add the new component to the placeholder.

### Scaffolding

To facilitate the creation of new components, JSS Next.js, React and Vue.js sample applications provide a scaffolding script, defined int the *scripts/scaffold-component.\[ts|js]\. 

Invoke the script using JSS CLI `jss scaffold`. The path is defined in the manifest definition file in *sitecore/definitions/components*.

```sh
jss scaffold ComponentName
```

```sh
jss scaffold some/new/path/ComponentName
```

For **Angular**, JSS installs the **JSS Angular Schematics package** during app creation.

### Component Factory

When a JSS app renders a page, it reverses the layout data JSON fetched from Sitecore to figure out what components to render on the page.

The **Component Factory** is a mapping between **Sitecore renderings** and their **JSS component implementations**. Every JSS sample application has a **Component Factory implementation**. It is a JavaScript function that accepts a rendering names as a parameter and returns the associated JSS component.

The **Component Factory** is generated programmatically at build time by recursively inspecting the application's directory of components.

The logic is defined in *script/generate-component-factory.\[ts|js] file.

Place **granular components** in a different directory than all other components, such as *src/helpers* and *src/containers*.

Because the Component Factory only inspects the main directory for components *src/components*, it will not attempt to map any of the components included in other folders.