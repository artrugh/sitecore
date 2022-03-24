## Sitecore Layout Services

There are two services:

- Layout Service which is in **Sitecore Headless Services**
    The Sitecore Headless Services includes the **Sitecore Layout**.
    The Layout Service is an **endpoint** that provides **JSON formatted Sitecore content**.
    It communicate with the **Layout Service Client**.
- Layout Service Client which is in the **Rendering Host Service**

Those two services communicate throug an **endpoint** using **query string key**.

### Sitecore Layout Request

The **Layout Service Client** generates a **Sitecore Layout Request** which instantiated a **Data Transfer Object** (DTO) and contains properties.

| property | method | content | sample | query string key |
| -- | -- | -- | -- | -- |
| API key (required) | ApiKey() | GUID | 1789317-7837-71388932 | sc_apikey |
| Imte (required) | Path() | Content tree path | /articles | item |
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