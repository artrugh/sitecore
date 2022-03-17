## Binding components

There are two ways to bind the component to the presentation:

- statically
- dynamically

### Statically binding rendering to the layouts or a component.

It is useful for components such headers, navigation, and footers that **need to be protected** from **accidental editing**.

Its content can not be moved or removed by Content Authors or Designers.

Reference the **component definition item** within the Sitecore content tree.

```csharp
@Html.Sitecore().Rendering("{781397983473-sd2323-342543544}");
// perform slower cause it has to solve the ID before displaying the rendering
@Html.Sitecore().Rendering("/sitecore/layout/Rendering/Structure/Header");
// alternitably you can add new data source
@Html.Sitecore().Rendering("/sitecore/layout/Rendering/Structure/Header", new { Datasource = "sitecore/content/home"});
```

This method doesn't require a **component definition item**

```csharp
@Html.Sitecore().ViewRendering("˜/sitecore/ClothingCo/Structure/Footer.cshtml");
// perform slower cause it has to solve the ID before displaying the rendering
// two params: controllerName and Action
@Html.Sitecore().ControllerRendering("FooterNav", "Index");
```

### Dynamic binding rendering (Placeholder)

Placeholders allow **Content Author or Designer** to add and remove components from a page.

- Static pladeholder
    ```csharp
    @Html.Sitecore().Placeholder("key-value");
    ```

- Dynamic placeholder assing components to the placeholder.
    ```csharp
    @Html.Sitecore().DynamicPlaceholder("key-value");
    ```

The **key** is the marker for assigning components to placeholders.

It is needed to create a **placeholder settings** with the same name in the **Content Editor**:
Sitecore/layout/Placeholder Settings


