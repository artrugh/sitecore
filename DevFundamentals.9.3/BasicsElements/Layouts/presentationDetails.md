## Presentation Details

A Layout needs **presention details** which store the **necessary information** to render a page when a called is made from a site visitor.

**Presentation details** for templates are only neccesary on templates used to create **content items** that will rendered directly as pages in the website.

Items created based on a template, inherit the standard values, **including presentation details**, and **NULL fields default** to the template standard values.

**Presentation details** should be set on the **standard values of templates**.

Which means that each resulting item in Sitecore created from that template will have the selected layout.

However they can also be set or edited in the layout item itself, overwritten the inheritance from the template.

### Adaptative approach

Sitecore offers device detection.

**Adaptative approach responses** can send different layout depending on the device detected through **devices options** <sitecore/Layout/Device>.

Sitecore already includes, default, print and feed, but you can create new device options in <sitecore/Layout/Device>.

In the presentation details of an item, you can set an specific layout for each device.

- Select standard values from a template
- On the **presentation tab** from the ribbon click **details**
- The **Layout Details** dialog will open. 
    - Shared Layout
        - **In Sitecore you can have numbered and language versions of items**
        - all version an languages from an item.
        - see the settings from the standard values of the templates.
        - you can edit the layout that appply to all the verions of the item.
        - the presentation details are stored in the _Rendering field
    - Final Layout
        - you can edit the layout details for the lenaguage version of the item.
        - the presentation details are stored in the _Final Rendering field
- Click reset
    - Return a content item to the default set on the standand values of the template.


Important:
When **Content Authors** change the presentation of items, they override the **presentation details**. Sitecore creates a **Layout Delta** in the background. The changes are, by default, only made for the current numbered and lenaguage version of the item. The **Layout Delta** changes are visible in the **Final Layout** of an item, which only shows the changes for the default.