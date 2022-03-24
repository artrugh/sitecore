## Listing Component

### Model

```csharp
using Sitecore.Data.Items;
using System.Collection.Generics;
using System.Linq;

namespace ClothingCompany.Models
{
    public Item ParentItem { get; set; };
    public IEnumerable<NavItem> Posts { get; set; } = Enumerable.Empty<NavItem>();
}
```

### Controller

```csharp
using Sitecore.Web.Mvc;
using Sitecore.Mvc.Presentation;
using Sitecore.Links;

namespace ClothingCompany.Controller
{
    public class ListingController: Controller
    {
        public ActionResult Index()
        {
            var dataSourceId = RenderingContext.CurrentOrNull.Rendering.DataSource;

            var pageList = new Listing();

            // the listing is pulling from a data source instead of the current context item
            // can throw a rendering error
            // to avoid error when the datasource hasn't been selected yet
            if(dataSourceId != null)
            {
                // get the specific item
                var dataSource = Sitecore.Context.Database.GetItem(dataSourceId);

                if(dataSource != null)
                {
                    var listOfArticles = dataSource.Children;
                    pageList.Post = listOfArticles.Select(item => new NavItems
                    {
                        Item = item;
                        Url = LinkManager.GetItemUrl(item);
                    }).ToList();
                }
            }

            return View(pageList);
        }
    }
}
```

### Add View

- Click on View(pageList) to Add a View
- Click Add
- Check that use a layout page checkbox is not selected
- Visual Studio will create automatically a View file in View Folder

```csharp
@model ClothingCompany.Models.Listing;

<div>
    <h1>
    @Html.Sitecore().Field("__Display Name", Model.ParentItem)
    </h1>
    <div>
        @foreach (var article in Model.NavItems)
        {
            <div>
                <a href="@article.Url">
                    <figure>
                        @Html.Sitecore().Field("Primary Image", article.Item, new { disableWebEdit = true })
                    </figure>
                    <div>
                        @Html.Sitecore().Field("Page Title", article.Item, new { disableWebEdit = true })
                    </div>
                </a>
            </div>
        }
    </div>
</div>
```

### Component Definition Item

1. right-click to *Layout/Renderings/Feature*
2. Add new Item
3. Search for controller
4. Select Controller rendering
5. Name the component definition with the same name Listing
6. Add ControllerAction to Index
7. Add the using path in the controller and include where the solution is included (ClothingCompany.Controllers.ListingController, ClothingCompany.Web)
8. save
9. Build the solution

### Add the Controller to the Placeholder

1. go to *sitecore/Layouts/Placeholder Settings*
2. Select the placeholder you want
3. Scroll to the edit section
4. Add the new definition Item from *sitecore/Layouts/Renderings/Feature/Listing*

### Select the data source

In the Experience editor

- Add here
- Select Listing
- Click in More Option
- Edit Component properties
- Data Source is Empty
- Click Browse
- Expand *Content/Home*
- Select Blog Posts
- Click Ok