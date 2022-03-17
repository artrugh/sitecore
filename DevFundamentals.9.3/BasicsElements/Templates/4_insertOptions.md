## Insert options

Content Authors need to be able to add **child items** based on templates, to the content tree, such as pages.

**Insert option** determines what child items a **Content Author** can add below a template on the content tree.

This capability should be implemented, restricting the ability to add an item into an specific node or folder.

If **insert options** are not set, it will never be possible to create an item based on a template.

For that, developers should determine which fields and fields types are required for a particular page or module.


```diff
+ Insert options can be set on any item within the content tree, but it is recommended practice to set Insert Options on a template's standard values@
```

### Settings

In Visual Studio:

- right-click in the Standard Values

In content editor:

Create the ability to add an item based on an specific template in the content node.

- right-click sitecore/Content/Home
- Insert Folder
- name folder Authors
- select the Authors folder
- go to configure tab and select Assign
- Select the template u want and add it with the arrays
- you can also remove the ability to create a new folder from the options using the arrays
- Look at the insert option in the sitecore/Content/Home/Authors
- the template is already included

Restrict the items they can been created from a template:

- select the Standard values from a template
- go to configure tab and select Assign
- Select the template u want and add it with the arrays
- you can also remove the ability to create a new folder from the options using the arrays
- select Home node
- Configuration/Assign
- Go to the template
- remove Sample Item
- Look at the insert option in the sitecore/Content/Home
- the template you have selected can be already included

Add path to templates fields from content/home

- click in the template field
- add manually the path
- click in the item in home/content
- the option should be on the dropdown in the item in home/content/item

