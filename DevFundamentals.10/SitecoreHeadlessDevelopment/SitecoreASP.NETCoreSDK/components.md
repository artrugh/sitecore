## Components in Sitecore ASP.NET Core

Components are created primarily through views and models. There are different view types used to create components for use with the **Sitecore Rendering Host**.

### Model Binding

The **Sitecore Rendering Engine** provides ASP.NET model-binding support for **key objects, properties, and fields** returned by the Layout Service in a **Sitecore Layout Response** object.

When the response comes in, ASP.NET Core resolves a **controller action** and inserts middlewares, triggering the mapping between the incoming **request** and the **Layout Service Request**.

The Sitecore ASP.NET Core SDK model-binding extension allows binding to data from the Layout Service Response to strongly typed model.

This model can be rendered in a Razor view using field rendering tag helpers.

### View types

- Model Bound Views

    They are backed by a **default Sitecore View Component**.

    They are the most used.
    
    You just need the **Razor View** in */View/Shared/Components/SitecoreComponent* folder and the **View Model Class**. It doesn't need a view class.

    Then, configure the mappings in the *Startup* class, in the `ConfigureServices()` method, by the `AddModelBoundView<TModel>(<name-of-the view>)`method.

    This method map the **Layout Service Response** to the **view component**, providing the view with the **Model**.

- Custom View Components

    They **do not use ASP.NET model binding** and only access data on demand.

    They are use to render **complex logic**.
    
    However the ASP.NET Rendering SDK provides a service and base component to enable binding a model to Layout Service output.
    
    A View Component consists of three files:

    1. View Component Class which add additional logic.
    2. Razor View.
    3. View Model Class.

- Partial Views

    They render **HTML output** within another **View's Rendered output**.

    They are the lightweight components that make a Sitecore page. And they are used for structural components that contain placeholders.
    
    
    They follow the standard MVC conventions and the standard rules in ASP.NET Core MVC.
    
    You must map the Layout Service response to the partial view.
    
    Configure the mappings in the *Startup* class, in the `ConfigureServices()` method, by the `AddPartialView<TModel>("view-layout")`method.


    Template are Sitecore Items created to provide structure to content and data through the Sitecore system.

- Rendering Contents Resolver Items.

    Rendering Content Resolvers allow to define a Sitecore query or .NET class that customizes the output of a JSON Rendering. With it a model-bound can access complex data.

    They are often used for items such as **site navigation components, search bar components, or user login features**.

Some components required data input from Content Authors, certain data fields need to be accessible when building the components.

When creating a templete it is important to set the Standard Values which are used as initial values for the new item before being edited or changed by Creator Author.

#### SitecoreLayoutService NuGet package

It provides assemblies, types, and classes needed for extending the Layout Service server output.

