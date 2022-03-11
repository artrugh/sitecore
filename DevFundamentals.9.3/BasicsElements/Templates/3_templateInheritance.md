## Template Inheritance

Template inheritance ensures **template reusability**.

It allows to share **fields**, **standart values** and **presentation details**, from one or more base templates, and makes edits in a single location to promote **maintainability**.

`Important: if a template inherits from two templates, and both have presentation details, the new template will only use the presentation details from the first template. That means that a template can only inherit one presentation details`

A common scenario could be to **create a content page** based on a base content template.

It allows to add **standard values** for a standard content page.

1. create _ContentPageTemplate
2. create contenPage template
3. add as base template _ContentPageTemplate

The contentPage inherits all the fields and standard values from _ContentPageTemplate and new fields can also we added.

Recommended practices:

- don't create circular inheritance
- use friendly names
- begin the name of a base template with an underscore
- assing icons for all the template

### Template inheritance type

- Direct Inheritance

    a => b

- Indirect Inheritance

    a => b => c

- Multi inheritance

    a => b
    c => b