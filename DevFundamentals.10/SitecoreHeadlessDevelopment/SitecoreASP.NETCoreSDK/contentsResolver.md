## Content Resolver

1. Create a content resolver.

    In Visual Studio:

    - Add Sitecore.LayoutService Nuget Package and access *RenderingContentResolver*.
    - Add templates (it is a class).
    - Create a Content Resolver Class that implements *RenderingContentResolver* and override *ResoverContent* method.
    - Publish

    In Content Editor:

    - In *sitecore/System/Modules/Layout Service/Rendering Content Resolvers* add a **Content Resolver Item** (registration of the Content Resolver).
    - enter name.
    - On the content tab in the **Data section** in the **Type** field, enter the name of the Content Resolver: `MyProject.LayoutService.NavigationContentsResolver, MyProject`
    - Select **Use Content Item**.
    - Save

2. Create a JSON Rendering Item.

    The **Json Rendering** renders the output of the content resolver class.

    In the Content Editor:

    - In *sitecore/Layout/Renderings* insert a JSON Rendering.
    - enter name.
    - On the content tab in **Layout section** in **Rendering Content Resolver** field, select the item.
    - Save the JSON rendering item.

3. Add the JSON rendering item to the Page Template standard values.

    - navigate to the standard values.
    - In *presentation details/Layout Details*, in *Layout Details* in the *Default* section, edit.
    - Select Main Controls and add.
    - Select *Rendering Window* and click the Rendering.
    - In *Add to Placeholder* field, enter the placeholder and click *Select*.

4. Create the Model.

    - In the Solution, in *RenderingHost/Models* add a new Item.
    - Installed/Visual C#/ASP.NET Core/Code
    - Class
    - Name
    - Add

    In the Model you are not binding directly Sitecore fields, so use **String Type** and the attribute **[SitecoreComponentField]**

5. Create the model bound view.

    - In the Solution, in *RenderingHost/Views/Shared/Components/SitecoreComponent* add a new Item.
    - Installed/Visual C#/ASP.NET Core/Web
    - Razor View
    - Name, it should match the name of the **JSON Rendering**
    - Add

6. Register the model-bound view in *Startup.cs* file using the `.AddModelBoundView<Model>("Name JSON Rendering")`.