# Controller rendering

A controller rendering uses RenderingModel or a custmon Model which follows the MVC pattern.

They are made by:

- Custom Model
- Controller
- View
- Static bind controller rendering

# Create the custom Models you need. 

1. right-click model Folder
2. Add new item
3. Select Class
4. Write your custom model

```csharp
using Sitecore.Data.Items;

namespace ClothingCompany.Models
{
    public class NavItem
    {
        public Item Item { get; set; }
        public string Url { get; set; }
    }
}
```

```csharp
using System.Collection.Generic;
using Sitecore.Data.Items;

namespace ClothingCompany.Models
{
    public class NavGroup
    {
        public Item RootItem { get; set; }
        public string RootUrl { get; set; }
        public IEnumerable <NavItem> NavItems { get; set; }
    }
}
```

# Create the controller.

1. right-click controller Folder
2. Add Controller
3. Select MVC file Controller
4. Add
5. Name following the convetion NameController

```csharp
using System.Web.Mvc;
using Sitecore.Data.Items;
using System.Collection.Generic;
using Sitecore.Links;
using ClothingCompany.Models;

namespace ClothingCompany.controllers
{
    public class NavigationController: Controller
    {
        public ActionResult Index() {

            Item homeItem = Sitecore.Context.Database.GetItem(Sitecore.Context.Site.Start);

            IEnumerable<NavItem> GetNavItems (Item navRoot)
            {
                var items  = new List<Item> { navRoot };

                // each item in those childrens descens from different Templates
                // we need to get only ones which descends from the contentPage Template,
                // because all the base pages are created base on this template
                // we don't want to include those items which were created based on other templates
                // we want the top level navigation 
                items.AddRange(navRoot.Children.Where(x => x.DescendsFrom( new Sitecore.Data.ID("7913427942-u97813789213-123479821374"))));

                var navItems = items.Select(item => new NavItem
                {
                    Item = item;
                    Url = LinkManager.GetItemUrl(item);
                }).ToList();

            }

            var navigation = new NavGroup
            {
                RootItem = homeItem;
                RootUrl = LinkManager.GetItemUrl(homeItem);
                NavItems = GetNavItems(homeItem);
            }

            return View(navigation);
        }
    }
}
```

6. Click on View(navigation) to Add a View
7. Check that use a layout page checkbox is not selected
8. Click Add
9. Visual Studio will create automatically a View file in View Folder

```csharp
@model ClothingCompany.Models.NavGroup

@foreach (var navItem in Model.NavItems)
{
    <div>
        <a href="@navItem.Url">
        @Html.Sitecore().Field("__DisplayName", navItem.Item, new { disableWebEdit = true })
        </a>
    </div>
}
```

# Include the new Controller Rendering into the header view

```csharp
using Sitecore.Mvc;
using Sitecore.Presentation;
using RenderingModel;
@{
    var homeItem = Sitecore.Context.Database.GetItem(Sitecore.Context.Site.StartPath);
}

<nav>
    @Html.Sitecore().ControllerRendering("Navigation", "Index")
    <div>
        <div>
        @Html.Sitecore().Field("__Display Name", homeItem, new { disableWebEdit = true })
        </div>
    </div>
</nav>

```