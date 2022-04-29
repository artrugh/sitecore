## Sitecore Layout Services

There are two services:

- Layout Service which is in **Sitecore Headless Services**
    The Sitecore Headless Services includes the **Sitecore Layout**.
    The Layout Service is an **endpoint** that provides **JSON formatted Sitecore content**.
    It communicate with the **Layout Service Client**.
- Layout Service Client which is in the **Rendering Host Service**

Those two services communicate throug an **endpoint** using **query string key**.

The Layout Service exposes two actions:

- Getting the output of the whole layout for the item.

  - REST API

    `<hosting-name>/sitecore/api/layout/render/<config>?item=<path or ID>&sc_lang=<language>&sc_apikey=<key>&tracking=<true | false>&sc-site=<sitecore-name>`

  - Odata
    `<hosting-name>/sitecore/api/ssc/aggregate/content/Items('{item-id}')?sc_apikey=<key>`

- Getting the output of a particular placeholder.

  - REST API

    `<hosting-name>/sitecore/api/layout/placeholder/<config>?placeholderName=<path or ID>&sc_lang=<language>&sc_apikey=<key>&tracking=<true | false>`

  - Odata
    `<hosting-name>/sitecore/api/ssc/aggregate/content/Items('{placeholder-id}')?sc_apikey=<key>`
  

Process:

1. The Layout Service performs an item lookup based on the item parameterm which takes into account the start itme of the context site.

2. After resolving the item, the Layout Service utilizes placeholder data in Layout and Rendering definition items to render the item to an object structure. By using Sitecore MVC pipelines, the Layout Service output accounts for any personalization rules and/or content testing in the item's layput definition.

3. Instead of rendering MVC views, a custom JavaScript serializer takes the component's data source items and serializes them into JSON.

4. The output is a JSON.

| property | description |
| -- | -- |
| config | name of the Layout Service configuration to use, normally jss for JSS |
| item | The path to the irem, relative to the context site's home item or item GUID (ID) |
| sr_lang | The language version of the item you want to retrieve |
| sc_apikey | An **SSC API key** configured for use with the Layout Service controller |
| sc_site | The name of the site to fetch data for |
| tracking | (Optional) Enables/disables analytics tracking for the Layout Service invocation. Default is *true* |
### Sitecore Layout Request

The **Layout Service Client** generates a **Sitecore Layout Request** which instantiated a **Data Transfer Object** (DTO) and contains properties.

| property | method | content | sample | query string key |
| -- | -- | -- | -- | -- |
| API key (required) | ApiKey() | GUID | 1789317-7837-71388932 | sc_apikey |
| Item (required) | Path() | Content tree path | /articles | item |
| Site name | SiteName() | Human readable name | MySite | sc_site |
| Language | Language() | ISO language code | en, en-GB | sr_lang |

### SitecoreLayoutResponse

The Layout Service return an object  instantiated from  **SitecoreLayoutResponse**. It consists of several parts:

- Request: The SitecoreLayoutRequest sent to the Layout Service.
- Matadata: response metadata such as HTTP response headers.
- Content: deserialized JSON response.
    - Route: maps to Route object in the JSON response.
    - Component: maps to objects in the list value of placeholder.
    - IField: Maker to identify the types that can be read through an IFieldReader.
        - CheckboxField.
        - ContentListField.
        - DateField.
        - FileField.
        - HyperLinkField.
        - ImageField.
        - ItemLinkField.
        - NumberField.
        - RichTextField.
        - TextField.
- Errors: list of errors.
- HasError: Errors lenght.

### Configuration

The **Layout Service Client** is part of the **Host Rendering Service** and it is config in the *Startup* class.

```cs
services 
  .AddRouting() 
  .AddMvc() 

  // Configure the required Newtonsoft.Json serialization behavior for use
  // with the Layout Service Client.
  // The Layout Service Client requires Json.NET due to limitations in System.Text.Json.
  .AddNewtonsoftJson(o => o.SerializerSettings.SetDefaults()); 

  // Register the Sitecore Layout Service Client,
  // which is used by the ASP.NET Rendering Engine.
  .AddSitecoreLayoutService() 

  // Configure the default parameters for Layout Service Client requests.
  .WithDefaultRequestOptions(request => 
  { 
    request 

      // Optional language configuration, if the application is not using localized routes.
      // .Language("en")

      // The name of the Sitecore site which this application is rendering.
      .SiteName("website")

      // The ID of the Sitecore Services Client API Key to access the Layout Service.
      .ApiKey("{00000000-0000-0000-0000-000000000000}");
  }) 

  // Provide the URL to the Layout Service on your Sitecore instance.
  // In production, this is typically a Content Delivery server.
  // In development, it might be a standalone combined Content Management
  // and Content Delivery instance.
  .AddHttpHandler("default", "https://<sitecore instance>/sitecore/api/layout/render/jss") 
  .AsDefaultHandler(); 

```

### API keys for the OData Item Service

You must pass a valid API key in each request to the OData Item Service. Otherwise the request fails.

The API key is the ID of an item that you create in the **master** database. In the content editor navigate to */sitecore/System/Settings/Services/API* folder, using the *sitecore/templates/System/Services/API key* template.

Once it is created, publish the item.

| field | description |
| --- | --- |
| AllowedControllers | A semicolon-separated list of controllers allowed to use the API Key, or "*" |
| CORS Origin | A semicolon-separated list of allowed origins. Example: *https://name-of-the-app; https://localhost6500* **For Azure Web Apps** check documentation. |
| Impersonation User | Anonymous users are impersonated as this user. Example: sitecore\User. By default value is comming from *Sitecore.Services.AnonymousUser* |

### Layout Service and Sitecore Placeholders

TO return an item's full structured layout data, the Layout Service must know the placeholders on a rendering.

Check the **Layout Service Placeholder** field in a rendering.