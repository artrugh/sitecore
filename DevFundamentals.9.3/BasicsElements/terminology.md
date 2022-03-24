## Sitecore terminology

- content tree
- item
- templates
- placeholder
- layout
- rendering
- database

> Data definition: **Templates**, Content: **Items**, Presentation: **layout and components**.

### Content tree

Organizational system that houses items in a hierarchical structure.

- - -

### Item

> Everything within the content tree in Sitecore is an item and receives a name and ID.

An item is a building block and the basic unit of content and organization in Sitecore.

All items are built from a template that defines the structure of data fields that an item contains.

- - -

### Template

A template is an item which defines the **data structure** of other items, which are not templates items, such as content items or page items.

A template allows to define structured content types using **field section** and **fields**.

Each field has a specific **data type** that defines how it is presented or how it is stored.

Templates can optionally include these settings:
- **standard values** where default field values are set.
- **insert options** are setted in the **standart values** and define the type of **content items** that content author can insert as a child of an item based on this template. Basically, they allow **Content Author** to add **content**.
- **presentation details** are used to assign default layout details for all items based on a data template. They store the necessary information to render a page when a called is made from a site visitor.

- - -

### Layout

Layouts defines the shape of the **rendered appearence** for an item, when it is shown to a site visitor.

An example of a layout, can be a page shell with a header and a footer.

Layouts have two parts:

- an **definition item** which registers the layout in Sitecore.
- an **implementation** of the layout created by a developer, that defines the markup to use, and is written in a a Razor.cshtml.

Layouts can expose one or more placeholder.

You can assign a layout to a template, which makes that template a **page type** using the frame provided by the layout.

- - -

### Placeholder

It is the Sitecore's way of identyfing and naming a **position in the markup of a page**.

It allows **content authors** to dynamically add **content components** within the Experience Editor.

A placeholder is identified by a unique attribute: **the placeholder key**.

- - -


### Rendering

It defines an **individual content component** that can be added to a placeholder, such as a *accordion* or a *Two Column Content*.

```diff
+ Placeholder can be defined on a layout, but Renderings may also expose additional placeholder to create layout hierarchy.
```

A rendering has two parts:

- **rendering item** registers the rendering with Sitecore.
- **code implementation** includes component logic and markup.

There are two types of renderings:

- View Renderings
    **Razor views** that contains a default model provided by Sitecore and have any controller.

- Controller Renderings:
    They follows [ASP.NET MVC Conventions](https://ecs.syr.edu/faculty/fawcett/handouts/cse686/presentations/MVC_Conventions.pdf)

A Controller Rendering invokes an **action method** of type *Action Result* on an MVC controller to produce the component markup. This method returns Controller.View.

- - -

### Databases

Sitecore stores content in databases and each database contains a completely independent tree and item data.

There are two main databases:

- Master
    It stores all versions of content, published and draft.
    Content Authors view the master database when they write content.

When new content is published, Sitecore synchronizes the content tree from the **Master database** to one or more **publishing databases**. The most common is the **Web database**.

- Web databases
    It store the latest published version of the master content.
    Sitecre visitors see content delivered from the Web database, which only contains approved and published content.

- - - 

| item type | settings items name | location in the content tree | description |
| -- | -- | -- | -- |
| layout and component | rendering definition item | *sitecore/layout/rendering* |
| content item | insert options | *sitecore/template/standart values* |
| placeholder items | placeholder settings | *sitecore/layouts/placeholder settings* | set a key and the rendings (allow controls) that are allowed to be included |
| layouts | presentation details | *sitecore/template/standart values* | define what will be presented to the visitor after a page request |