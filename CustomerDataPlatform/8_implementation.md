### Implementation

#### Integration Type

[documentation](https://doc.sitecore.com/cdp/en/developers/sitecore-customer-data-platform--data-model-2-1/walkthrough--preparing-to-integrate-with-sitecore-cdp.html)

Select an integration type from the following table, depending on your type of application.

| Type of application | Recommended integration type |
| --- | --- |
| Web application with TMS | Client-side integration using the Boxever JavaScript Library and a TMS |
| Native application with TMS | Client-side integration using the Boxever JavaScript Library and a TMS |
| Web application without TMS | Client-side integration using the Boxever JavaScript Library |
| Native application without TMS | Server-side integration using direct HTTP requests |
| Hybrid application with both WebView parts and native parts | <ul><li>For the WebView parts, choose the web application integration type that you want in this table.</li><li>For the native parts, choose the native application integration type that you want in this table.</li></ul> |

#### Point of Sale

A Point of Sale (POS) is a specific storefront for which your organization sells products. There are many advantages to setting up a POS. You must be assigned an **Enterprise User Manager** or **Enterprise Admin** role in Sitecore Personalize to manage a POS.

Fields:
- Name 
    - enter a name for the POS, such as myretailsite.co.uk.
- Market
    - enter the market for the POS. This might be the region or country associated with the POS, such as France.
- Brand
    - enter the brand for the POS. This is the marketing brand the POS is under, such as Acme French Scarves.
- Language
    - select the language for the POS, such as Fr.
- Timeout
    - select the number of minutes before the browser session times out as a result of inactivity, such as 20.

#### Required Details

- Client-side integration using the Boxever JavaScript Library:
    - Client key.
        - Organization's unique and public identifier.
    - Stream API target endpoint.
        - Use it to send real-time behavioral data to CDP. It is determined by the location of the CDP Server
    - Channel, language, and currency.
        - Channel, language, and currency are parameters that you send from your application to Sitecore CDP during integration.
    - Name of point of sale.
    - Cookie domain.
        - The cookie domain is the **top-level domain** of the website that you are integrating. The cookie domain ensures that the library cookie is stored in the web browser as a first-party cookie. The first character is a full stop.
            - main domain: www.myretailsite.com, cookie: .myretailsite.com
            - subdomain: beta.myretailsite.com, cookie: .beta.myretailsite.com
            - localhost: localhost:5500, cookie: empty string "".
    - Web flow target.
        - If you have chosen to integrate with Sitecore CDP using the Boxever JavaScript Library, you must determine your web flow target. The web flow target is the path for the Amazon CloudFront CDN for Sitecore Personalize.

    The _boxeverq object makes using asynchronous syntax to create a queue possible. It acts as a queue, which is a **first-in, first-out** data structure that collects function calls until boxever-min.js is ready to run them.

    Functions run in the order that they are pushed into the _boxeverq object. To add something to the queue, use the _boxeverq.push method. Functions can contain any arbitrary JavaScript. This technique is useful for chaining calls to the API. For example, ensuring that a PAYMENT event runs before a CHECKOUT event.

- Server-side integration using direct HTTP requests:
    - Client key.
    - Stream API target endpoint.
    - Channel, language, and currency.
    - Name of point of sale.


#### Event

##### Event and Flow Data Object

[docu](https://doc.sitecore.com/cdp/en/developers/sitecore-customer-data-platform--data-model-2-1/the-event-object.html#UUID-b002a47e-869c-a187-3fa5-57b22092f441_itemizedlist-idm1903320569834268)


If you integrate with Sitecore CDP using the Boxever JavaScript Library or direct HTTP requests, use this event object to collect all the event data about a user's interaction with your application. You then send the event to Sitecore CDP.

- Flow Object
    - It should include the friendlyId of the Full Stack Experience or an Interactive Full Stack Experiment that you want to run, so CDP runs the Experience or Experiement.
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

##### Event Method

- Boxever.eventCreate(eventDataObject, callBack function, format of response), to send data to Sitecore CDP.

    ```JavaScript
    // Send the event data to the server
    Boxever.eventCreate(eventData, () => {}, "json");
    ```
- Boxever.callFlows(flow Object event data /include friendlyId/, callback ), function runs:
    - Interactive Full Stack Experience
    - Interactive Full Stack Experiment

    ```JavaScript
    const flowObject = {
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
        flowObject,
        response => console.log(response)
    );
    ```
- Boxever.AddUTMParams(event) - function adds every UTM parameter from the URL of the current webpage to the event object for tracking data.

- Boxever.getBucketNumber(callback) - update bucket number cookieto match the latest from CDP. Call this method after IDENTITY Event trigger.

- Boxever.reset()
    - Clears the event queue.
    - Deletes the browser ID and the guest reference.
    - Reloads the Boxever JavaScript Library. During loading, the Boxever JavaScript Library creates a browser ID and a guest reference.

- Boxever.templating.compile() - rerenders a Web Experience or Web Experiment that is currently live in Sitecore Personalize.

- Boxever.triggerExperiences() - reruns every Web Experience and Web Experiment that is live in Sitecore Personalize.

##### Event types

###### Browser Id

CDP assigns to every user of your application a **Browser ID**. It associates sessions, events, and orders with the respective user.

Every event that you send to Sitecore CDP must include the Browser ID. This ensures that the correct session, event, and order data is associated with the correct user.

- Client-Side
Boxever JavaScript Library automatically creates the browser ID. Then, the web browser stores the browser ID as a **first-party cookie**. The cookie is persisted until it expires or gets deleted. When you send an event to CDP, you must include the browser ID in the event object.

    ```JavaScript
    Boxever.getID();
    ```

- Server-side
    Using direct HTTP requests, you must manually request a browser ID first. To do this, you make a GET request to the Browser API (Stream API type). The response includes the browser ID. When you send an event to Sitecore CDP, for example, a VIEW event, you must include the browser ID in the event object.

    ```bash
    curl -X GET -g 'https://api.boxever.com/v1.2/browser/create.json?client_key=psfu6uh05hsr9c34rptlr06dn864cqrx'
    ```
    response
    ```bash
    {   
        "status":"OK",
        "version":"1.2",
        "client_key":"psfu6uh05hsr9c34rptlr06dn864cqrx",
        "ref":"d324a895-72b8-458b-84ad-2090494fd79a",
        "customer_ref":"0f6f4713-ac7d-4858-8d22-01d246736d03"
    }
    ```

###### Attributes

Each **event type** required different attributes.

- **Minimum required attributes**
    - browser Id - string - ex: a38b230c-11eb-4cf9-8d5d-274e9f344925​
    - channel - string - ex: MOBILE_WEB
    - type - Custom or CDP event type - ex: VIEW, IDENTITY, CLICK
    - language - string - DE, EN
    - currency - string - USD, EUR
    - page - string - name of the website where the interaction with the brand take place (custom value) - home, contanct.html
    - pos - point of sale name

- **View Event** - Include *minimum required attributes**

    It captures the guest's action of viewing a page. You must capture VIEW events on all pages where you want to track guest behavior.

    `Recommended: first event that you send and validate.`

    On any tagged page, your website sends a VIEW event when a user lands on the page and it fully loads.

    Additionally you can capture session data as a **Custom name/value pair Object** in the VIEW event.

    ```JavaScript
    const viewEvent = {
        browser_id: Boxever.getID(),
        channel: "WEB",
        type: "VIEW",
        language: "EN",
        currency: "EUR",
        page: "home",
        pos: "myretailsite/ireland",
        sessionData: {
            deep_link:"https://www.retailsite123.com/search?product=shoes",
            is_logged_in:true,
            assistance:false
        }
    };
    ```

- **Indetity Event** - Include *minimum required attributes*, plus:
    - **Identifier** - Array of Object. It is the identity identifiers that are used to identify the users of your application.
        - id*: string - The unique guest identifier provided by your organization's identity system, such as a Customer Relationship Management (CRM) system.
        - provide*: string - The name of your organization's identity system, external to Sitecore CDP, that provided the unique guest identifier.
        - expiry_date: string - The date the unique guest identifier expires. This is determined by your organization's identity system.
    - it can optionally include **personally identificable information** - PII. Some examples:
        - email.
        - title (Mr, Mrs, etc).
        - firstname
        - lastname
    
    ```JavaScript
    const identityEvent = {
        browser_id: Boxever.getID(),
        channel: "WEB",
        type: "IDENTITY",
        language: "EN",
        currency: "EUR",
        page: "home",
        pos: "myretailsite/ireland",
        identifiers: [
            {
                id: "123456",
                provider: "BXLP"
            }
        ],
        email: "jane.doe@myretailsite.com",
        firstname: "Jane",
        lastname: "Doe"
    };
    ```

- **Search Event** - Include *minimum required attributes*, plus:
    - product_type: The product type the guest searched for and is a custom value of your choice. ex: running shoes ,office supplies, FLIGHT.
        - for FLIGHT include:
            - flight_type: OW, RT.
            - origin: BCN, DUB.
            - destination: BCN, DUB.
            - start: Date.
            - end: Date.
            - adult: integer.
            - children: integer.
            - infant: integat.
            - fare_classe: Economy.
            - fare_family: Economy - Optional.

    - product_name: The product name the guest searched for: ex: airSupport, M06P-BLK pencil, 0.6mm, DUB-LON.

    ```JavaScript
    const searchEvent = {
    browser_id: Boxever.getID(),
    channel: "WEB",
    type: "SEARCH",
    language: "EN",
    currency: "EUR",
    page: "search results page",
    pos: "myretailsite/ireland",
    product_type: "running shoes",
    product_name: "airSupport"
    }

    const searchEvent = {
        browser_id: Boxever.getID(),
        channel: "WEB",
        type: "SEARCH",
        language: "EN",
        currency: "EUR",
        page: "search results page",
        pos: "myretailsite/ireland",
        product_type: "FLIGHT",
        product_name: "DUB-LON",
        flight_type: "RT",
        origin: "DUB",
        destination: "LON",
        start: "2022-08-21T16:17",
        end: "2022-08-23T07:00",
        adults: 1,
        children: 0,
        infants: 0,
        fare_class: "Economy",
        fare_family: "Economy Plus"
    }
    ```

- **Add Event** - Include *minimum required attributes*, plus:
    - product: JSON object that contains the product entity data.
    - Additionally you can capture session data as a **Custom name/value pair Object** in the VIEW event.

    The ADD event captures the product details when a user adds the product(s) to their online cart.

    ```JSON
    {
    "channel":"WEB",
    "type":"ADD",
    "language":"EN",
    "currency":"EUR",
    "page":"races",
    "pos":"myretailsite.com",
    "browser_id":"56860bff-94ba-4d84-aa37-2b5a83d5411b",
    "product":{
        "type":"BET",
        "item_id":"EXACT_90",
        "name":"Exact score after 90 minutes",
        "orderedAt":"2015-08-23T16:17:16.000Z",
        "quantity":1,
        "price":100.00,
        "productId":"CORRECT_SCORE",
        "currency":"EUR",
        "originalPrice":100.00,
        "originalCurrencyCode":"EUR",
        "referenceId":"BET_001-1"
    },
        "sessionData":{  
            "deep_link":"https://www.retailsite123.com/search?product=shoes",
            "is_logged_in":true,
            "assistance":false
    }
    }
    ```

- **Custom Event** - Include *minimum required attributes*, plus **Custom Attribute**.

    ```JavaScript
    const customEvent = {
        browser_id: Boxever.getID(),
        channel: "WEB",
        type: "myretailsite:CLICKED_POPUP",
        language: "EN",
        currency: "EUR",
        page: "home",
        pos: "myretailsite/ireland",
        // custom attributes
        clickedPopup: isPopupClicked(), // true or false
        timeBetweenPopupAndClick: `${getTimestampPopup() - getTimestampClick()} ${timeUnit}` //for example, "8 seconds"
    };
    ```

#### Cookies

A cookie is a small file that your organization places on a user’s device (such as a PC, tablet, or mobile phone) to perform identity and data capture.

The Boxever JavaScript Library places the following cookies on the site visitor's device:

##### bid_{clientKey} cookie

It persists the browser ID between sessions. It generates a Universally Unique Identifier (UUID) that is unique per browser until the cookie expires or is deleted, then a new UUID is generated. Sitecore CDP data capture cookies expire after two years of inactivity.

##### bx_bucket_number cookie

To facilitate experimentation in Sitecore Personalize, Sitecore CDP assigns a bucket number to every user of your website. The web browser stores the bucket number as a **bucket number cookie.**

This cookie allocates the Guest to a specific variant when using audience allocation . It performs allocation for each Web Experiment that is live on your site during the particular session.

It is possible that the bucket number in Sitecore CDP changes, but the bucket number cookie in the web browser remains unchanged.

If you integrate with Sitecore CDP using the Boxever JavaScript Library, you can fix this by using the Boxever.getBucketNumber() function. This function updates the bucket number cookie in the web browser to match the latest bucket number in Sitecore CDP. We recommend that you call this function after an IDENTITY event.

##### boxever_test cookie

The boxever_test cookie - checks that the other cookies are working as expected then is immediately removed from the visitor's device.

##### Third parties cookies

There are scenarios when a Sitecore CDP session cookie is similar to a third-party cookie, for example, when you enable cross-domain support. This is true when the cookie is set by a website that is distinct from the website that appears in the web address bar.

If this applies, a value is set against api.boxever.com and then the value is used in local storage to set first-party cookies across all domains.

The Boxever JavaScript Library versions 1.4.6 includes the optional _boxever_settings.itp_cross_domain setting which automatically applies the cross-domain setting only in respect to Intelligent Tracking Prevention (ITP) browsers, most commonly Safari. This ensures first-party cookies are used otherwise.

#### Local Storage

- bid_{clientkey} - the UUID (browser ID) stored against your organization's client key.

- bx_bucket_number - the bucket number between 1 and 120 inclusive that is stored in the session. This only pertains to Sitecore CDP tenants that have web experiments enabled and where you want to set the traffic allocation for the variant.

#### TTL

The Boxever JavaScript Library versions 1.4.2+ provide a property, *_boxever_settings.cookie_expiry_in_days*, that enables you to change the cookie and local storage expiry from the **default of two years.**