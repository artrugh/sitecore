## Sitecore Rendering Engine

[Official Docu](https://doc.sitecore.com/xp/en/developers/101/developer-tools/sitecore-rendering-engine.html)

The **Sitecore Rendering Engine** renders content fetched from a Sitecore instance using the **Sitecore Layout Service**.

You must perform some configuration to use the Rendering Engine in your application. Most of this configuration is done in the Startup class. See the Microsoft documentation on App startup in ASP.NET Core.

### Registry the Sitecore Rendering Engine

To add the required Sitecore Rendering Engine services to the Dependency Injection container, you use the AddSitecoreRenderingEngine() extension method from the Sitecore.

The method returns an ISitecoreRenderingEngineBuilder instance to allow further configuration of the Rendering Engine using other extension methods.

In the Startup class:

```cs
public void ConfigureServices(IServiceCollection services)
{
    var renderingEngineBuilder = services.AddSitecoreRenderingEngine();
}
```

The AddSitecoreRenderingEngine() method accepts an Action<RenderingEngineOptions> parameter which allows for the Rendering Engine options configuration.

```cs
public void ConfigureServices(IServiceCollection services)
{
    var renderingEngineBuilder = services.AddSitecoreRenderingEngine(
        options => options.MapToRequest(
            (httpRequest, sitecoreLayoutRequest) => sitecoreLayoutRequest.Language(httpRequest.Query["lang"]))
    );
}
```

- ICollection<Action<HttpRequest, SitecoreLayoutRequest>> RequestMappings - a list of mappings between the current HttpRequest and SitecoreLayoutRequest can be specified.

    The default mapping sets:

    - The Language on the SitecoreLayoutRequest from RequestCulture.Culture.Name in the IRequestCultureFeature, if present.

    - The Path on the SitecoreLayoutRequest from the sitecoreRoute route value, if present.

    - The Path from the HttpRequest.Path value, if the sitecoreRoute route value is not present.

- SortedList<int, ComponentRendererDescriptor> RendererRegistry - a sorted list of component renderers. By default, this list is empty.

```cs
public void ConfigureServices(IServiceCollection services)
{
    var renderingEngineBuilder = services.AddSitecoreRenderingEngine(
        options => options
            // Map Partials
            .AddPartialView("HeaderBlock", "_HeaderBlock")
            .AddPartialView(name => name.StartsWith("sc"), "_OtherBlock")

            // Map View Components
            .AddModelBoundView<BoundContentBlock>("ContentBlock")
            .AddViewComponent("Styleguide-Layout", "StyleguideLayout")
            .AddViewComponent(name => name.StartsWith("sc"), "Other")

            // Add fallback for any other component
            .AddDefaultPartialView("_ComponentNotFound");
    );
}
```

### Using endpoints and controllers with the Rendering Engine

When creating content-driven Sitecore sites, the Sitecore content tree typically owns routing – that is, Sitecore URLs are driven by the structure of its content tree.

A Sitecore URL takes one of the following forms out of the box:

- With Language - /[language ISO]/path/to/the/page

- Without Language - /path/to/the/page

If your site is multilingual, you must also configure request localization. You can then use the *MapSitecoreLocalizedRoute* extension to configure a route which supports Sitecore-style language embedding and content paths.

To support paths without language, you can use the built-in ASP.NET *MapFallbackToController* as a catch all to handle Sitecore content paths.

Multilingual sites typically handle both language embedding and content paths, unless your Sitecore link provider is explicitly configured to always embed language.

Example of Sitecore routes mapped to the Index action in the Default controller:

```cs
app.UseEndpoints(endpoints => 
{ 
  endpoints.MapSitecoreLocalizedRoute("Localized", "Index", "Default"); 
  endpoints.MapFallbackToController("Index", "Default"); 
}); 
```

Be sure to tag the Index action with the [UseSitecoreRendering] attribute (available in the Sitecore.AspNet.RenderingEngine.Filters namespace) to enable the Sitecore rendering middleware and the corresponding request to the Layout Service:

```cs
public class DefaultController : Controller 
{ 
  [UseSitecoreRendering] 
  public IActionResult Index(Route route) 
  { 
    return View(route); 
  } 
} 
```