## Datasource over context item

A **datasource** is a **pointer** from your **definition item** to a **content item**.

This item can easily be picked from a global or local placement in the content tree.

You can still navigate from the datasource to other items (like subitems) if you want a more complex structure for your content.

Using **datasources** over the **context item** is the foundation for Sitecore personalization.

Use datasource as often as possible if the component is used to **personalization** or is **reusable**.

### Get datasource

1. where to get the data from the **current context item**

    ```csharp 
    var dataSourceId = RenderingContext.CurrentOrNull.Rendering.DataSource; 
    ```

2. go directly to the **datasource** itself, but if the value of data source is null, the core stops executing before the .Rendering.Item to avoid an Exception

    ```csharp
    var datasource = Sitecore.Context.Database.GetItem(dataSourceId); 
    ```

3. RenderingContext allows the call to have a **null value without throwing an exception** if the datasource is not set by default, it returns the current item.

    ```csharp
    var dataSource = RenderingContext.CurrentOrNull?.Rendering.Item;
    ```

4. You need to refer a data field in the current context

    ```csharp
    Item currentItem = RenderingContext.Current.ContextItem;
    ```

Example: how to get the datasource of the home/item

```csharp
Item homeItem = Sitecore.Context.Database.GetItem("/sitecore/content/Home");
Item homeItem = Sitecore.Context.Database.GetItem(Sitecore.Context.Site.StartPath);
```

### Set datasouce in a Rendering


By default, renderings read data from the current page, but can be set to read information from the data source item instead.

This means that the content they display is not bound to the page on which they appear but is **stored in data source items**.

| Field | Value |
| --- | --- |
| Datasource Location | specify where the user is allowed to look for the data source. |
| Datasource Template | specify the types of data sources users can create. |
| Data source | specifies a data source item. |

1. Set the datasource for a renderings:

- go to sitecore/layouts/renderings folder
- select the **rendering definition item**
- scroll to **datasource location**
- click on Insert Link
- insert a locaction of a folder
- save

2. Provide restriction in the type of items that can be selected at data source for the rendering without limiting the content author:

- go to renderings Folder
- select the rendering definition item
- scroll to **datasource template**
- click on Insert Link
- select a template
- Save

