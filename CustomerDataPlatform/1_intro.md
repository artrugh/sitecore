## Customer Data Platform and Personalization

### CDP

It is a **packaged software** that creates a **persistent and unified customer database** that is accessible to other systems.

Basically, CDP is a centralized store for customer information.

CDP consists of 4 important components:

1. Customer Data Platform: Activate historic and live customer data with a real-time CDP.
2. Decisioning: Select next-best-actions based on live customer and business context.
3. Experimentation: Test, optimise, repeat. Evolve faster with data-drive experimentation.
4. Experiences: Deliver relevant, engaging and profitable experiences.

#### Sitecore CDP Process:

Customer Data:

1. Data Collection:
    - The CDP collects **first party data** to create better customer profiles.
    - Data: Individual-level customer data from multiple sources, **online and offline**.
        - Type of data:
            - preferred channels, most active days, personal contact information, and spend insights.
            - channel session types.
            - supplemental service inclination.
            - loyalty data*.
            - service history.

2. Profile unification:
    - It consolidates profiles and connects specific attributes to specific indentities.

3. Segmentation:
    - Collected data can be assigned to a segment withing the CDP. Each segment contains a **subset of users** that shares common attributes (age-location-goals), behaviours, or transactions.

4. Activation: 
    - Content can be created for each segment individually. Sending segments to engagement tools to trigger:
        - email campaigns.
        - mobile messaging.
        - social media campaigns.

### Personalize

Sitecore Personalize leverages/influences the data captured by CDP to deliver **targeted experiences to users.**

#### Sitecore Personalize Process:

1. Experimentation:
    - Create controlled and random experiments variants to improve:
        - clicks.
        - purchases.
        - website metrics.
    - Add goals to the experiements to align changes with the outcomes important to yor business.
    - View inbuilt analytics to track the progress of your experiments within the tool.
    - Types:
        - **Web Experiments** consists in personalization A/B test on web pages. It is an **offer, next best action, operational message**, or any other customer experiment that can run on the web or be deployed into a web-based application.
            - Add a Variant:
                - Select Web Experiment Template: HTML, CSS, JS.
                - Set traffic allocation to specify the percentage of guests that will be exposed to the personalization configured in the web template.
            - Configutation:
                - Page targeting.
                - Audience.
                - Decisioning.
                - Goals.
            - UI elements:
                - Design layout.
                - Images - including the wow-factor, placement, number, and style.
                - Headlines - varying the content, length, size, font, and so on.
                - Company branding.
                - Text - changing the content, style, font, size, and placement.
                - Call-to-action (CTA) buttons - changing the text on the button, varying the sizes, colors, and page placement.

2. Decisioning:
    - Rules and predictive analytics to make smart decisions:
        - customers to talk to.
        - things to talk to customers about.
        - channels to talk to customers in.
        - times to talk to customers.
    - Decisioning can use sources from external services that are not neccesary related with customer (Price, Inventory, Risk).

3. Omnichannel experiencies:
    - Integration of *physical* and *digital* channels, to offer a **unifed customer experience.**
        - Channels: 
            - mobile.
            - web.
            - chatbots.
    - Personalize includes the delivery of relevant, engaging, and profitable experiences. This is where the gathered data is acted on by adding enhancements such as overlays, popups, etc.

#### Benefits

- First parties cookies: CDP creates a consistent customer profile and stores it so that a **single record** is produced.
- Third-party data is used to create a concentric **holistic view of a customer.**
- The data is taken and shared within the company to create customer-first experiences.

#### How does it work?

CDP can ingest data from all data sources **across multiple channels.**

Once ingested, the data is appended against relevant guest profiles to create a holistic view of the customer.

#### Methods

##### Integration Process:

1. CDP => download boxever.js => website
2. Website => request Unique ID => CDP(Stream API - Browser API)
3. CDP (Stream API - Browser API) => Cookie User => website
4. Website => send behavioral data => CDP (Stream API - Event API)
5. Website => request Interaction Data => CDP ( Interactive APIs - Interactive Rest API)
6. CDP ( Interactive APIs - Interactive Rest API) => Send Interaction Data => Website

- Stream API:
    - Only use to write data to CDP.
    - Capture real-time, high velocity, and high-volume **behavioral data**. Typically deployed via Sitecore's lightweight JavaScript library for:
        - web.
        - mobile web.
        - mobile app.
        - call-center behavioral tracking.
    - Types:
        - **Event API** allows for **event-processing**, setting event via mobile and web.
            GET https://{apiEndpoint}/v1.2/event/create.json?client_key={{CLIENT_KEY}}&message={...}
        - **Browser API** extends functionality and manages **cookies** that help identify guests, further facilitating personalization. These Browser APIs are used for **capturing and consuming data.**
            GET https://{apiEndpoint}/v1.2/browser/create.json?client_key={{CLIENT_KEY}}&message={...}

