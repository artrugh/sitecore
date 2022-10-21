### APIS

- Stream API:
    - Only use to write data to CDP.
    - Capture real-time, high velocity, and high-volume **behavioral data**. Typically deployed via Sitecore's lightweight JavaScript library for:
        - Web.
        - Mobile web.
        - Mobile app.
        - Call-center behavioral tracking.
    - Types:
        - **Event API** allows for **event-processing**, setting event via mobile and web.
            GET https://{apiEndpoint}/v1.2/event/create.json?client_key={{CLIENT_KEY}}&message={...}
        - **Browser API** extends functionality and manages **cookies** that help identify guests, further facilitating personalization. These Browser APIs are used for **capturing and consuming data.**
            GET https://{apiEndpoint}/v1.2/browser/create.json?client_key={{CLIENT_KEY}}&message={...}

- Interactive API:
    - Consume data from the CDP.
    - Suite of **REST APIs** that provide **sync access to the CDP**. **CRUD operations** are available on individual guest profiles and orders.
        - Usage: Set a customer attribute and make it available to CDP resources. Use a **Data Extention Resource**, which is a JSON Squema Object with specific key-value pair.

- Batch API:
    - **Large volume of guests and order data** that is imported using CDP's standard JSON schema.
        - Greater flexibility in guest segmentation.
        - A more comprehensive single customer view.
        - Higher sophistication of decision logic.   
    - Typically used for **initial upload of all historical data** to store against the customer profile.
    ```shell
        curl -X GET https://{apiEndpoint}/v2/batches -u $YOUR_API_KEY_ID:$YOUR_API_KEY_SECRET -H 'Accept: application/json'
    ```