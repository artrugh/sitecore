### Send Orders to CDP

- Use **real-time order submission** with the **Stream API** when order details are available and one of the following conditions is true:
    - Your organization uses cookies and local storage to capture order details.
    - Your organization manages orders using a third-party system such as OrderCloud.
        1. Send an ORDER_CHECKOUT event.
- Use **real-time order assembly** with the **Stream API** when order details are not available and one of the following conditions is true:
    - Your organization's implementation of Sitecore CDP does not use cookies.
    - Your organization does not manage orders using a third-party system such as OrderCloud.
        1. Send an ADD event. 
        2. Send an ADD_CONTACTS event. 
        3. Send a CONFIRM event. 
        4. Send a CHECKOUT event.
- Use **offline order submission** with the **Batch API** when you want to do any of the following:
    - Submit a large amount of historical orders from a data lake or data warehouse as a once-off, when your organization first integrates with Sitecore CDP.
    - Submit offline orders from a third-party system, such as a call center.
    - Submit orders for guests who block cookies or who use an anonymous browser.
    - Submit complete orders if your organization submits partial orders using Stream API.
    - Update orders submitted with Stream API on a daily basis.
        1. Use Batch API.