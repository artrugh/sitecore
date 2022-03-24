### Tag Helpers

They are the feature of ASP.NET Core Rendering SDK that makes it possible to harness **server-side code** when rendering HTML elements, Sitecore fields, and various Sitecore field types, side-by-side, with Razor syntax.

Tag helpers should be in *View/_ViewImports.cshtml* imports.

```cs
@addTagHelper *,
```

Sitecore fields which can be render by the **Sitecore.AspNet Rendering engine**:

- Placeholder

    It can **render** the components defined in a Sitecore placeholder.

    The name attribute is required and the value must match the name of a placeholder returned by the Layout Service for the current component. If it is invalid or unmatched, a warning is rendered.

    ```html
        <sc-placeholder name="name"></sc-placeholder>
    ```

- TextField

    It can **render and edit** the content of a single-line and multi-line text fields when the page is in edit mode. Add the name of a TextField property in the asp-for attribute of an HTML element. For disable editing add the editable attribute.

    ```html
        <h2 asp-for="@Model.Heading" convert-new-lines="false" editable="false"></h2>
    ```
- Rich Text Fiel

    It can **render and edit** the content of Sitecore rich text field when the page is in edit mode.

    This way is prefered because Sitecore rich text has it own root `<p>` tag, and this medhot does not introduce a new element.

    ```html
        @model MyComponentModel
        <sc-text asp-for="@Model.Content"></sc-text>
        <div asp-for="@Model.Content"></div>
    ```
- Hyperlink

    It can **render and edit** the content of Sitecore general link field when the page is in edit mode.

    ```html
        @model MyComponentModel
        <sc-link asp-for="MyLink"></sc-link>
        <sc-link asp-for="MyLink">This is my link</sc-link>
        <a asp-for="MyLink">This is my link</a>
        <!-- You can overwrite or add additional attributes -->
        `<sc-link asp-for="MyLink" class="font-weight-hold" data-otherattributes=""></sc-link>`
    ```
- Date

    It can **render and edit** the content of Sitecore date field when the page is in edit mode.

    ```html
        @model MyComponentModel
        <!-- You can specify the format of the date with the date format attribute. If not date format attribute is set, the Date tag helper shows the local format. -->
        <sc-date asp-for="MyDate" date-format="d" culture="en-us"></sc-date>
        <span asp-for="MyDate"></span>
    ```
- Image

    It can render and edit the content of Sitecore image field when the page is in edit mode.

    ```html
        <sc-img asp-for="@Model.Image"></sc-img>
        <img asp-for="@Model.Image" image-params="new { mw=100, mh=100 }"/>
        <img style="background-image: url(@Model.Banner?GetMediaLink())"/>
    ```
- Number

    ```html
        <sc-number asp-for="MyNumber"></sc-number>
        <span asp-for="MyNumber" number-format="C" culture="en-us"></span>
    ```