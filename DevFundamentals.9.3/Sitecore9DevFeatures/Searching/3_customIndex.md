
## Custom Index

By default, Sitecore index the whole app but you can index an specific template, item, field, etc.

A **custom index** is is a new index that you can customize to index only select fields, templates, etc.

Benefit:

Building a custom index decreases build time, making development much quicker.

Usage:

- to isolated some part of the **content tree** inside and index by itself.
- to bring **external data** into Sitecore so it is searchable within Sitecore.
- to **share indexes** to support large amounts of content.
- to define your **custom start** path so you do not have to index the entire content tree.

### Create a Custom Index

This is just a brief and simple description.

1. create a file **Sitecore.ContentSearch.Solr.Master.Templates.config** in
"C:\inetpub\wwwroot\<website>\App_Config\Include\folder" using the file explorer

2. copy file from sitecore documentation

    - Index id
        Index id setting identifies the name of the new index. The context of this file will be display in the **Sitecore Indexing Manager**.
        `<index id="sitecore_custom_index">`

    - Parameter description
        `<param desc="core">xp0-_custom_index</param>`

    - Configuration Ref
        declare default Sitecore index configurations
        `<configuration ref="contentSearch/indexConfigurations/defaultSolrIndexConfiguration">`

    - Index all field should be set to false
        `<indexAllFields>false</indexAllFields>`

    - Included Fields
        Set the field types to index
        Index the PageTitle field from _BaseTemplate.NETThe GUID of the item in between tags may change based on the instance.
        `<PageTitle>{templateId}</PageTitle>`

    - Included Templates
        Set the templates that you want to index.
        `<Product>{templateId}</Product>`

    - Database
        set the databse
        `<Database>master</Database>`

    - Root Path
        set the rootpath.
        `<Root>/sitecore</Root>`

3. create a master and web version of the custom index

### Add the new custom index to the **Solr**

1. Locate the Solr index folder that contains the xp0-_master_index
2. duplicate de folder and name it xp0-_custom_index
3. open the core.properties file
4. change name to xp-_custom_index
5. Save changes

6. view the new core using [solr](https://localhost:8983/solr)
7. click **Core Admin** in the left-hand bar.
8. click in xp0-_custom_index

9. Open the Control Panel in the Sitecore Experience Platforms
10. Scroll to indexing and click **Indexing Manager**
10. Select the new index sitecore_custom_index
11. click on rebuild

### Build a query that retrieves the new custom index

In Visual Studio

- Tools/Nuget Package Manager/Manage Nuget Packages for Solution
- add:
    - Sitecore.ContentSearch
    - Sitecore.ContentSearch.Linq

```csharp
// now you can get the custom index using the custom index name
var Index = ContentSearchManager.GetIndex("sitecore_custom_index");

using (var context = Index.CreateSearchContext())
{
    var searchResults = context.GetQueryable<SearchResultItem>()
    .Where(s => s.Content.Contains("hello, world!"))
    .ToList()
    .Select(item => item.GetItem())
    .ToList();
}
```