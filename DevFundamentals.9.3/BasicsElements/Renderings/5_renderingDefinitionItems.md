## Rendering or component definition items

They are **data items** called **definition items** that configure and registry the presentation of **render or layout** and have a direct relationship with the impementation and business logic in the code (MVC).

Those **definition items** are store in sitecore/layout/renderings/ in the content tree.

### Fields

- Data/Path: path to the component.cshtml or layout.cshtml
this path is located in the webroot folder for view renderings.

Additional fields for **controller components**

- Data/Controller: path to the controller and solution. It indetifies the controller's namespace and solution file.
- Data/ControllerAction: Name of the controller action method from the controller. It indentifies the action view.

**Commmon fields**

- **comparable renderings**, allows Content Authors to select other rendering to replace the current rendering.
- **editable checkbox** make a component non editable.

[Datasource](3_dataSource.md) is also defined in the **component definition item** datasource field.

Select the **data source** as a default source, if the current context item is not a valid data source for that component. This option is very useful for those permanent components and static renderings that need to have the same data source throughout the site.

- **datasource location**, limits where a **Content Author** can select the data for a component.
- **datasource template**, restrict the use of data for an **specific type**.