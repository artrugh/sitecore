## Composite Renderings in SXA

Composite Renderings allow to drop components within them.

### Snippet

It allows to create a reusable group of renderings.

It is an item which has more than one component. It can be embedded within a page or copied into a page placeholder.

The difference between Snippets and Partial design is that snippet are extensible.

Create

- Content Editor / Home / Data / Snippets /
- right-click Insert Snippet item
- name it and leave data source to default

Edit

- right-click on the snippet and select Experience Editor
- drag the components into it

Use

In the experience editor

- toolbox/composites/snippet
- drop the snippet on the page
- select the snippet
- click go and save the changes

### Data source configuration options

In the snippet item on the content editor, select the data source configuration to:

- Do not copy
    - use global data source. The source of the snippet is in the site data folder. When you change  it, the changes will be automatically reflected across all instances of the snippet on all pages.
- Copy global datasource to local context upon selection.
     - this option allows to localize the snippet configuration to the page. Any change made to the snippet only applied to the specific page.
- Ask user whether the copy of global data source  to local context is required upon selection.
    - User can choose how to reuse a snippet.
