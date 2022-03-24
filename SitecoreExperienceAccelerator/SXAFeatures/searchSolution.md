## Search Solution

### Terminology

- Facets

It is used to refine search results by categorizing the items returned by the search.

| Facet | Component |
| -- | -- |
| Date | Filter (Date) |
| Distance | Filter (Radius), Location Finder |
| Float | Filter (Managed Range), Filter (Range Slider), Filter (Slider) |

You can add facets to a site /Sitecore/content/Tenant/Site/Settings/Facets

- Scopes

Search scopes are used to limit the search results based on conditions.
You can build a query that checks and limits for multiple conditions.

You can add facets to a site /Sitecore/content/Tenant/Site/Settings/Facets/Scopes

- Tokens

They are used in search queries to apply additional search filters.

- Pagination

It is the process of spliting the contents of a website. In SXA, the pagination rendering allows to add pagination to a Page List, Event List, and File List renderings.


### Search renderings

- Search box rendering

By default, the Search Box rendering adds the search text box to the page. As an administrator, you can create and customize search boxes for campaign pages using the **Control Properties dialog box** of the rendering (result signuture, target signature, scope, max).

In Experience Editor

1. Drag the search box from the toolbar
2. Select create
3. Name it
4. Click on the settings icon
5. Edit the rendering
6. Click on control icon and edit the Search criteria

- Search result rendering

Enble visitors to view their search results. You can configure the search results.

In Experience Editor

1. Drag the search result from the toolbar
2. Select the associated search box
3. Click on the settings icon
4. Edit the rendering
5. Click on control icon and edit the Search criteria

When working with **Search result rendering** you can use the variant selector to change the look and feel of diplayed results.

Create a custom Search result rendering

In Content Editor 

1. navigate Content/Home/Presentation/Rendering Variants/Search Results/
2. Insert Variant Definition
3. name it
4. right-click on the new variant definition anc choose Insert Section
5. right-click on the new section definition anc choose Insert Field
6. name it row
7. add field name
8. right-click on the new variant definition anc choose Insert Section
9. name it column
10. right-click on the new section definition anc choose Insert Field
11. name it title
12. right-click on the section / sorting / sort first
13. right-click on the new section definition anc choose Insert Field
14. name it text
15. customise the sections
16. Go to the experience editor and click on variant
17. Select the custom search result rendering


- Page Selector rendering

Choose how to display the search results page.

1. Drag the page selector from the toolbar
2. Select create
3. name it
4. Click on the settings icon
5. Edit the rendering

### Search settings

Create scopes

- In content editor

1. Content/Settings/scopes
2. right-click on Scope and add Scope
3. name it
4. on the field scope query
5. click build query
6. delete the exiting searchbox text
7. choose a template
8. click on search icon
9. click ok and Save

- In the experience editor

1. click on the control icon in the search box and in the search result
2. scroll to the search criteria section
3. select the scope
