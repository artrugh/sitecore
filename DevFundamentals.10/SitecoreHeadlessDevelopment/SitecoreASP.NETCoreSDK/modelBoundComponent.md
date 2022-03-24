## Model Bound Component

Template are Sitecore Items created to provide structure to content and data through the Sitecore system.

Some components required data input from Content Authors, certain data fields need to be accessible when building the components.

When creating a templete it is important to set the Standard Values which are used as initial values for the new item before being edited or changed by Creator Author.

### Create JSON Renderings with ASP.NET Core Rendering SDK

In Sitecore MVC, the renderings items created are either view or controller renderings.

When working with  Sitecore headless SDKs the preferred rendering item is a **JSON Rendering**. The Layout Service is able to return data in JSON format.

Process:

1. Create a DataSourceTemplate. This is the foundation for the data source of the component.

2. Create the JSON Rendering.
    - sitecore/Layout/Renderings/Project/MyProject
    - Insert Json Rendering
    - name it
        The Component Name of the **JSON Rendering** is important as it is how Sitecore maps the Layout Service response to the component in the rendering host.
    - set **Datasource Location** field.
    - set **Datasource Template** and select the template.

3. The JSON Rendering Item needs to be available for use in a placeholder.
    - sitecore/Layout/Placeholder Settings/Project/MyProject
    - select a pladeholder
    - add the Allowed Controls section edit and include the JSON Rendering.

4. Add the component to the placeholder in Sitecore Explorer.

5. Add the data source item.

6. Run publish to make changes accessible in Visual Studio.

7. Pull changes to Visual Studio `dotnet sitecore ser pull`

8. View the logs in the PowerShell of the Layout Service `docker-compose logs -f`

In Visual studio

A model contains the fields utilized in the data template. These are automatically data-bound due to type inheritance from the instance Field.

The razor view utilize tag helpers to output fields edited in Experience Editor and has HTML and CSS markup for design.

9. Registration is necessary to map the JSON rendering with the model-bound view. With it the placeholder can render the component with the Layout Service output.
    - In Startup.cs file on the services.AddSitecoreRenderingEngine => AddModelBoundView<ModelName>("RenderingName")
    - Recompile running `dotnet watch` or right-click on Platform / Publish
