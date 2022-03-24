## Create a View Component with Custom Logic

View Component is the most powerful component where you can add complex logic. They support C# Classes that you can uso to implement that logic.

1. Create the **Service template** in Content Editor.

2. Create the **Service JSON** Rendering. In the *Datasource Template* select the created template.

3. Configure the placeholder for the created JSON Rendering.

    - *Placeholder Settings/Allowed Controls/* edit and select the **JSON Rendering**.

4. Publish site/ Republish.

5. Add the JSON rendering to the home page in the **Experience Editor** and **Publish/Smart Publish**.

6. Create a Service Interface in the solution.

    - Add a new folder *Services* in the *Rendering Host* project.
    - In the Solution, in *RenderingHost/Services* add a new Item.
    - Installed/Visual C#/ASP.NET Core/Code.
    - Select Interface.
    - Code and Save.

7. Create a Service Class in the solution.

    - In the Solution, in *RenderingHost/Services* add a new Item.
    - Installed/Visual C#/ASP.NET Core/Code.
    - Select Class.
    - Code and Save.

8. Register the Service in the *Startup* class.

    ```cs
    using MyProject.Services;
    public void ConfigureService(IServiceCollection services)
    {
        services.AddTransient<IService, Service>();
    }
    ```

9. Create the class model.

    - In the Solution, in *RenderingHost/Models* add a new Item.
    - Installed/Visual C#/ASP.NET Core/Code.
    - Class.
    - Name.
    - Add.

10. Create the View Component Class.
    
    This Class implements the custom logic.
    It extends *ViewComponent* Class and uses *modelBilder* and the created *Service* by Dependency Injection

    - Add a new folder *ViewComponents* in the *Rendering Host* project.
    - In the Solution, in *RenderingHost/ViewComponents* add a new Item.
    - Installed/Visual C#/ASP.NET Core/Code
    - Class
    - Name
    - Add

11. Create the Razor View

    - Add a new folder *Service* in the **RenderingHost/Views/Shared/Components/* project. This name should match the class name without the suffix *ViewComponent*.
    - In the Solution, in *RenderingHost/Views/Shared/Components/Service* add a new Item.
    - Installed/Visual C#/ASP.NET Core/Web
    - Razor View - Empty
    - Name, it should match the name of the **JSON Rendering**
    - Add

12. Register the View Component in *Startup.cs* file using the `.AddViewComponent("ViewComponent name without suffix")`.

13. After that you can add content in the **Experience Editor** home page and Publish.
    