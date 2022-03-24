## Layouts

Sitecore layout and sublayout are primary used to structure pages with the outer HTML markup. 

A sublayout refers to a Sitecore rendering which defines a part of the overall page HTML layout and should not be confused with webforms sublayout rendering.

Layouts and sublayouts (in MVC, defined as view layouts, view rendering, and controller renderings) beling in Project layer modules.

They typically control the overall page design and contain site or porject-specific markup.

Minimize the number of layouts and sublayouts in your solution by dinamically assembling the pages in layout definitions and using the asset management techniques.

As a rule, it is usually sufficient to have just a single layout per site type or project medule.

## Renderings

Renderings typically belong to the Feature layer modules as they are connected to business features int the solution. Only sublayout style renderings should cocur in the Project layer.

The business-centric pattern prioritize maintainability and simplicity over reusability.

### Naming convention

- align th rendering item name with the .cshtml file name.
- favor Editors over Developers, avoid CamelCase and don't use abbreviations.
- set display names to support languages.
- Partial view renderings should be prefixed with the underscore (_) to separate them from the views references through Sitecore items or controllers.

### Renderings Files

- place the view rendering files in subfolders under views named after the module to which they belong.

### Rendering parameters

- rendering pareameter templates should be managed in the same module as the code that uses them.
- if it is in Foundation layer module, then any rendering parameters template in a Feature module can derive its template from Foundation modules and include all parameters in the rendering.

### Compatible renderings

They can share same data source and wheter you can place them in the same placeholder. They should be placed in the same module.

### Datasource template field

- It controls which types of items aer allowed as Datasource items for the rendering.
- It designtes the template used for new items created through the data source dialog.

### Datasource locations

- It specify one or more content locations where editors can select content for the rendering.
- Content allways belong to the Project layer.

### Positioning placeholders

- Dynamic assembly of page layouts either by enabling the editors to design specific pages or by letting Administrators create predefined variotions of layouts on page Type templates.
- Placeholder settings always belong on th Project layer module.
- Avoid putting placeholder in Feature layer renderings.
