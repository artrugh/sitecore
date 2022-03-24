## Search Controller Rendering

- create a controller
- build the model
- add a view
- create the controller rendering

### Create the controller

1. right-click controller Folder
2. add controller
3. name it **SimpleSearchController**

```csharp
using System.Web.Mvc;
using Sitecore.Data.Items;
using System.Collection.Generic;
using Sitecore.Links;
using ClothingCompany.Models;
using Sitecore.ContentSearch;
using Sitecore.ContentSearch.SearchTypes;

namespace ClothingCompany.controllers
{
    public class SimpleSearchController: Controller
    {
        public ActionResult Index() {

            var searchList = new SimpleSearch();
            // gets the id value of the datasource item
            var capsuleWardrobeID = RenderingContext.CurrentOrNull.Rendering.DataSource;

            if(capsuleWardrobeID !== null)
            {
                var capsuleWardrobeItem = Sitecore.Context.Database.GetItem(capsuleWardrobeID);

                if(capsuleWardrobeItem !== null)
                {
                    // creating a search using ContentSearch API
                    var index = ContextSearchManager.GetIndex("sitecore_master_index");

                    using(var context = index.CreateSearchContext())
                    {
                        var mySearch = context.GetQueryable<SearchResultItem>()
                            // pull all the post that contains "2020" in the page title field
                                .Where(s => s["Page Title"].Contains("2020"))
                                .ToList()
                                .Select(item => item.GetItem())
                                .ToList();

                        searchList.ListOfItems = mySearch.Select(item => new CapsuleWardrobeItem
                        {
                            Item = item;
                            Url = LinkManager.GetItemUrl(item);
                        } ).ToList();
                    }
                }
            }

            return View(searchList);
        }
    }
}
```

### Build the models

1. right-click in Models Folder
2. new Item/ Sitecore Model
3. Name the model SimpleSearch

```csharp
using Sitecore.ContentSearch;
using System.Collection.Generic;
using Sitecore.Data.Items;

namespace ClothingCompany.Models
{
    public class SimpleSearch
    {
        public SitecoreIndexableItem ParentItem { get; set; }
        public IEnumerable <CapsuleWardrobeItem> ListOfItems { get; set; } = Enumerable.Empty<CapsuleWardrobeItem>();
    }
}
```

4. right-click in Models Folder
5. new Item/ Sitecore Model
6. Name the model CapsuleWardrobeItem

```csharp
namespace ClothingCompany.Models
{
    public class CapsuleWardrobeItem
    {
        public Item Item { get; set; }
        public string Url { get; set; }
    }
}
```

### Include a view

1. right-click Views/SimpleSearch => add view
2. set the name to Index

```csharp
@model ClothingCompany.Models.SimpleSearch;
@model ClothingCompany.Models.CapsureWardrobeItem;

<div>
    <h1 class="title">
    @Html.Sitecore().Field("__Display Name", Model.ParentItem)
    </h1>

    @foreach (var wardrobe im Model.ListOfItems)
    {
        <div>
            <figure class="image">
                @Html.Sitecore().Field("Primary Image", wardrobe.Item, new { disableWebEdit = true, mh = "150" })
            </figure>
            <a href="@wardrobe.Url">
                @Html.Sitecore().Field("Page Title", wardrobe.Item, new { disableWebEdit = true, mh = "150" })
            </a>
        </div>
    }
</div>

```

### Create the controller Rendering

1. right-click Layouts/Rendering/Feature
2. Add controller rendering
3. name it ContentSearch
4. add Controller: "ClothingCompany.Controllers.SimpleSearchController, ClothingCompany.Web".
5. add Controller Action: Index
6. Save

### Add Datasource for Rendering

1. In **Content Editor** navigate to the new controller rendering (ContentSearch).
2. add Data source: */sitecore/content/Home/Capsule Wardrobers*
3. Save

### Add Controller Rendering to placeholder

1. navigate to *Layout/Placeholder Settings* and click col-render
2. click Edit under allowed Controls
3. Add ContentSearch controller rendering to the col-center placeholder
4. click Ok
5. save