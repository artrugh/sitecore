## Sitecore Experience Platform Single Developer (XPO) Intallation using SIF

### XP Single Developer topology

- Sitecore standalone wesite - Content Manager - Content Delivery Processing.
- xConnect and xDB webservices.
- Sitecore Identity Server.
    - Standaline website acts as an Open ID.
    - Connects compliant security token servise.
- Solr search engine.

### Installation

1. [Download ZIP](https://dev.sitecore.net/Downloads/Sitecore_Experience_Platform/102/Sitecore_Experience_Platform_102.aspx) - Download options for **on-premises** deployment section as **Packages for XP Single**
2. copy the folder in C:/resourcesfiles
3. ```sh
    Install-SitecoreConfiguration -Path .\Prerequisites.json
    ```
4. Save license in C:/resourcefiles
5. Edit Sitecore Admin Password in XPO_SingleDeveloper.ps1
6. run .\XPO-SingleDeveloper.ps1
7. The password is automatically generated and insert into the appropriate config files.
8. Check App_Config/connectionStrings.config
9. Rebuild the search indexes and the link for the database.
    - Search indexes: Launchpad/Control Panel/Indexing/Index Manager - Select All - Rebuild
    - Link database (Master Core): Launchpad/Control Panel/Databases/ Rebuild link databases