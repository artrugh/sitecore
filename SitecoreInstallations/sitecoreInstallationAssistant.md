## Sitecore Installation Assitant

Sitecore Installation Assitant, also called SIA, was introduced in XP 9.2.0, and it is an intuituve graphical user interface.

It includes some optionally installations and configurations:

- Optionally install and configures the required version of the **Solr search service**.
    - Alternatively you can install and set up Solr manually.
- Optionally install **Sitecore Experience Accelerator**.
- Configures **Microsoft Window Server options**.
- Validate the specified installation **parameters** and **settings**.

### Requirements

- Hardware
    - 4 core processor and 16 GB RAM.
- Software
    - IIS (Internet Information Services) 10.0
    - Windows Server 2016/ 10 (64 - bit).
    - For Experience Platform: .Net Framework 4.8.0
    - For identity server: .NET Core 2.1.18 . check Windows Hosting Machine
    - Microsoft Visual C# 2015.
- Databases servers:
    - Microsoft SQL Server 2017.
    - Microsoft SQL Server 2019.
    - Microsoft Azure SQL.
- Microsoft SQL Server drivers and utilities.
    - install xConnect Application Server.
    - Microsoft ODBC Driver 13 for SQL Server.
    - Microsoft Command Line Utilities 13 for SQL Server.
- Search Provider:
    - Solr: content search and Analytics search.
    - `deplicated` for Sitecore 9 **Azure Search** is recommended for **Azure Cloud PaaS deployment**.
    - PaaS: required Azure Searchm Solr, Solr Cloud in Azure.
    - on-premise: Solr
    - Solr: Install and Configure Solr to run as a Window Service. Enable and set secure sockets layer (SSL) for Solr.

### Settings

Installation/solution prefix: name of the project
Sitecore admin password: any
Sitecore license file: path to the file

SQL settings:

SQL Server instance: (local)
SQL Server admin user name: sa
SQL Server admin password: password
Instance Name: nameOfTheProject93.dev.local
Sitecore Install Folder: Windows C:/Dev

Solr settings:

Solr Service URL: https://solr:8983/solr
Solr file system root: C:\Solr\8.1.1Solr-8.1.1
Solr Windows service name: 8.1.1Solr-8.1.1
