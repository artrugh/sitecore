### Event and Flow Data Object

[docu](https://doc.sitecore.com/cdp/en/developers/sitecore-customer-data-platform--data-model-2-1/the-event-object.html#UUID-b002a47e-869c-a187-3fa5-57b22092f441_itemizedlist-idm1903320569834268)


If you integrate with Sitecore CDP using the Boxever JavaScript Library or direct HTTP requests, use this event object to collect all the event data about a user's interaction with your application.

You then send the event to Sitecore CDP.

#### Flow Object
- It should include the **friendlyId** of the Full Stack Experience or an Interactive Full Stack Experiment that you want to run, so CDP runs the Experience or Experiement.
- It includes the **Minimum required attributes** and:
    - at least one guest identifies attribute:
        - browserId.
        - email.
        - identifiers
    - optionally, it can includes a custom key-value pair object.

```JavaScript
    const flowObject = {
    clientKey: Boxever.getClientKey(),
    friendlyId: "running_shoes_popup_02",
    channel: "WEB",
    language: "EN",
    currencyCode: "EUR",
    pointOfSale: "myretailsite/ireland",
    // guest identifier:
    browserId: Boxever.getID(),
    // optional attributes:
    aCustomObject1: { key: "value" },
    aCustomObject2: { isOptional: true }
    }
```