- Interactive API:
    - Consume data from the CDP.
    - Suite of **REST APIs** that provide **sync access to the CDP**. **CRUD operations** are available on individual guest profiles and orders.
        - Example: for set a customer attribute and make it available to CDP resources, use a **Data Extention Resource**, which is a JSON Squema Object with specific key-value pair.

- Batch API:
    - **Large volume of guests and order data** that is imported using CDP's standard JSON schema.
        - Greater flexibility in guest segmentation.
        - A more comprehensive single customer view.
        - Higher sophistication of decision logic.   
    - Typically used for **initial upload of all historical data** to store against the customer profile.
    ```shell
        curl -X GET https://{apiEndpoint}/v2/batches -u $YOUR_API_KEY_ID:$YOUR_API_KEY_SECRET -H 'Accept: application/json'
    ```

#### Functions

- Audience sync:
    - **Sitecore batch segmentation** enables you to see the volatility and variability of segments to ensure you capture the right people and respond to changes in the market. When creating a segment, think about:
        - which one has the **more potential.**
        - which is the **most important.**
        - **how easy can be identified** who belong to it.
    - **Sitecore audience sync** enables you to export your highly targeted segment for targeted campaigns.

- Basic integration:
    - The JavaScript library that is loaded on the website, performs an async call to the **stream API**, where the **Browser API** responds with a **cookie for the user.**
    - After the new cookie is sent, it's possible to track events and send behavioral data to the **Event API**, a company can request interaction data.
    - **Sitecore Personalize** provides lightweight access to the CDP for personalization.

- Personalization:
    - It is underpinned by CDP dataset and leverages the CDP data and analytical insights. It allows customers to personalize every interaction seamlessly across every digital experience.

- Decisioning:
    - Decisions are managed in an interactive canvas that translates your business logic into a **model**, leveraging the **real-time customer profile behavioural events** that are accessed by the CDP.
    - Automates the **Next Best Action** in real-time.
    - Experiencies can incorporate **Decision Models** to make the experience truly personal.

- Experimentation:
    - Test, run, and repeat. Evolve faster with data driven experimentation.
    - It takes the guesswork out of establishing which **experiences resonate most with your customers.**
    - Users can create and try on experiences, analyze results, test and deploy them, without technical support, using the canvas and the tables.
    - Characteristics:
        - easy to deploy.
        - advanced targeting capabilities and segmentation.
        - CDP Backend.
        - decisioning.
        - custom Goals.
        - A/B/N Experimentation.
        - performance analytics.

- Experiencies:
    - Deliver relevant, engaging and profitable experiences.
        - Trigger Experiencies
            - Send Message: when a customer performs an Event, a decision is evaluated, a and a message is sent(SMS, Email, etc) to the customer.
        - Web Experiencies
            - Add functionalities to webs and mobile web.
            - Client side testing and personalization.
        - FullStack Experiencies
            - Add functionalities to any channel.
            - Server side testing and personalization.

#### Decision Models

Decision Models can be built on a whiteboard. They allows complex decisions to be broken down into easier to manage and describable components. They provide transparency as to why specific decisions/actions are taken.

Features:

- Visually draw business logic with **drag and drop decision models** to select **next best actions**.

- Combine **rules, AI and programmable** logic.

- **A/B and silent testing** ensure models are optimised to meet your goals.

- Activate **real-time customer context** from Boxever CDP to support decisions.

- Connect **real-time business context** (inventory, price, risk, credit score, etc) to support decisions.

### Benefits

- Consolidation: DCP, experimentation, decisioning, experiences in one platform.
- Orchestration: the *quarterback* for the CX ecosystem.
- Scale 150ms response times, horizontal scalability.
- Velocity: agile approach.
- Data Activation: unchained insights and AI activated at point of interaction.
- SaaS: No neccesary upgrades, performance monitoring, quick time to value.

### Sitecore Technologies

- **Sitecore xDB** provides access to customer data and can handle large quantities of data.
- **Sitecore AI** indentifies visitor trends to power personalization, modify pages, and segment customers.
- **Sitecore CDP** stores and manages customer data, complete with real-time data, tracking and integration.
- **Sitecore Cortex** provides marketers with efficient and advanced data processing.