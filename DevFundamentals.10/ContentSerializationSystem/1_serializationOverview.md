## Content Serialization System

[docu](https://doc.sitecore.com/xp/en/developers/100/developer-tools/sitecore-content-serialization.html)

The **Content Serialization in Sitecore** is the process of converting **Sitecore items** into **files**, allowing developers to **save and restore** the item between Sitecore instances.

As a developer, you can **pull and push items to disk** in order to move content changes between different environments in the **development and deployment process**.

It allows to:
- easily put items into **source control**,
- build **deployment scripts** that push items to various environments, 
- and create **packages** for later deployment.

The SCS system serializes content items into your project folder as **YAML** files.

The project configuration file is named **sitecore.json**. It has several properties including **modules** that references the relevant **Sitecore Content Serialization modules**.

### Mode

You can serialize manually or automatically.

- **manual**: to push or pull **content items** to or from Sitecore instances on demand.

- **automatic**: to specify **content items** that should be automatically serialized from Sitecore instance to your file system when they are **created or updated**.

### Include

You single out subsets of content items for serialization with includes and rules. This is useful for repeating the serialization of particular parts of your content item tree.

You configure **what and how** content items are included and excluded from serialization in a module file such as Project.module.json. You can place and override serialization configurations in all module files.

Each include must have a **name property** that becomes a folder name in your file system and a **path property** that specifies what part of your content item tree to serialize.

### Rules

They includes:
- a path relative to the root path.
- the scope of content items to influence.
- alternations to the allowed push operations.

The rule system works by the **first-match-win** principle, meaning that when a content item matches a rule, all subsequent rules are ignored.

Because of that, you should put the most specific rule first. Rules for parents path override rules for children's and descendant's paths.

```json
{
    "items": {
        "includes": [
            {
            "name": "content",
            "path": "/sitecore/content/home",
            "rules": [
                    {
                    "path": "/products/legacy",
                    "scope": "ignored"
                    },
                    {
                    "path": "/products",
                    "scope": "ItemAndDescendants",
                    "allowedPushOperations": "createUpdateAndDelete"
                    },
                    {
                    "path": "*",
                    "scope": "ignored"
                    }
                ]
            }
        ]
    }
}
```
### Relative serialization path hashing and alishing

It uses hashing to shorten paths that are too long for your file system. It
The file system path of serialized content items is determined by one absolute and three relative paths.

- the absolute path, where the project is located in the file system.
- the relative **serialization path**, where SCS system serializes content items.
- the relative **include path**, what you have named the folder that your content items must be stored in.
- the **relative content item path**, is the path of the content item in a **Sitecore instance**.

Example:

- *C:\Users\Peter\Sitecore\Project\src\Sites\/* is the base path.
- *serialization\/* is the serialization path by default.
- *content\/* is the include path.
- Home\Products\Toys\Ball.yml is the content item path.

Concatanation:

*C:\Users\Peter\Sitecore\Project\src\Sites\serialization\content\Home\Products\Toys\Ball.yml*

*C:\Users\Peter\Sitecore\Project\src\Sites\serialization\content\<hash value>\Ball.yml.*


### Max Relative Item Path length and Relative serialization path

In the sitecore.json file you can find the **defaultMaxRelativeItemPathLength** and **defaultModuleRelativeSerializationPath** properties.

A reasonable value should be between 100-200

### Models

SCS utilizes **modules** to specify which Sitecore items should be included and how they should be serialized.

In your project folder, create an empty module text file named *nameOfModule.module.json*

| property | inclusion | pupose |
| -- | -- | -- | 
| namespace | mandatory | the namespace of the module |
| references | optional | references toother modules that must be deserialized first (such as templates in a Foundation module) |
| items | optional | items to be serialized |
| roles | Sitecore role domain and a regex pattern to determine specific roles to include under the domain |

```json
{
    "namespace": "",
    "references": [""],
    "items": {},
    "roles": [
        {
            "domain": "sitecore",
            "pattern": "Developer"
        },
        {
            "domain": "custom",
            "pattern": "Role*"
        },
        {
            "domain": "extranet",
            "pattern": "^MySite.*$"
        }
    ]
}
```

### Exclude fields

Modify the serialization section of the *sitecore.json* file, for example:

```json
{
  "modules": ["scr/*/*/.modules.json"],  
  "serialization": {
    "defaultMaxRelativeItemPathLength": 120,
    "defaultModuleRelativeSerializationPath": "serialization",
    "excludedFields": [
      {
        "fieldId": "badd9cf9-53e0-4d0c-bcc0-2d784c282f6a",
        "description": "__Updated by"
      },
      {
        "fieldId": "d9cf14b1-fa16-4ba6-9288-e8a174d4d522",
        "description": "__Updated"
      },
      {
        "fieldId": "5dd74568-4d4b-44c1-b513-0af5f4cda34f",
        "description": "__Created by"
      },
      {
        "fieldId": "25bed78c-4957-4165-998a-ca1b52f67497",
        "description": "__Created"
      },
      {
        "fieldId": "{52807595-0F8F-4B20-8D2A-CB71D28C6103}",
        "description": "__Owner"
      },
      {
        "fieldId": "{001DD393-96C5-490B-924A-B0F25CD9EFD8}",
        "description": "__Lock"
      }
    ]
  }
}
```

in **.module.json*

```json
{
    "items": {
        "includes": [
            {
                "name": "Apikey",
                "path": "/sitecore/system/Settings/Services/API Keys"
            },
            {
                "name": "Media",
                "path": "/sitecore/media library/my-first-jss-app"
            },
            {
                "name": "Templates",
                "path": "/sitecore/Templates/Project/my-first-jss-app"
            },
            {
                "name": "Content",
                "path": "/sitecore/content/my-first-jss-app"
            },
            {
                "name": "Layout",
                "path": "/sitecore/Layout/Layouts/Project/my-first-jss-app"
            },
            {
                "name": "Renderings",
                "path": "/sitecore/Layout/Renderings/Project/my-first-jss-app"
            },
            {
                "name": "Placeholders",
                "path": "/sitecore/Layout/Placeholder Settings/Project/my-first-jss-app"
            }
        ],
        "excludedFields":[
            {
				"fieldID": "{EB504D1B-B612-4FFF-B239-CA3BD7273D1B}",
				"description": "FieldsForExclude1"
			},
			{
				"fieldID": "{3C2C061E-F61F-4DF6-89EA-0B7A56348737}",
				"description": "FieldsForExclude2"
			},

			{
				"fieldID": "{4F7446A4-79C8-4853-A357-723665FE68DA}",
				"description": "ExcludeUnversionFIeld"
			}
        ]
    }
}
```

check using CLI

```sh
serialization info -t
```

### Sitecore Management Services

It is a package that you must download and install in **Sitecore Content Manager** instance to support Sitecore CLI and Sitecore for Visual Studio.