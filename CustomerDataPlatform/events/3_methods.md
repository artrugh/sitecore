### Event methods

- **eventCreate**
    Boxever.eventCreate(eventDataObject, callBack function, format of response), to send data to Sitecore CDP.

        ```JavaScript
        // Send the event data to the server
        Boxever.eventCreate(eventDataObject, () => {}, "json");
        ```
- **callFlows**
    this method runs:
    - Interactive Full Stack Experience
    - Interactive Full Stack Experiment

    Boxever.callFlows(flow Object event data /include **friendlyId**, callback)

        ```JavaScript
        const flowDataObject = {
        clientKey: Boxever.getClientKey(),
        friendlyId: "running_shoes_popup_02",
        channel: "WEB",
        language: "EN",
        currencyCode: "EUR",
        pointOfSale: "myretailsite/ireland",
        // guest identifier:
        browserId: Boxever.getID()
        };

        Boxever.callFlows(
            flowDataObject,
            response => console.log(response)
        );
        ```

- **AddUTMParams**
    Boxever.AddUTMParams(event) - function adds every UTM parameter from the URL of the current webpage to the event object for tracking data.

- **getBucketNumber**
    Boxever.getBucketNumber(callback) - update bucket number cookie to match the latest from CDP. Call this method after **IDENTITY Event trigger.**

- Boxever.reset()
    - Clears the event queue.
    - Deletes the browser ID and the guest reference.
    - Reloads the Boxever JavaScript Library. During loading, the Boxever JavaScript Library creates a browser ID and a guest reference.

- Boxever.templating.compile() - rerenders a Web Experience or Web Experiment that is currently live in Sitecore Personalize.

- Boxever.triggerExperiences() - re-runs every Web Experience and Web Experiment that is live in Sitecore Personalize.