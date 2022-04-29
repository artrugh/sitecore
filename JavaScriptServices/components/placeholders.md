## Placeholders

- Sitecore JSS utilize a tree/nested route layout structure instead of addressing components on a page.
    - In disconnected, the route data structure is created by the developer. When working disconnected, developers determine the binding of components to specific placeholders through route data files.
    - In connected and integrated modes, the layout data from Sitecore is converted into a nested structure before rendering.
- All placeholder are dynamic, except the immediate children of the root placeholder.
- Utilize dynamic placeholder format that includes the rendering UID.
- Generate the rendering UID when creating the manifest before a Sitecore import.

### Placeholder naming

- Prefix placeholder names with an app-specific prefix. This is important because a sitecore instance can host multiple JSS apps and websites, and it is best to avoid conflicting placeholder names.
- Choose a name that describes the general purpose of the placeholder and avoid jargon.
- Assign a user-friendly display name for each pladeholder in */sitecore/definitions/pladeholders.sitecore.js*
