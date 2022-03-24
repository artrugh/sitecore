## Sitecore Multi Languages Feature
### Add Language

In Sitecore Explorer Platform navigate to:
Control Panel / Location / Add a new lenguage

After setting a new language, you can **change the language of an item** in the content editor.

### Language Fallback

[docu](https://doc.sitecore.com/xp/en/developers/102/sitecore-experience-manager/language-fallback.html)

Setting up **Language Fallback** ensures that the text on your page is **translated correctly**.

If your solution has a version that does not exist in a given language, language fallback functionality gets activated and the item or field value is displayed in the fallback language instead.

- navigate to "C:\inetpub\wwwroot\<website>\App_Config\Sitecore.config" using the file explorer

- create a file LanguageFallback.config in
"C:\inetpub\wwwroot\<website>\App_Config\Include\" using the file explorer
- check the content of the file in [sitecore docu](https://doc.sitecore.com)
- specify language fallback rules. 

You can also set a language fallback chain.

- navigate to *sitecore/system/languages*
- click in the language
- scroll to the fallback language field
- Data/FallbackLanguage select a fallback language from the dropdown

- navigate to a desire template
- select the standard values
- you can **Enable Item Fallback Checkbox**

- Publish changes


### Sitecore Dictionary

It is used for labels that are fixed and used across the whole website. They are harcoded.

- Dictionary Domain.
    - Support multiple languages.
    - Uses Sitecore's native logic for localization.
- Global Dictionaries.

Recomendation:

- Reimplement your own dictionary.
- Avoid reusing Dictionary texts across modules, feature, or views.
- Use the dictionary entries in the presentation and business logic of the module.
- Make the dictionaries available at the site or tenant level to allow labels to be managed individually across sites.

#### Create a Dictionary

- navigate to "C:\inetpub\wwwroot\<website>\App_Config\Sitecore.config" using the file explorer
- create a file Dictionary.config in
"C:\inetpub\wwwroot\<website>\App_Config\Include\" using the file explorer
- check the content of the file in [sitecore docu](https://doc.sitecore.com)

- In Content Editor navigate to *sitecore/system/dictionary*

- click on ribbon / Insert from template
- make sure the template is /System/Dictionary/Dictionary Domain
- specify the item name which **was written in the Dictionary.config**
- you can entries clicking on ribbon / dictionary entry
- select entry in the prompt
- entry the key and the value
- push the changes nav/ publish

On the default.cshtml include

```csharp
    @Sitecore.Globalization.Translate.Text("ENTRY")
```