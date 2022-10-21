### Event Types

Each **event type** required different attributes.

Attribute **type** defines the event:
`type: "EVENT_TYPE"`

- **View Event** 
    - Include *minimum required attributes*

    It captures the guest's action of viewing a page. You must capture VIEW events on all pages where you want to track guest behavior.

    `Recommended: first event that you send and validate.`

    On any tagged page, your website sends a VIEW event when a user lands on the page and it fully loads.

    Additionally you can capture session data as a **Custom name/value pair Object** in the VIEW event.

    ```JavaScript
    const viewEvent = {
        browser_id: Boxever.getID(),
        channel: "WEB",
        // define the type
        type: "VIEW",
        language: "EN",
        currency: "EUR",
        page: "home",
        pos: "myretailsite/ireland",
        // include session data if it neccesary
        sessionData: {
            deep_link:"https://www.retailsite123.com/search?product=shoes",
            is_logged_in:true,
            assistance:false
        }
    };
    ```

- **Indetity Event** 
    
    - Include *minimum required attributes*, plus:

        - **Identifier** - Array of Object. It is the identity identifiers that are used to identify the users of your application.
            - id(required): string - The unique guest identifier provided by your organization's identity system, such as a Customer Relationship Management (CRM) system.
            - provide(required): string - The name of your organization's identity system, external to Sitecore CDP, that provided the unique guest identifier.
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

- **Search Event**

    - Include *minimum required attributes*, plus:
        - product_type: The product type the guest searched for and it is a custom value of your choice. ex: running shoes ,office supplies, FLIGHT.
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

- **Add Event**

    - Include *minimum required attributes*, plus:
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

- **Custom Event**

    - Include *minimum required attributes*, plus
        - **Custom Attribute**.

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

- **Order Event**
    - Use **real-time order submission** with the **Stream API** when:
        - order details are available and one of the following conditions is true:
            - Your organization uses **cookies and local storage** to capture order details.
            - Your organization manages orders using a third-party system such as OrderCloud.
                1. Send an **ORDER_CHECKOUT** event.
    - Use **real-time order assembly** with the **Stream API** when:
        - order details are not available and one of the following conditions is true:
            - Your organization's implementation of Sitecore CDP does not use cookies.
            - Your organization does not manage orders using a third-party system such as OrderCloud.
                1. Send an ADD event. 
                2. Send an ADD_CONTACTS event. 
                3. Send a CONFIRM event. 
                4. Send a CHECKOUT event.
    - Use **offline order submission** with the **Batch API** when:
        - you want to do any of the following:
            - Submit a large amount of historical orders from a data lake or data warehouse as a once-off, when your organization first integrates with Sitecore CDP.
            - Submit offline orders from a third-party system, such as a call center.
            - Submit orders for guests who block cookies or who use an anonymous browser.
            - Submit complete orders if your organization submits partial orders using Stream API.
            - Update orders submitted with Stream API on a daily basis.
                1. Use Batch API.
