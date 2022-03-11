## Content Search API

**Sitecore's search architecture** is based on a provider model.

When a query is created, Sitecore crawls the items in the content tree and **indexes** the field values of all the items.

ContentSearch API allows to write your search queries using **LINQ** statements.

Additionally you can set this search mechanism to find content from various databases (master, code, web).

### Create a Search using ContentSearch API

In Visual Studio

- Tools/Nuget Package Manager/Manage Nuget Packages for Solution
- add:
    - Sitecore.ContentSearch
    - Sitecore.ContentSearch.Linq

You can retrieve the necessary index from an item based upon the **current context**, otherwise the control will not work on both, **the website and in the Experience Editor**.

- SearchResultItem is available.
- GetQueryable LINQ
- the result is a list of items which contains the string
- you can use ToList() method to convert all the items into a list.

```csharp
// se;ect the index based on context using GetIndex
var Index = ContentSearchManager.GetIndex((SitecoreIndexableItem)Item);

// Set up the search context in a using block
// Open a connection to run a search and close it when the search has run
using (var context = Index.CreateSearchContext())
{

    // create the search using LINQ
    // search all the content within th master index that contains "hello, word!" as searcn parameter for the query
    var searchResults = context.GetQueryable<SearchResultItem>()
    .Where(s => s.Content.Contains("hello, world!"))
    .ToList()
    .Select(item => item.GetItem())
    .ToList();

}
```
