## Templates

Topics:
- Templates
- Standard Values
- Insert options

[Main Docu](https://doc.sitecore.com/xp/en/developers/102/sitecore-experience-manager/data-templates.html)

Content tree path: **sitecore/Templates**

Everything within the content tree is an item, and all items are built from templates.

Because of that, the first step before creating any item, is to create a template.

The item will be based on the created template, creating a **strong dependency**. The dependency will be even greater if the data template has a defined **layout** and **content** in standard values (it is cover in other sections).

A templates can be shared between differents items. Those items will have common fields.

A **data template** can be used to model anything, from a page to a set of configurations.

> Create data structure means:
> 1. create data template in Sitecore,
> 2. define standard values,
> 3. assign insert options,
> 4. create content items,

The template has nothing to do with the **presentation of content**, it determines the **structure of the content**.

- **Data templates** structure the data of all the items you create in Sitecore and define the behavior of other items.
- They allow to logically group data together into field sections and fields.

1. Create a Template
2. Build an item

Every change to a template will propagate to all the items which have been built based on this template.

Template and items have a strong dependency or association. All **content items** are based on templates.

That means that an item is **heavily dependent on that original template association**.

```diff
+ Group templates into folders is a best practice, avoid confusion and improve easy access.
```

`*Important:** All template must be created in the **Master database**, not the Web or Core databases`

### Templates Types

- **Data template** defines fields used to control how data is entered (field sections, field types and field names).

- **Branch templates** enable to create a set of items rather than a single item, using a reusable, predifined structure. It consist of a branch template definition item. Instead of apply the same single values to all items based on the **branch template**, Sitecore duplicates field values to each item created using it.

  - use a branch template to:

    - copy initial field values into a created item, rather than inheriting them from the standard values. This includes both field values for the Standard template fields and fields defined in cutom adta templates.
    - insert multiple items.
    - assign access rights to inserted items.
    - control which accounts can insert items using the branch template.
    - provide **Content Author** with the ability to create multiple items at once., the corresponding field in the new items contains its standard value.

  - process
    - copies the descendents of the branch template definition item, including field values, to create new items.
    - performs token substitution on the new items, replacing `$name` and other tokens whith item name entered by the user when he creates an item based on this template .
    - for any field not overriding its standard value in the branch template, the field in the new items contains its standard value.

- **Command templates** allow to insert items using logic rather than a predefined structure.


### Template Fields

Excluding the **binary components of database media**, Sitecore stores all field values as text. Some field types, as **single-line** is store as simple text value, but others, **Multilist** stores the GUIDs of the selected Sitecore Items separeted by pie charecters ("|"). Complex types, like **Image** are stored as **XML** element.

- **Field sections**

  - Groups of fields withing a Template.
  - Key user interface feature when building and using templates because they provide structure and organization for fields.
  - All fields withing a template are grouped into specific, collapsible sections to allow you to more smoothy navigate and make changes to the content contained with an item's template.

- **Fields names**

  - names you give to fields to indentify their purpose.

- **Fields types**

  - It determines the UI component Sitecore presents for that field in user interfaces **Content Editor and Page Editor**.
  - It indicates what forms of content value a **Content Author** can include in that field.
  - It determines the .NET classes and programming techniques developers use to access the field value in the classes and HTML helpers, such as in the `Sitecore.Data.Fields` namespace.

- **Fields sources**

  - Contain the location of content, defined by a path or GUID. The use of the field source depends on the fields types, and many field types use the field source to define the root item from which to show options.
    - Not all fields will required a field source. However, to have it, allows a Content Author to choose from specific item in a defined list.
    - They are using in different ways:

      - For fields that allow a content author to define the location to generate a list of items users can choose from in real-time. The field source is used to configure the source of choice given to the editor.
      - For an image/file field, the field source defines the browsing location in the Media Library.
      - For a Rich Text field, the field source is used to configure the buttons in the toolbar for the HTML editor

- **Icons**

  - They are used to indetify and organized templates. However

#### Field types

Fields types are grouped:

- Simple
Select an individual value.
- List
Select one or multiply values.
- Link
  Allows to store a reference to other item. You can classify them according to whether they store a link to a single item or multiple items.

  - General Link: store a link to an internal or external site or email addresses
  - Link enable to enter links to Sitecore internal items, external URLs, anchors, and email addresses

- Developer field types.
- System field types.

Sitecore internal items should follow this path: /sitecore/...

Two of the most used Fields are:

- Text Fields
  Store only text
  - Single-Line text
  - Multi-Line Text
  - Rich Text field types stores an HTML fragment and provides an interface for the content author to enter HTML wihout having any technical know-how.

- Media Fields
  Store **reference** to a **media asset** and also store the reference in Sitecore.
  - image
  - movie
  - audio

### Template Inheritance

Data templates support sequestial and multiple inheritance.

Templates can inherits from other templates, which means that when the parent template changes, all the children templates will change.

Templates inherit sections and fields from one or more **base templates**, and all fields are merged.

If a template doesn't expecify a base template it inherits from the default **standard templates**. Which menas that **explicity or implicity** all data templates inherit from the **standard templates**.

The **standard templates** defines sections such as security and workflow relevant to all types of items.


- How to set a **base template**?

In Content Editor:

1. Select the Template
2. Click **Options Builder** on the ribbon
3. Base template
4. In the dialog, select the template you want to use.

### Standard Values

**Standard values** is an item inside a **template**.

Standard value represents the **default values** of a field when a template is created.

The purpose is to store and display those default values if a **field is not filled in by a Content Author**.

All items based on data template automatically inherit and contain the template's standard values, which are defined by an item named `_Standard Values`

Standard values are backups, not actual values.

#### Set standard values

In Content Editor:

1. Select the Template
2. Click **Options Builder** on the ribbon
3. Standard Values
4. Set default Values

**If a standard is unique (ex, title), use a token.**

```
$title
```

- How does a token work?

When the item is created, it inserts the name that the user assign to the item. When the value is changed by the content creator, the value is not overwriten.

#### Modify standart values

In visual studio:

- navidate to the page into templates
- right click => create standart values
- can add or edit the standart values for the template in the prompt
- save changes


