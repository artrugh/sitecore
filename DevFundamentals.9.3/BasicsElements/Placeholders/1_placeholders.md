## Placeholder

It is the Sitecore's way of identyfing and naming a **position in the markup of a page**.

It allows **content authors** to dynamically add **content components** within the **Experience Editor**, dynamically bindinging the components.

A placeholder is identified by a unique attribute: **the placeholder key**.

The key is used to identify placeholder on the **layout** or within the **components**.

```csharp
@Html.Sitecore().Placeholder("key-name");
@Html.Sitecore().DynamicPlaceholder("key-name");
```

Placeholders have a corresponding **placeholder settings item** which list the placeholder key and are store in *sitecore/layout/Placeholder settings* in the content tree.

To make the placeholder available to use on the Experience Editor, the **placeholder settings item** should be added to the **presentation details** of an item or data template's standard values. This process is similiar than adding a **Layout**.

You can also, through the [Placeholder Settings](3_placeholderSettings.md), restrict which controls components are allowed within an specific placeholder.