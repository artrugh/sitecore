## Responsibe design

### Grid

View/Grid

It allows three different grid sistems:

- Bootstrap
- Foundation
- Grid 960

With the use of grid layouts, the page will be divide into columns, allowing to determine page structure and divide your space both horizontally and vertically.

When you add a component to the page, the component has 12 column grids by default.cshtml

You can create your own custom grid.

## View Mode

Create themes

- Selected Theme
- Grayscale
- Wireframe

Themes are store in the Media Library/Themes and the theme items can be customise.

## SXA Renderings and rendering variants

- Simple
    - Consists on a layout and use single data source items to provide page content.
- Complex
    - Contains multiple simple or complez renderings. These renderings have one layout definition, all eadded renderings are defined in a renderings page property.

When you place a rendering which supports rendering variants, you can choose an option. You can also configure the default renderings and create new variants.

Some default SEA Renderings:

- language selector
- facebook comments
- Image
- Link List, of items which contain title, link and text
- Rich text

Composite Renderings:

Select a Rendering/Composites

- Accordion: a list of collapsible sections.
- Carousel: set of routing slides that are accompanied by descriptions and links.
- Flip: two items, front and back.
- Snippet: reusable group of renderings.
- Tabs: display of content within a tabbed layout.

[check the full list](https://doc.sitecore.com/xp/en/users/sxa/102/sitecore-experience-accelerator/the-sxa-renderings-and-rendering-variants.html)

More SEA renderings support rendering variants. By default the first is applied. Any custom rendering variants created are added to the list.

It is possible to use components that support rendering variants inside composites.