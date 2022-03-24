## Implementation

Set up the folder structure to organize your modules.

**Modules** are sets of includes-rules that determine:
- what you want to serialize.
- how you want to interact with items you **pull** and **push** in your solution.

Follow this steps to implement **serialization modules**.

### Creates Modules

1. Go to the **Content Editor**:

    - right-click *Home/myProject* and click on Insert -> Page
        - Page Name: Care
            - Page Name: Light
            - Page Name: Solution
            - Page Name: Watering
        - Page Name: Plants
            - Page Name: Flowers
            - Page Name: Herbs
            - Page Name: Trees

2. Create a **Module** using the text editor in **Visual Estudio Code**.

    - Navigate to sitecore.json file (this file is created with the up.ps1 script)

    - in modules section, change *src/Items.module.json* to *src/*/*.modules.json*

    - *sitecore.json* file controls how **Sitecore serialization** behaves.
        
        - The module section is used by Sitecore serialization to locate all modules in your solution.
            
                ```json
                    {
                        "modules": [
                            "src/*/*.modules.json"
                        ]
                    }
                ```

    - Create a folders in */src* called: TestModule

    - Navigate to the TestModule folder you has created and create a file called: *TestModule.module.json* and add:

                ```json
                {
                    "namespace": "TestModule"
                }
                ```
    - Save changes.

    
4. Create a **Module** using **Sitecore Module Explorer** in **Visual Studio Code**.
        
    - In the Sitecore Module Explorer right-click in **Modules**
    - select **New Module** and set the namespace to SVSTestModule
    - under module file path, browse to src/SVSTestModule
    - click save
    - to see the code: right-click on the module and choose **View Code**

#### Allowed Include properties

An **include** indicates which section of the **Sitecore Content Tree** to serialize.

Modules can contain **more than one include**, depending on the complexity of your serialization needs.

When creating an include you can indicate:

- name
- path
- maxRelativePathLength
- database
- scope
- allowedPushOperations of items that you want to be serialized.

| concept | definition |
| -- | -- |
| name | sets the name of the folder name in the file system |
| path | sets the path of the content tree | 
| scope | indicates the extends of the include |
| database | sets the database your item are in |
| allowedPushOperations | sets the abilities of the include: create, update, delete |

| property | required | Valid Values | Default Value |
| -- | -- | -- | -- |
| name | yes | String | None |
| path | yes | String | None |
| scope | no | SingleItem, ItemAndChildren, and ItemAndDescendants | ItemAndDescendants |
| database | no | Master or Core | Master |
| maxRelativePathLength | no | Number | 130 |
| allowedPushOperations | no | CreateOnly, CreateAndUpdate, and CreateUpdateAndDelete | CreateUpdateAndDelete |

### Create Include 

1. **Visual Studio Code**
  
    - *TestModule.json* serializes the Plants item and its descendents (scope: ItemAndDescendants by default)

            ```json
                {
                    "namespace": "TestModule",
                    "items": [
                        {
                            "includes": [ 
                                {
                                "name": "plant include",
                                "path": "/sitecore/content/myproject/plants"
                                }
                            ]
                        }
                    ]
                }
            ```
    
2. **Sitecore for Visual Studio**
    - in the Sitecore Module Explorer, right-click on TestModule
    - click **Add Include**
        - name: *care include*
        - path: "/sitecore/content/myproject/care"
        - Ok
        - Save

### Include Rules

Rules are created to **modify the behavior of an include**.
The order of the rules dictates the order the rules are evaluated.

| property | required | Valid Values | Default Value |
| -- | -- | -- | -- |
| path | yes | String | None |
| scope | yes | Ignored, SingleItem, ItemAndChildren, and ItemAndDescendants | None |
| alias | no | String | None |
| allowedPushOperations | no | CreateOnly, CreateAndUpdate, and CreateUpdateAndDelete | Inherited from parent |

| concept | definition |
| -- | -- |
| path | path to the item you are referring to, in the content tree |
| scope | indicates to what extent we are serializing the item in the content tree |
| alias | allows to indentify the items and it is custom hash value |
| allowedPushOperations | indicates what will happen to the item during serializion |

1. **Visual Studio Code**
        - *TestModule.json* will pull all the items under plants, minus a single item called Flowers

          ```json
                   {
                    "namespace": "TestModule",
                    "items": [
                        {
                            "includes": [ 
                                {
                                "name": "plant include",
                                "path": "/sitecore/content/myproject/plants",
                                "rules": [
                                            {
                                                "path": "/flowers",
                                                "scope": "ingnored"
                                            }
                                        ]
                                }
                            ]
                        }
                    ]
                }
            ```

2. **Sitecore for Visual Studio**
    - in the Sitecore Module Explorer, right-click on SVSTestModule
    - click **Add Rules**
        - path: "/flowers"
        - scope: Ignored
        - alias: blank
        - Allow Push operations: empty
        - Ok
        - Save

#### Pull serialization modules

1. CLI

Check the serialization command options

```sh
dotnet sitecore ser -h
```
or right-click in the module folder in **Sitecore Module Explorer**.


To test **what whould happen without executing it**, use the w flag.

```sh
dotnet sitecore ser pull -w (what if)
```

Pull **all your sitecore items** from your content tree to disk.

``sh
dotnet sitecore ser pull
```

2. Sitecore Module Explorer

- right-click on Sitecore Configuration Root
- click Pull items
- select the items and click Sync