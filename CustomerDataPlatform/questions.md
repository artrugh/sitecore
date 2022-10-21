### Training questions and answers:

1. Operational dashboards update every **15 seconds.**

2. CDP can process a guest's behavioral data, such as when they clicked, viewed or added an item to their cart. Each instance of **behavioral data** is called **Event**.

3. Use **Batch API** to update the data extensions on a **large number** of Guest profiles.

4. The **Stream API** only supports using the indetifiers object when sending an **IDENTITY event.**

5. Configure the Page Targeting, when you want to show a UI in an specific page.

6. If you **lower** the confidence level of an Experiment, the required minimum sample size to reach statistical significance **reduces** and the time until the test is conclusive **reduces.**

7. When you find and issue, try to reproduce it.

8. When you set up a connection for the users to use an **AI component** in **Decision Model Variants**, you include a parameter in the request URL configuration to enable users to pass a parameter from the Decision Model Variant to the AI model: *parameter=${value}*.

9. To set up a A/B test, it is required information: the base rate of customers completing an order.

10. Remember to connect the **Knowledge Source** to the **Decision Table** on the canvas, to make available the offers for selection when entering an Output in a **Decision Table.**

11. The _boxeverq object acts as a queue, **first-in-first-out** data structure that collects function calls until boxever-min.js is ready to execute them. Call *_Boxeverq.push()* to add data to the queue.

12. When you create a Full Stack Interactive Experience check to:
    - set a primary goal.
    - don't restrictive too much the audience filter, so you allow enough Experience executions.

13. When creating a **Web Experience** to personalize a homepage carousel banner, be aware that there is a potential issue: Web Experiences run after the JavaScript library is loaded, because of that, there is potential for **flicker**.

14. **NOT Personally identifiable information (PII)** need to be stored in CDP. External identifiers or hashed values can be used as well.

15. **API Response Test tool** help to:
    - Configure the Experience Response.
    - Test Experience Execution.

16. Data on the Performance screen is updated daily (24hs).

17. Stream API is used for:
    - Capture behavioral data that feeds the CDP to ensure that **Decisioning** has the most up to date Guest data for use in personalization Goals.
    - Keep track of items added to the cart. If sessions closes without an order, send to the Guest an email with the cart contents.
    - Send **identity events** that contain and use the indentifiers object to identify Guests.
    - **NOT** to Import **large amount** of offline data in order to support greater flexibility in Guest Segmentation. In that case, use the **Batch API**.

18. If during testing, a **Full Stack Interactive Experience** returns an **error**, look at the **execution report** for the experience in the API response.

19. If you want to include the same users in two different A/B tests, choose the guests to be in the control group and exclude their guest references using a **real-time audience** in both experiences.

20. If an experiment with a A/B test has been running by more than 30 days, and the **number of sessions** has not reached the required sample size, the test will be still running.

21. If an **Anonymous profile** is created when a first event was sent to CDP, you type Boxever.getID() in your Browser's Console to return the browser ID, and you search the **Guest Profile** with the id in the CDP, but no events data is returned, means that **Point of Sale** have not been setup correctly.

22. Decision Models can be added to multiple experiences without changing anything.

23. If you want to target customers that have a common behaviour (check for a destination place in a airline organization), you can create both
    - a segment.
    - a real-time audience of customers that have viewed flights to Tokyo.

24. If you need to send monthly a **personalized experience** use the **Batch Flow**.

25. If you want to test a Decision Model Variant against a Guest, move the Decision Model Variant to the **Draft state**, and use the **Test Canvas** feature.

26. When you need to create an Experience for the homepage of a native mobile application, use the **Interactive Full Stack Experience**.

27. If a guest is experiencing issues with the Decision Model, you can use the **Test Canvas** with the Guest's ID reference.

28. If you want to roll out an experiment to live to just 5% of the site visitors:
    - Set 6 of the 120 audience buckets to be part of the variant group.
    - Adjust the traffic allocation for the experiment to 5%.
    - Make the traffic split 5% to the variant and 95% to a controlgroup.
    - **DONT** set the desired population percentage to 5% in the real-time audience.

29. If **real time prices** are required for an Experience, use an external connection on the **Decision Model** to request real time price information from an API.

30. To investigate a customer case who doesn't receive the expected personalized content from a **Full Stack Triggered Experience with a Decision Model**:
    - Check the customer's timeline and the experience execution.
    - Look at the execution report for the customer.
    - Use a test canvas to replicate the results.
    - **Dont** mesure the performance of the experience.

31. To capture all the UTM patameters into the URL and send them to CDP as part of the view event:
```js
var viewEvent = { channel="WEB", ...};
viewEvent = Boxever.addUTMParams(viewEvent);
Boxever.eventCreate(viewEvent, (data) => {}, "json")
```

32. The **bx_bucket_number** performs allocation for each Web Experiment that is live on your site during the particular session.

33. Testing if events are sending through in the correct manner:
    - **Browser Developer Tools console** while interacting with the website to check JavaScript errors.
    - **Browser Developer Tools Network** monitor and filter by "boxever".
    - Test events using a testtool such as **Postman**.
    - **DONT** monitor the Browser Developer Tools Local Storage and watch the Boxever value.

34. If you want to send and email and a SMS to a customer, after the cart was abandoned, apply two triggered Full Stack experiences:
    - email service provider.
    - SMS service provider.