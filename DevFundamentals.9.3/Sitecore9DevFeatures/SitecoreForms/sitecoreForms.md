## Sitecore forms

They allows Digital Markets to collect information from visitors.

**Sitecore Forms analitycs** also provide improved visibility regarding the performance of forms and form-level reporting.

| Benefits | Description |
| -- | -- |
| Improved Security | Security of data using SSL encryption. There are some other General Data Protection Regulation |
| Seamless Data Storage | Collect and share all data in Sitecore |
| Streamlined Migration and Conversion Tools | It provides a preconfigured mapping of data from the database to the API, ensuring a streamlined migration process |
| Headless and JSS | All content is shared by the JSON API and can be personalized and tested |

### Typical Forms

- Contact us
- Login/SignUp
    - Fields: FirstName, LastName, Email.

### Set a Registration Form

#### Create a outer layout

1. create a view called Outer
2. right-click views => add => view
3. Copy and paste the entire code from default.cshtml to outer.cshtml.

```csharp
@using Sitecore.Mvc
@using Sitecore.Mvc.Presentation
@using Sitecore.ExperienceForms.Mvc.Html 
@model RenderingModel
// ...
    <head>
        ///...
        // support Form Functionalities
        @Html.RenderFormSyles()
    </head>
    <body>
    // the layout controls the body
        @RenderBody()
        <script src="˜/Project/js/clothingco-script.js"></script>
        // support Form Functionalities - should be before the body closing tag
        @Html.RenderFormScripts()
    </body>
//...
```

#### Modify default.cshtml view

```csharp
@using Sitecore.Mvc
@using Sitecore.Mvc.Presentation
@model RenderingModel
@{
    Layout = "outer.chtml";
}
<div>
    @Html.Sitecore().Rendering("{798179813-12379872431-23421323}")
</div>
<div>
    @Html.Sitecore().Placeholder("main")
</div>
<div>
    @Html.Sitecore().ControllerRendering("Footer", "Index")
</div>
```

#### Create a Form

In Sitecore Experience Platform

- Select Form on the Launchpad
- Click Create
- Click Blank
- Click Basic
- Drag fields
    - Single Line Text - Label: Name - Validation / field importance: Optional.
    - Single Line Text - Lable: Email - Validation / field importance: Mandatory.
    - Number - Label: Age - Validation / Importance: Optional - Range: Min 15, Max 150.
    - List-DropList, Label: Country - Static list: Germany, Spain, France.
- Drag Submit Button from Structure Category
    - change label to
    - Submit action: save data
- Save
- Clcik + Redirect to Page
- Select the page
- Click OK
- Save
- Give a Name
- Arrow => and Publish

#### Add a Mvc Form in Renderings

- Navigate to the item where the form was include
- open presentation details
- Share Layout
- Click Edit
- Click Controls and the click Add
- Click Renderings/Forms/MVC Form 
- add to placeholders
- Click select
- add a data source to control properties forms/contact us clicking browse

#### Create a Multi-Page Survey

In Sitecore Experience Platform

- Select Form on the Launchpad
- Create
- Click Blank / Form
- Click Basic
- Drag fields
    - Text - Text: Blog Survet - Html Tag: h2.
    - ListItems / List Box - Label: Question? - Listem Items: add new - Selection Mode: multiple
- Drag Submit Button from Structure Category
    - change label to Continue
    - Submit action: save data
- Drag Pge from Structure Category
    - change label to Continue
    - Submit action: save data
- Save
- Arrow => Publish