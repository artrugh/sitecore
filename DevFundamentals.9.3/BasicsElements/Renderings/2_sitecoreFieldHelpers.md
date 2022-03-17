## Sitecore MVC HTML Field Helpers

Sitecore is built using **ASP.NET** and utilizes **Model View Controller** [MVC.](https://ecs.syr.edu/faculty/fawcett/handouts/cse686/presentations/MVC_Conventions.pdf)

You can use **standard MVC** for building Sitecore components.

However, it is not a Author friendly approach and lacks flexibility and functionality when pair with the Sitecore platform.

Instead you should use **MVC HTML Field Helpers**.

When the .Field HTML Helper encountered in **Experience Editor**, the data field that is rendered is wrapped in an **editable frame**.

These **HTML Helpers** work as building blocks for making reusable components that render content from within Sitecore.

Only some fields can be rendered as editable within the **Experience Editor**, means, they are in-line editing.

- Text fields
  - single line
  - multi line
  - rich text
- Image field
- Data field
- Datatime field
- General link field

The other fields aren't support for in-line editing in the Experience Editor because there is not standard for rendering.

```csharp
@Html.Sitecore().Field("FieldName")
```

By default the HTML helper renders the content of the data field from the current item (context item).

A data source or another content item can be used.

```csharp
@Html.Sitecore().Field("FieldName", itemObj)
```
itemObj: data source item for the field (article page or content object).
fieldName: specific targeted data field on that item (page title, image field).

### Sitecore Helper Parameters - Optional Anonymous Objects

1.   
  ```csharp
  @Html.Sitecore().Field("FieldName", itemObj, new { DisableWebEdit = true})
  ```

  It prevents the field from being editable in-line when rendered in Experience Editor.
  It protects the field from inline-editing

2.  
  ```csharp
  @Html.Sitecore().Field("FieldName", itemObj, new { EnclosingTag = "div"})
  ```

  It is usuful for fields that may not contain data, without explicity setting it within the code. It prevents empty div when the is an empty field.

3.  
  ```csharp
  @Html.Sitecore().Field("DatatimeFieldName", new { Format = ".NETstring"})
  ```

  You can use .NET formatting string for Data and Datetime fields.

4. 
  ```csharp
  @Html.Sitecore().Field("ImageField", new { @class = "cssClass"})
  ```

  It modifies image and anchor tags with a class attribute.
  It works with any HTML tag that will be rendering as a wrapper on the content.

### Sitecore Helper - BeginField and EndField

5. 
  ```csharp
  @Html.Sitecore().BeginField("FieldName") @Html.Sitecore().EndField("FieldName")
  ```

  They are used by link fields, to put custom content within a link wrapper.

### Sitecore Helper - FieldRender

6. 
  ```csharp
  FieldRender.Render()
  ```

  All HTML Helpers call this method at the API level.
  You can use it withing MVC Controller to render the content of a data field to a string value.

  It is a way to turn a data field's content into a variable's content to be manipulated in code.

### Sitecore Helper - Additional Image Paramaters

- mw / max width
- mh / max height
- w / width
- h / height
- as
- bc / background color