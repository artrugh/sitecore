
## Components Types

- View renderings
- Controller renderings

### View rendering

View rendering are the more basic rendering and utilize a default model, **RenderingModel**.

A view rendering is a basic, stand alone [Razor](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-6.0) view file to display content data.

Razor view components are implemented using a combination of c# and html. It contains little to no code. Not logic at all. It presents data.

When paired with **dynamic binding**, view rendering components can be **added or removed** from a presentation with ease.

```diff
+ In order to user a View Rendering, same as Layout, it needs a component definition item, that link the component definition item  to the path for the .cshtml file.
```

Create a **component definition item** in sitecore/layout/Renderings, to linking the **View rendering** adding the path for the .cshtml file.

The Rendering presentation file references to Sitecore.Mvc, Sitecore.Mvc.Presentation namespaces and RenderingModel.

### Controller rendering

A controller rendering uses RenderingModel or a custmon Model which follows the MVC pattern.

Advance business logic is necessary.

When creating a Controller rendering, you need to manually create the corresponding **controller rendering definition item** for the rendering Sitecore Explorer or Content Editor, and specify the controller within the project and the action the controller invokes.

Create:

- Controller rendering definition item
- Specify the controller within the project and de action (Index).

An example:

In the controller rendering definition item in layouts/renderings/foundation/FooterController

template: /sitecore/templates/System/Layout/Renderings/Controller rendering

Data:
    Controller: .../Controllers.FooterController.ClothingWeb
    Controller Action: Index
