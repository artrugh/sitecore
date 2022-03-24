## Templates

Templates are items that define the structure and behaviour of the items and the templates upon which they are based.

Template inheritance makes it possible for multiple modules and the business logic to share items and content because templates can look at the item's interface.

## Types

- Interface templates:
    - They act as an interface for the business logic to work against. They define the fields that are used by a module's logic. They are also refer as base templates.

- Page Type templates
    - They define the structure of a site. They derive from interface templates and have a presentation layout.

- Datasource templates
    - They serve as a reference point for renderings. They derive from interface templates but they don't have a presentation layout.

- Settings templates
    - They define configuration content for the business logic and the lookup items for fields.

- Folder templates
    - They shape the content structure.

- Rendering paramaters templates
    - They configure renderings and derives from the standard rendering parameters. They are prefix with _ to distinguis them from the other templates type.
