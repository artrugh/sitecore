### Implementation

#### Integration Type

[documentation](https://doc.sitecore.com/cdp/en/developers/sitecore-customer-data-platform--data-model-2-1/walkthrough--preparing-to-integrate-with-sitecore-cdp.html)

Select an integration type from the following table, depending on your type of application.

| Type of application | Recommended integration type |
| --- | --- |
| Web application with TMS | Client-side integration using the Boxever JavaScript Library and a TMS |
| Native application with TMS | Server-side integration using the Boxever JavaScript Library and a TMS |
| Web application without TMS | Client-side integration using the Boxever JavaScript Library |
| Native application without TMS | Server-side integration using direct HTTP requests |
| Hybrid application with both WebView parts and native parts | <ul><li>For the WebView parts, choose the web application integration type that you want in this table.</li><li>For the native parts, choose the native application integration type that you want in this table.</li></ul> |

#### Required Details

- Client-side integration using the Boxever JavaScript Library:
    - Client key.
        - Organization's unique and public identifier.
    - Stream API target endpoint.
        - Use it to send real-time behavioral data to CDP. It is determined by the location of the CDP Server
    - Channel, Language, and Currency.
        - Parameters that you send from your application to Sitecore CDP during integration.
    - Name of point of sale.
    - Cookie domain.
        - **Top-level domain** of the website that you are integrating. The cookie domain ensures that the library cookie is stored in the web browser as a first-party cookie. The first character is a full stop.
            - main domain: www.myretailsite.com, cookie: .myretailsite.com
            - subdomain: beta.myretailsite.com, cookie: .beta.myretailsite.com
            - localhost: localhost:5500, cookie: empty string "".
    - Web flow target.
        - If you have chosen to integrate with Sitecore CDP using the Boxever JavaScript Library, you must determine your web flow target. The web flow target is the **path for the Amazon CloudFront CDN** for Sitecore Personalize.

    The _boxeverq object uses asynchronous syntax to create a queue possible. It acts as a queue, which is a **first-in-first-out** data structure that collects function calls until boxever-min.js is ready to run them.

    Functions run in the order that they are pushed into the _boxeverq object.
    
    To add something to the queue, use the _boxeverq.push method. Functions can contain any arbitrary JavaScript. This technique is useful for chaining calls to the API. For example, ensuring that a PAYMENT event runs before a CHECKOUT event.

- Server-side integration using direct HTTP requests:
    - Client key.
    - Stream API target endpoint.
    - Channel, language, and currency.
    - Name of point of sale.