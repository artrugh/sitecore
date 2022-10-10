## Customer Data Platform and Personalization

### CDP

It is a **packaged software** that creates a **persistent and unified customer database** that is accessible to other systems.

Basically, CDP is a centralized store for customer information.

#### Sitecore CDP Process:

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
    - Create controlled and random experiments to improve:
        - clicks.
        - purchases.
        - website metrics.

2. Decisioning:
    - Rules and predictive analytics to make smart decisions:
        - customers to talk to.
        - things to talk to customers about.
        - channels to talk to customers in.
        - times to talk to customers.

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

- Stream API:
    - Capture real-time, high velocity, and high-volume **behavioral data**. Typically deployed via Sitecore's lightweight JavaScript library for:
        - web.
        - mobile web.
        - mobile app.
        - call-center behavioral tracking.
    - Types:
        - **Event API** allows for event-processing, setting event via mobile and web.
        - **Browser API** extends functionality and manages cookies that help identify guests, further facilitating personalization. These Browser APIs are used for **capturing and consuming data.**

- Interactive API:
    - Suite of **REST APIs** that provide **sync access to the CDP**. **CRUD operations** are available on individual guest profiles and orders.

- Batch API:
    - Large volume of **guests and order data** that is imported using CDP's standard JSON schema.
    - Typically used for **initial upload of all historical data** to store against the customer profile.

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
    - Decisions are managed in an interactive canvas that translate your business logic into a **model**, leveraging the real-time customer profile behavioural events that are accessed by the CDP.
    - Automates the **Next Best Action** in real-time.
    - Experiencies can incorporate **Decision Models** to make the experience truly personal.

- Experimentation:
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