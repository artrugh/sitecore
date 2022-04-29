## Supporting multilingual applications in JSS

Rendering translated data from Sitecore:

- Primary page content.
- Dictionary items used for translation of labels, button text, and so on.

When getting content from Sitecore, whether with GraphQL or with REST, the request is made behind the scene to the **Sitecore Layout Service**.

The Layout Service respects the Sitecore Language Context when fetching route and context data.

`http://JssReactWeb/sitecore/api/layout/render/jss?item=/Services&sc_lang=es-MX&sc_apikey={YOUR_API_KEY}`

In Disconnected Mode, the Disconnected Layout Service is powered by the JSS Manifest data, which is single-language.