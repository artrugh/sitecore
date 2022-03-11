## Items

[visit](https://doc.sitecore.com/xp/en/users/101/sitecore-experience-platform/creating-and-editing-items.html)[]
[and][]https://doc.sitecore.com/xp/en/users/92/sitecore-experience-platform/managing-items.html

Items are the basic building blocks of the Sitecore website.

An item can represents any kind of information, templates, component definition items, placeholder settings items, etc.

```diff
+ Everything within the content tree in Sitecore is an item and receives a name and ID@@ 
```

All items are built and based on a [template][/DevFundamentals.9.3/Templates], that defines the **structure of data fields** that an item contains.

The creation of an item is not neccesary a creation of a page.

Items houses data and can be used as part of a page.

Howerver a typical scenario can be to create a Page Item based on a template.

An item always haas:
- name
- id
- based template

### Relations between items

- **Parent**
- **Sibling** same lavel items
- **SubItem** an item directly under the item
- **Ancestor** all the items that are above the item
- **Descendent** all the item that descend from the item

### Add an Item

#### Insert a subitem item

- in the content tree, navigate to the item where you want the new item.
- in the ribbon, select **HOME** and in the **Insert** group, click the dropdown array and select the item type you want to insert.

#### Insert a sibling item

- in the content tree, navigate to the item where you want the new item.
- in the ribbon, select **HOME** and in the **Insert** group, click the dropdown array and **Insert a new sibling**.
- Select the item type you want to insert.

#### Create an item based on a template

Using the ribbon

- in the content tree, navigate to the item where you want the new item.
- in the ribbon, select **HOME** and in the **Insert** group, click the dropdown array and **Insert from template**.
- Select the template.

Using the node in the content tree

- go to content/home
- right click in a Node
- click in insert <template-name>

from code

Use the correct database: MasterDB and check for permission.

```csharp
using(new UserSwitcher(@"sitecore/admin", false));
{
    var database = Sitecore.Configuration.Factory.GetDatabase("master");
    var template = database.GetTemplate("Sample/SampleItem");
    var parent = database.GetItem("/sitecore/content/Home");
    var newItem = parent.Add("my-item", template);
}
```

#### Create a new item by copying an item

- copy an item to another location
    - select the item you want to copy
    - in the **Operation** group, click **Copy to** or right-click the item in the content tree, click **Copying** and then **Copy to** 
    - In the dialog, select the location.

- duplicate an item to another location
    - select the item you want to duplicate
    - in the **Operation** group, click **Duplicate** or right-click the item in the content tree, click **Duplicate**
    - Enter the name for the new item and click **OK**

### Edit Items

- lock and unlock
- edit a field
- manage associated content
- 