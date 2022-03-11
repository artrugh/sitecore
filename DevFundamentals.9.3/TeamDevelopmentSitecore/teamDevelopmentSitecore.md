## Team Development for Sitecore

There was an issue in Sitecore to move projects from local develoment to other environments(production).

Team Development for Sitecore(TDS) is a **plug-in** for **Visual Studio** that allows to serialize Sitecore Items into a project in the same solution and automate synchronization of item changes.

Syncronize database changes between individual development environment (local and production).

The **source control system** also **keep track** of database changes and allows to compare database changes.

It helps to creat, build and deploy Sitecore solutions.

It makes sitecore items to behave the same ways as code assets. It focus on **developer items**.

TDS allows to:

- put items into source control.
- build deployment scripts that push items to various environments.
- create packages for later deployment.

### TDS Features

- **TDS UI** helps to synchronize changes between the **serialized copies in the file system** and the **sitecore installation**.

- **TDS** can create deployment features which are **deployment artifacts or packages** that contain the item and code needed to deploy the changes.

- **TDS** can create a **remote endpoint** in a Sitecore installation, so you can install the package on installation on other computers.

- **TDS** offers features which allow developers to trim items and fields that need to go into packages.

### Steps

1. How to create a TDS Project in Visual Studio?

    1. Right-click in Solution in Solution Explorer.
    2. Hover Add
    3. Click **New Project**
    4. Search **Sitecore TDS Projects**
    5. Click Next
    6. Add Name:ProjectName.Items.Content, and Location:path to the solution.

2. How to set TDS properties?

    1. Right-click in the new **TDS Project** you have created
    2. Click **Properties**
    3. In the **General** tab select the **Source Web Projects**: ProjectName Web
    4. In the **Build** tab, set your **Sitecore Web URL**: https://ProjectName93sc.dev.local
    5. In the **Build** tab, set your **Sitecore Deploy Folder**: C:\inetpub\wwwroot\ProjectName93sc.dev.local
    6. In the **Build** tab, under the **Sitecore Access Guid**, there is a checkbox called **Install Sitecore Connector** which generates the Guid when it is clicked: Click it.
    7. Save
    8. Click Test
    9. Save

3. Create a TDS Global Config Files

    It helps to create new projects more efficient.
    The config works **accross all projects in the solution**.

    1. Right-click on the solutions
    2. Hover over **Sitecore TDS**
    3. click **Add Global Sitecore TDS Config File**
    4. Copy from the TDS ProjectName.Items.Content and Paste
    5. Save

    ```xml
    <SitecoreWebUrl>https://ProjectName93sc.dev.local</SitecoreWebUrl>
    <SitecoreDeployFolder>C:\inetpub\wwwroot\ProjectName93sc.dev.local</SitecoreDeployFolder>
    <InstallSitecoreConnector>True</InstallSitecoreConnector>
    <SitecoreAccessGuid>paste guid from ProjectName.Items.Content.SitecoreAccessGuid</SitecoreAccessGuid>
    ```

3. Create a TDS User Config Files

    It allows to connect to the instance of Sitecore.

    1. Right-click on the solutions
    2. Hover over Sitecore TDS
    3. click **Add Global Sitecore TDS User Config File**
    4. Add:


    ```xml
    <SitecoreWebUrl>https://ProjectNamesc.dev.local</SitecoreWebUrl>
    <SitecoreDeployFolder>C:\inetpub\wwwroot\ProjectNamesc.dev.local</SitecoreDeployFolder>
    ```

4. `once the global config have been set, you can repeat step 1 for Master and Core DB. Just repeat the steps, but in 1.6 replace Content name with Master and Core. (Name:ProjectName.Items.Master, Name:ProjectName.Items.Core)`

5. Add items inside your TDS Projects

    You can create items inside your TDS Projects.

    1. Right-click on the TDS project 
    2. Click **Get Sitecore Items**, which shows the Sitecore Items in the root of the content tree.

### YML serialization

You can use your **YML serialization method** after configured **TDS**.

1. Ensure that your TDS projects are configured properly
2. Build your project
3. Pull Sitecore items into your project.

Push Sitecore Items

1. Right-click in **TDS project**
2. Click properties
3. General Tab
4. Set the Serialization Format dropdown: **YML Serialization**
5. Click yes in the popup menu
6. Check Solution: .web/app_config/Include/SerializationYaml.config
7. Build your solution before pulling Sitecore items into your projects
    - Build: click Build in the nav, and select Build Solution
        Automatically it will:
        - push your file to Sitecore
        - push the configYaml file so that Sitecore uses YAML serializationYam

Pull Sitecore items into your project

1. Right-click in TDS projects
2. Click Get Sitecore items
3. Open up Content node
4. Open up templates node
5. Right-click on the NameSite
6. Select all children
7. Click Get Items


```diff
+ Important: When inputting TDS license key during TDS installation, the Company Name and license key are case sentive
```

### Packages

There are two types of deployable packages that TDS can build out that can be pushed into production:

- **Update package**
    - It is defined by Sitecore and contains all the **items and code zipped into a file**. The file can the be run through the Sitecore update installation wizard or another open-source tool to drive and deploy the necessary APIs.

- **Web deploy package**
    - It is a **zip** of the **web route** that will be deployed with a specific TDS created serialization method to get items into the database. It is faster than the **update package** because the APIs can be driven in amulti-threaded way as they push items into Sitecore.

- **Custom deployment package**
    - You can stract the elements that may best fir the needs of your site and build your own package.