## Base template

Base Template is a parent template that allows to establish common fields across other templates.

```diff
+ Naming Convention: the name of BaseTemplates with a underscore. Example: _BaseTemplate@
```

### Set a base template

#### In visual studio

Scope your project by using the scope feature in Sitecore Rocks. This feature allows to hide sections of the content tree in the Sitecore Explorer. Hiding instancing will help to avoid confusion and focus the work area and also prevents you unintentionally creating and editing items in other databases.

- Extentions -> Sitecore -> Sitecore Explorer
- right-click in the project.master
- choose scope to this

#### In sitecore explorer

- navigate to the /Sitecore/templates node
- right-click and select new template folder
- name the Folder
- it is recommended to create another template folder for your base template, to avoid confusion adn for easy access.
- named one folder Base_Templates
- right-click in Base_Templates
- select new template
- name the template \_ContentPageTemplate and Ok
- create a new section and name it Main Content
- create a new field, name it Page Title, and select the Single-line tezt field type
- Save
- repeat this process creating two more templates \_Banner and \_Image Bank

#### In Sitecore Experience Platform

- Go to content editor
- Store all the templates used in one project in one folder
- The templates section of the content tree is where you will find all the templates and their definitions, and this location is where you want to create new Templates
- right-click in Templates
- insert a new template Folder
- create a new folder into your project
- create a template in the new folder
