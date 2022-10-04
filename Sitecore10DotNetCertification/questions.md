
### Training questions and answers:

1. [When you are working with a multisite implementation?](https://www.advaiya.com/sitecore-multisite-architecture-single-installation/)

2. Reasons to assign security rights to roles instead of individual users.
    - Roles enable to control security access for groups of users and role simultaneously.
    - Assign permissions to individual users can be confusing and create risk.

3. Template inheritace is not recommended for **fields with the same name but different field source**.

4. It is recommended to define an **item presentation detail** as part of the **standard values child item** of a data template, because items created from a template **inherit the standard values**, including presentation details, and NULL fields default to the template standard values.

5. **Statically renders** prevent that Authors **select or edit** a component in the Experience Editor.

6. The dafault scope for a serialization is: **ItemAndDescendent**.

7. The purpose of a .env file (environment file), when deploying **Sitecore containers**, is to allows to declare environment variables for your Docker containers.

8. **Sitecore Core database** stores **settings and content** for the Sitecore application itself.
[sitecore core db](https://doc.sitecore.com/xp/en/developers/90/platform-administration-and-architecture/core-database.html#:~:text=The%20Core%20database%3A,creating%20or%20modifying%20an%20interface.)

9. You syncro the **MasterDB** whith **one or more indetified publishing targets**, when using `sitecore publish`.
[sitecore publish](https://doc.sitecore.com/xp/en/developers/100/developer-tools/the-cli-publish-command.html)

10. **Insert Options** are setted in the **Standart Values** in the item template.

11. A **layout** provides the **base struture** for a given delivery channel, while **components** are smaller structure items added to the **presentation details**.

12. The **layout service** provides structured data (JSON) about Sitecore-based pages, including components and their associated content.

13. When using **Sitecore Content Serialization**, the **sitecore.json** file, is the configuration file for **global development plugins and module locations**.

14. If you do not add the hostnames of your Sitecore environment to your Windows host file, you will not be able to access the Sitecore environment via the IP address in a browser.
[hostname config](https://doc.sitecore.com/xp/en/developers/102/sitecore-experience-manager/configuration.html)
**Solr Windows service name**

15. Install sitecore: Manual or zip file, Scripts, Sitecore Rocks, SIM, EXE.

16. After you make a Template bucketable, sync the existing items.

17. You can control the order in which your changes are applied when you patch in changes to the <Sitecore.config>, In App_Config/Include, use a naming convention and sub-folders for config files.

18. To enable **dynamic binding**, you need to create **placeholder**.

19. Check the effective permission of an account int the **Access viewer**.

20. **SIM Import/Export features**: Export an entire set of Sitecore database with content and import to a new environment.

21. The best way to source control Sitecore items is by **serialization**.

22. An **unversioned field** contain once version of the data per language.

23. **Field Editor** opens a pop up where fields are edited.

24. **Visual Studio Solution** is created outside the webroot because it is more portable.

25. An **item resolver** maps a URL to an item in the content tree.

26. If the same field name is used in **two separete inherited data templates**, the field will be duplicated.

27. Field types define: **raw value store in the DB**, which **editor control** will be use in Experience Editor, the **API field class** used in code.

28. If one role denies access and other allows, the result is **denied**.

29. `GetChildren()` get the list of all the children.

30. An item is the construct Sitecore uses to store data.

31. The default search providers in Sitecore are: **Solr** and **Azure Search**.

32. `GroupBy, Aggregate, Sum` are not supported by **Sitecore's implementation** of **LINQ** `IQueryable<T>`

33. The license are located: Sitecore application root folder/Data/license.XML

34. For support use the **Support Package Generator** from Sitecore Marketplace.

35. The **Master DB** publish items to the **MasterDB**.

36. When sync master and web db, it does not update index. **Deleted or unpublished items** are removed by publishing.

37. If an **item version** is not in a final **workflow state**, no automatic versioning and version is not publishable.

38. To allow user to add and remove components from a placeholder, create a **placeholder setting**.

39. Config changes get added **alphabetically** by default and it overrider settings from previous one, but it can be changed using <loadOrder>

40. **Dynamic placeholders** allow to reuse a component containing placeholders.

41. When an item inside a bucket is not bucketable, item is not hidden.

42. When the site is not multilingual, set languageEmbedding option to **never**.

43. The best way to modify web.config is using .config file in App_Config/Include.

44. You can not use placeholder inside placeholders.

45. All field types can be used with **Rendering Parameters**.

46. When you request a page that has no layout defined in the presenation detail, you get a **Layout not found error page**. To fix it, define layout in the **presentation details**.

47. `LinkManager.GetItemUrl(item)` retrieves the URL of an item.

48. Types of publishing: Delayed, Parallel, and Dedicated.

49. Define in a template: fields, field sections, icons, and base template.

50. DisableWebEdit when rendering a field inside the <title> tag in the <head> of HTML.

51. To take advantage of Sitecore intregrated **marketing** & **analytics** capabilities, implement **Experience Database**.

52. Presentation details can be set in: **Experience Editor**, **Content Editor**, **Template Editor**, **Sitecore Rocks**.

53. **SIM installation feature** you can install any version of Sitecore from repository of installers: install modules and packages, **reinstall the same configuration**.

54. An author use the **Experience Editor** to see an edit itmes in the tree structure.

55. In a template, you should define **Fields**, **Fields sections**, **Icon** and **Base Template**.

56. Using **field type** you define the raw data value stored in the **database**, determine which editor control will be used in the **Experience Editor** and the **API field class** used in code.

57. **Presentation details** can be set in the **Experience Editor**, **Content Editor**, **Template Manager** and **Sitecore Rocks**.

58. To translate fields and help text in the Sitecore client, use **Sitecore Dictionary entries**.

59. Data definition: Templates, Content: Items, Presentation: layout and components.

60. **Config files** are read in **alphabetical order** and it overrides settings from the previous one.

61. When you want to handle **more than one input form** on a controller rendering, you should create an **extension method** invoking the `FormHandler()` and Use `Ajax.BeginForm()` and specify the controller and action.

62. **Website**, **data** and **database** are the three folders in the physical path of the content folder that hosts the **Sitecore Application**.
