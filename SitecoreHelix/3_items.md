## Items in Helix

### Item

An item represents any information.

It has a name and an GUID and it is based on a template that defines which fields the item contains.

An item can have multiple language versions.

Types:

- Definition items
- Content items

#### Definition items

They define the configuration or structure of the implementation and content metadata for assets in the solution. They are owned in the development environment and moved as part of versioned deployment from development, to test, to production.

- Layout and rendering Items
- template and field Items
- Placeholder Settings items
- Custom field types
- Lookup items for seetings
- All item in the Core database

#### Content items

They are managed by the editors on the website and content content that is output on the sites or channels of the website. The production environment (editors and administrators) owns content items.

You should never overwrite an item comming from the development or test environments.

- Items that are created in development and deployed once into production
- Items that are created and managed in production

### Association between Items

Associate items with modules. Group the in folders according to their layers and module the belong. Ex: /Sitecore/Templates/[Project|Feature|Foundation]/[Module
]

Managing definition items along with the business logic that uses them, poses a technical challenge as the items are physically stored int the Sitecore SQL databses while you save the buisness logic in code files on the disk.

#### Serialization

It allows items in the databases to be written to disk in a text-based format and subsequently restored into a database.

Serialized items should be versioned as part of the owning module, next to the code and projet files. Place the serialized items on disk in a subfolder beneath the module: Ex: /src/[Project|Feature|Foundation]/serialization/

Serialization is support through Sitecore CLI, and TDS or Inicorn

#### Deployment

- It is recommended to version and manage items and business logic together in your development process and deployment.

- Separating Content from Defintion Items, enable to deploy all defintion items as part of a new version of your implementation. It assure that ownership of definition items remains in the development process and that no occasional changes are made in production or test environments.

- Helix is not equivalent to the general modular approach for deploying and running Sitecore in production. Your enire implementation should be integrated and deployed in a single-versioned process.