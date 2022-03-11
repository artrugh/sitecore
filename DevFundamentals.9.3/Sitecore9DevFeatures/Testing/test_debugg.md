## Testing and debugging in VS

### Testing

/View/ContentIndex.cshtml

```html
@Model Sample.Model.ContentModel

<div>
    <h1>@Model.Title</h1>
    <p>Lorem ipsum dolor sit amed</p>
</div>
```

/Model/ContentModel.csharp

```csharp
namespace Sample.Model { 
    public class ContentModel { 
        public string Title { get; set;} 
    }
}
````

/Controllers/BasicContent.csharp

```csharp
using Sample.Model;
using System.Web.Mvc;

namespace Sample.Controllers
{
    public class BasicContent: Controller
    {
        public ActionResult Index()
        {
        
        var title = RenderingContext.Current.ContextItem("title");

        if(string.IsNullOrEmpty(title))
        {
            title = RenderingContext.Current.ContextItem.Name;
        }

        var model = new ContentMode
        {
                Title = title
        };

        return View("/Views/ContentIndex.cshtml", model)
        
        }
    }

}
```

Refact the code to extract the business logic

```csharp
namespace Sample.Content
{
    public class BasisContentExtractor
    {
        public string ExtractTitle()
        {
            var title = RenderingContext.Current.ContextItem("title");

            if(string.IsNullOrEmpt(title))
            {
                title = RenderingContext.Current.ContextItem.Name;
            }

            return title;
        }
    }

}
```

Update Controllers

```csharp
using Sample.Model;
using System.Web.Mvc;
using Sample.Content;

namespace Sample.Controllers
{
    public class BasicContent: Controller
    {
        public ActionResult Index()
        {
            var extractor = new BasicContentExtractor();
            vat title = extractor.ExtractTitle();

            var model = new ContentMode
            {
                Title = title
            };

            return View("/Views/ContentIndex.cshtml", model)
        }
    }
}
```

Refact the controller using Dependency Injection.
It is easier to mock the dependency for testing purpose.

```csharp
namespace Sample.Content
{
    public interface IBasicContentExtractor
    {
        string ExtractTitle(Item item);
    }
}
```

Refact the BasicContentExtractor

```csharp
namespace Sample.Content
{
    public class BasisContentExtractor: IBasicContentExtractor
    {
        public string ExtractTitle(Item item)
        {
            var title = item["title"];

            if(string.IsNullOrEmpty(title))
            {
                title = RenderingContext.Current.ContextItem.Name;
            }    
            return title;
        }
    }
}
```

Update Controllers

```csharp
using Sitecore.Modules.WebBlog.Mvc.Model;
using Sample.Model;
using System.Web.Mvc;
using Sample.Content;

namespace Sitecore.Modules.WebBlog.Mvc.Controllers
{
    public class BasicContent: Controller
    {
        private IBasicContentExtractor _contentExtractor;

        public BasicConent(IBasicContentExtractor contentExtractor)
        {
            _contentExtractor = contentExtractor;
        }

        public ActionResult Index()
        {
            var item = Sitecore.Context.Item;

            vat title = _contentExtractor.ExtractTitle(item);

            var model = new ContentMode
            {
                Title = title
            };

            return View("/Views/ContentIndex.cshtml", model);
        }
    }
}
```

Register in Sitecore the dependent service, **the extractor**.

Therefore, it can be instantiated when required.

The BasicContentExtract and controller must be registered as services in the Sitecore IoC (InversionOfControl) container.

#### Unit testing Framework.

Create a new **Visual Studio Project**.

Create a new **Library projects** and add NUnit(v 3.12) and NUnit3TestAdapter (v 3.15.1) packages.

Create a **Class** to hold the tests for BasicContentExtractor and add the attr required by NUnit to mark it as a test class.

```csharp
using NUnit.Framework;

namespace Sample.UnitTest.ContentIndex
{
    [TestFixture]
    public class BasicContentExtractortest
    {

        public void ExtractTitle_ItemHasNoTitle_ReturnsItemName()
        {

        // Arrange

        var itemId = ID.NewId;
        var itemData = ItemData.Empty;
        var database = Substitute.For<Database>();

        var item = Substitute.For<Item>(itemId, itemData, database);
        item.Name.Returns("mock item");

        var sut = new BasicContentExtractor();

        // Act
        var result = sut.ExtractTitle(item)
        // Assert
        Assert.That(result, Is.EqualTo("mock item"));
    }

    public void ExtractTitle_ItemHasTitle_ReturnsTitle()
    {

        // Arrange
        var itemId = ID.NewId;
        var itemData = ItemData.Empty;
        var database = Substitute.For<Database>();

        var item = Substitute.For<Item>(itemId, itemData, database);
        item.Name.Returns("mock item");
        item["title"].Returns("the title");

        var sut = new BasicContentExtractor();
        // Act
        var result = sut.ExtractTitle(item);
        // Assert
        Assert.That(result, Is.EqualTo("the title"));
    }
}
```

#### Debugging

Attach to debug model to ensure you are attaching to your Sitecore site.

- In the nav click **Debug** and **Atach to Process...**
- Click the bottom checkbox "Show processes from all users"
- Filter fro "w3wp"
- Select the target process you want to attach to.
- Click Attach
- Reattach to process
