## Layouts

**Data and presentation** is separated in Sitecore environment. Which means that **content** and **renders** are detached.

How to transform content into HTML output?

Creating Layouts and assigning placeholders which houses the content.

The data type is control by templates.

While the presentation of a website is controlled by **layouts** which is based on a **template**.

Layouts define the general structure or **scaffolding** of the page site.

### Layout elements

- **implementation**
    It defines the markup to use and is written in a a Razor.cshtml visible in **Visual Studio**.

- **definition item**
    It is visible in the **Content editor** and it is by default in *sitecore/Layout/Layout* in the content tree. 
    It allows to register the **layout cshtml** file within sitecore in the **Data.Path field** by using the path on the site wwwroot folder from the project.

1. Add a Layout to the project in Visual Studio

- right-click *Views/ProjectName/Layout*
- Add new item
- Select *Sitecore/MVC/Sitecore View Layout*
- Add a name

A promp out will open to set the **definition item**

- Select *masterDB/sitecore/layout/layout/Project*

After that the **defintion item** and the **cshtml** files are created.
The path location of the layout is automatically included in the defition item.

2. Add a Layout to the a page in the Content editor

- go to *sitecore/content/home*
- select the template clicking in the panel/content/QuickInfo
- go to Standart Values of the template
- click presentation in the ribbon
- click on Details
- on the default option click on edit
- click on layout
- select *layout/project/<name-of-the-created-definition-item>*

3. Add a Placeholder to the a page

- go to *sitecore/content/home*
- select the template
- go to Standart Values
- click presentation in the ribbon
- click on Details
- click on edit
- click on Placeholder settings
- add or create a placeholder

`Best practice is to create one view per device`

### Presention Details

Each layout item in sitecore has presention details.

Visit the [presentation details section.](presentationDetails.md)
