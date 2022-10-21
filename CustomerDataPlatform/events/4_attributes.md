### Attributes

- **Minimum required attributes**

    - browser Id - string - ex: a38b230c-11eb-4cf9-8d5d-274e9f344925​
    - channel - string - ex: MOBILE_WEB
    - type - Custom or CDP event type - ex: VIEW, IDENTITY, CLICK
    - language - string - DE, EN
    - currency - string - USD, EUR
    - page - string - name of the website where the interaction with the brand take place (custom value) - home, contanct.html
    - pos - point of sale name

#### Point of Sale

A Point of Sale (POS) is a specific storefront for which your organization sells products. There are many advantages to setting up a POS. You must be assigned an **Enterprise User Manager** or **Enterprise Admin** role in Sitecore Personalize to manage a POS.

| Field | Description |
| --- | --- |
| Name | enter a name for the POS, such as myretailsite.co.uk. |
| Market | enter the market for the POS. This might be the region or country associated with the POS, such as France. |
| Brand | enter the brand for the POS. This is the marketing brand the POS is under, such as Acme French Scarves. |
| Language | select the language for the POS, such as Fr. |
| Timeout | select the number of minutes before the browser session times out as a result of inactivity, such as 20. |


#### Browser Id

CDP assigns to every user of your application a **Browser ID**. It associates sessions, events, and orders with the respective user.

Every event that you send to Sitecore CDP must include the Browser ID. This ensures that the correct session, event, and order data is associated with the correct user.

- Client-Side
    Boxever JavaScript Library automatically creates the browser ID. Then, the web browser stores the browser ID as a **first-party cookie**. The cookie is persisted until it expires or gets deleted. When you send an event to CDP, you must include the browser ID in the event object.

    ```JavaScript
    Boxever.getID();
    ```

- Server-side
    Using direct HTTP requests, you must manually request a browser ID first. To do this, you make a GET request to the Browser API (Stream API type). The response includes the browser ID. When you send an event to Sitecore CDP, for example, a VIEW event, you must include the browser ID in the event object.

    ```C
    curl -X GET -g 'https://api.boxever.com/v1.2/browser/create.json?client_key=psfu6uh05hsr9c34rptlr06dn864cqrx'
    ```
    response
    ```JSON
    {   
        "status":"OK",
        "version":"1.2",
        "client_key":"psfu6uh05hsr9c34rptlr06dn864cqrx",
        "ref":"d324a895-72b8-458b-84ad-2090494fd79a",
        "customer_ref":"0f6f4713-ac7d-4858-8d22-01d246736d03"
    }
    ```
