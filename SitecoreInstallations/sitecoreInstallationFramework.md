## Sitecore Installation Framework

[Official Docu](https://dev.sitecore.net/Downloads/Sitecore_Experience_Platform/102/Sitecore_Experience_Platform_102.aspx)

There are two option to use the SIF:

- Using  the Microsoft PowerShell
    - add Repository
    ```sh
    Register-PSRepository -Name SitecoreGallery -SourceLocation https://sitecore.myget.org/F/sc-powershell/api/v2
    ```
    - press yes and Enter.
    - Install PowerShell Modules
    ```sh
    Install-Module SitecoreInstallFramework
    ```
    - press yes and Enter.
    - to update
    ```sh
        Update-Module SitecoreInstallFramework
    ```

- Install SIF manually using ZIP

    1. Downloads the Zip sfrom [sitecore](https://dev.sitecore.net/Downloads/Sitecore%20Installation%20Framework/2x/Sitecore%20Installation%20Framework%20230)
    2. Navigate to the file in **Windows Explorer** and **unlock** the file in properties/general.
    3. Choose user:
        - all users C:\Program Files\WindowsPowerShell\Modules
        - specific user C:\Users\Documents\WindowsPowerShell\Modules
        - custom location: any path
    4. Validate installation
    ```sh
    Get-Module SitecoreInstallFramework -ListAvailable
    ```
    5. For custom Location: Import SIF into PowerShell session.
    ```sh
    Import-Module C:\<CustomLocation>\SitecoreInstallFramework
    ```
    6. Version:
    ```sh
    Import-Module -Name SitecoreInstallFramework -Force -RequiredVersion x.x.x
    ```
### Customize the Sitecore installation 

Configurations are written in json files. You can use tasks, parameters, config functions, and variables. Custom tasks and config functions can also packaged as a module, and included in configurations.

**Tasks**

Tasks are actions that are conducted in sequence when `Install-SitecoreConfiguration` runs. A task is implemented as a Powershell cmdlet.

Each task has **unique name** and a Type property.

They can have parameters or a collection of parameters passed to it.

Tasks map directly to PowerShell functions and are registered with the `Register-SitecoreInstallExtension -Type`.

```json
    {   
        "Paramaters":{
            "Param1": {
                 "Type": "string", "DefaultValue": ""
            }
        },
        "Variables": {
            "Destinition": "[concat(environment('SystemDrive'), '\\newfiles')]"
        }
        "Tasks": {
            "Task1": {
                "Type": "Copy",
                "Params": {
                        "Source": {"Type": "string"},
                        "Destination": { "Type": "string", "DefaultValue": "<new-file>"}
                    },
                "Skip":  "[not(Parameter('Param1'))]"
            }
        }
    }                   
```

- parameters: 
    - they changes values inside a configuration at runtime.
    - they can be passed into a task using parameter config functions.

```sh
Install-SitecoreConfiguration -Path .\configuration.json -Source C:\<source-file>
```
```json
    {
        "Paramaters":{
            "Source": { "Type": "string" },
            "Destination": { "Type": "string", "DefaultValue": "C:\/<new-file>" }
        }
    }
```
- skip
- register: 
```sh
Register SitecoreInstallExtention -Type ConfigFuntion
```

- parameter validation are functions:
    - ValidateCount
    - ValidateLenght
    - ValidateNotNull
    - ValidateNotNullOrEmpty
    - ValidatePattern

- Configurate functions: `[funtion-name(param1, param2)]`
```json
{
    "variable1": "[GetFunction(Number: 123, String: 'Text')]"
}
```
```sh
     Get-Function -Number 1234 -String "Text"
```

- Modules in configuration.json.
```json
{
    "Modules": ["ModuleName", "ModulePath"]
}
```
