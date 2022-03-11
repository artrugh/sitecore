# View Rendering

## Create the View Rendering

1. right-click in the View Folder
2. Add new Item
3. Select Sitecore View Rendering
4. Name it
5. In Visual Studio you will get a prompt to set the **definition Item** to the new view
6. Select sitecore/layout/Renderings/Feature/
7. Click Ok
8. Write your new Rendering

```csharp
using Sitecore.Mvc;
using Sitecore.Presentation;
using RenderingModel;
@{
    var authorItem = ((Sitecore.Data.Fields.ReferenceField)Model.Item.Fields["Author"]).TargetItem;
    var homeItem = Sitecore.Context.Database.GetItem(Sitecore.Context.Site.StartPath);
}

<article>
    <figure>
        @Html.Sitecore().Field("Author Image", authorItem, new { disableWebEdit = true })
    </figure>
    <div>
        <h2>
         @Html.Sitecore().Field("Author Name", authorItem, new { disableWebEdit = true })
        </h2>
        <h6>
        @Html.Sitecore().Field("Author Bio", authorItem, new { disableWebEdit = true })
        </h6>
    </div>
    <div>
        <p>
         Posted: @Html.Sitecore().Field("Date Time")
        </p>
        <p>
        @Html.Sitecore().Field("Primary Content")
        </p>
    </div>
</article>
```

## Add the new Component to the Experience Editor

1. go to sitecore/Layouts/Placeholder Settings/
2. Select the placeholder you want
3. Scroll to the edit section
4. Add the new definition Item from sitecore/Layouts/Renderings/Feature/NameOfTheDefinitionItem
