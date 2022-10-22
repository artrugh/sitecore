### Flow Execution Request

- Facilitates personalization in interactive experiments or web experiements.
- Invokes real-time responses.
- Supports using decision models in interactive experiments to return the next best offer or action.
- Send the output of the decision model in real-time to an external system such as a marketing cloud.

#### Flow execution REST API

A flow is the mechanism that runs an experiment or experience on the Sitecore CDP backend.

You can use the browserID attribute, email attribute, identifiers object, custom field, or the experiment ID to create the flow execution.

POST: https://apiEndpoint/v2/callFlows

- It should include the **friendlyId** of the Full Stack Experience or an Interactive Full Stack Experiment that you want to run, so CDP runs the Experience or Experiement.

The following is a request that uses the browserId attribute:

```JSON
{
    "clientKey": "abBah8aelipaPeebae7roox2tiexoSee",
    "channel": "WEB",
    "language": "en",
    "currencyCode": "EUR",
    "pointOfSale": "retailsite.com",
    "browserId": "56860bff-94ba-4d84-aa37-2b5a83d5411b",
    "friendlyId": "home_page_banner"
}
```