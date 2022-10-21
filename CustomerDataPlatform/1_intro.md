## Customer Data Platform and Personalization

### CDP

It is a **packaged software** that creates a **persistent and unified customer database** that is accessible to other systems.

Basically, CDP is a centralized store for customer information.

CDP consists of 4 important components:

1. Customer Data Platform: Activate historic and live customer data with a real-time CDP.
2. Decisioning: Select **next-best-actions** based on live customer and business context.
3. Experimentation: Test, optimise, repeat. Evolve faster with data-drive experimentation.
4. Experiences: Deliver relevant, engaging and profitable experiences.

#### Benefits

- Consolidation: CDP, **experimentation, decisioning, experiences** in one platform.
- First parties cookies: CDP creates a consistent customer profile and stores it so that a **single record** is produced.
- Third-party data is used to create a concentric **holistic view of a customer.**
- The data is taken and shared within the company to create customer-first experiences.
- Orchestration: the *quarterback* for the CX ecosystem.
- Scale 150ms response times, horizontal scalability.
- Velocity: agile approach.
- Data Activation: unchained insights and AI activated at point of interaction.
- SaaS: No neccesary upgrades, performance monitoring, quick time to value.

#### Sitecore CDP Priciples:

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
    - **Sitecore batch segmentation** enables you to see the volatility and variability of segments to ensure you capture the right people and respond to changes in the market. When creating a segment, think about:
        - which one has the **more potential.**
        - which is the **most important.**
        - **how easy can be identified** who belong to it.
4. Activation: 
    - Content can be created for each segment individually. Sending segments to engagement tools to trigger:
        - email campaigns.
        - mobile messaging.
        - social media campaigns.

### Personalize

Sitecore Personalize leverages/influences the data captured by CDP to deliver **targeted experiences to users across every digital experience.**

#### Sitecore Personalize Process:

1. Decisioning:
    - Decisions are managed in an interactive canvas **Decision Models** that translates your business logic into a **model** and automates the **Next Best Action** in real-time. They allows complex decisions to be broken down into easier to manage and describable components. They provide transparency as to why specific decisions/actions are taken.
        - Visually draw business logic with **drag and drop decision models** to select **next best actions**.
        - Combine **rules, AI and programmable** logic.
        - **A/B and silent testing** ensure models are optimised to meet your goals.
        - Activate **real-time customer context** from Boxever CDP to support decisions.
        - Connect **real-time business context** (inventory, price, risk, credit score, etc) to support decisions.
    - Rules and predictive analytics to make smart decisions:
        - customers to talk to.
        - things to talk to customers about.
        - channels to talk to customers in.
        - times to talk to customers.
    - Decisioning can use sources from **external services** that are not neccesary related with customer (Price, Inventory, Risk).
    - Desicion Model:
        - Input Data:
            - Data from the CDP: 
                - Sessions 
                - Guest 
                - Orders 
        - Programmable:
            - Collects all the data and returns a JavaScript object, output reference "map".
            - Identify a piece of information from the input:
                - Viewed Products
                - Get Age
                - Get Product Properties
                - Products Purchased
        - Decision Table
            - Set the Next Best Offer.
            - Each table contains:
                - Inputs for each **Programmable** that can be configured: Age >= 30.
                - Output: Recommendation bases on the config of the Input table: if lastViewdProduct === Car && Age > 30, then recommend "Car Insurance". 
        - Knowledge Source
            - Set Offers.
        - Offer
            - The Decision Table is linked to an Offer node.
        - External Systems
            - make requests to external services and use the response to inform the decision.
            - Data System, Analitical Model, AI.

2. Experimentation:
    - Test, run, and repeat. Evolve faster with data driven experimentation.
    - Create controlled and random experiments variants to improve:
        - clicks.
        - purchases.
        - website metrics.
    - Add goals to the experiments to align changes with the outcomes important to your business and take the guesswork out of establishing which **experiences resonate most with your customers.**
    - View inbuilt analytics to track the progress of your experiments within the tool.
    - Characteristics:
        - easy to deploy.
        - advanced targeting capabilities and segmentation.
        - CDP Backend.
        - decisioning.
        - custom Goals.
        - A/B/N Experimentation.
        - performance analytics.
    - Types:
        - **Web Experiments** consists in personalization A/B test on web pages. It is an **offer, next best action, operational message**, or any other customer experiment that can run on the web or be deployed into a web-based application.
            - Add a Variant:
                - Select Web Experiment Template: HTML, CSS, JS.
                    - UI elements:
                        - Design layout.
                        - Images - including the wow-factor, placement, number, and style.
                        - Headlines - varying the content, length, size, font, and so on.
                        - Company branding.
                        - Text - changing the content, style, font, size, and placement.
                        - Call-to-action (CTA) buttons - changing the text on the button, varying the sizes, colors, and page placement.
                - Set traffic allocation to specify the percentage of guests that will be exposed to the personalization configured in the web template.
            - Configutation:
                - Page targeting.
                - Audience.
                - Decisioning.
                - Goals.
            - Set:
                - confidence level: threshold for refecting the **null hypothesis**. default 95%.
                    -  \- confidence level - minimun sample size - time + errors
                - base rate: base conversion goal. default 15%.
                - minimum conversion goal difference: default 2%.
        - **FullStack Experiments**
            - Interactive
            - Triggered

3. Experiencies:
    - Deliver relevant, engaging and profitable experiences.
    - Integration of *physical* and *digital* channels, to offer a **unifed customer experience.**
    - Channels: 
        - mobile.
        - web.
        - chatbots.
    - Experiencies can incorporate **Decision Models** to make the experience truly personal.
        - Trigger Experiencies
            - Send Message: when a customer performs an Event, a decision is evaluated, and a message is sent(SMS, Email, etc) to the customer.
        - Web Experiencies
            - Add functionalities to webs and mobile web.
            - Client side testing and personalization.
        - FullStack Experiencies
            - Add functionalities to any channel.
            - Server side testing and personalization.

4. **Sitecore audience sync**
    - It is an export of **segment data** to an external destination such as a social media platform to power an ad campaign.
     1. Create a Connection
     2. Create Audience Sync Template 
        - condition
        - configurations
        - service credential
    3. Create Audience sync
        - set the schedule

#### Integration Process:

1. CDP => download boxever.js => website
2. Website => request Unique ID => CDP(Stream API - Browser API)
3. CDP (Stream API - Browser API) => Cookie User => website
4. Website => send behavioral data => CDP (Stream API - Event API)
5. Website => request Interaction Data => CDP (Interactive APIs - Interactive Rest API)
6. CDP (Interactive APIs - Interactive Rest API) => Send Interaction Data => Website

Basic integration:
- The JavaScript library that is loaded on the website, performs an async call to the **Stream API**, where the **Browser API** responds with a **cookie for the user.**
- After the new cookie is sent, it's possible to track events and send behavioral data to the **Event API**.
- **Sitecore Personalize** provides lightweight access to the CDP for personalization through the **Interactive API.**

### Sitecore Technologies

- **Sitecore xDB** provides access to customer data and can handle large quantities of data.
- **Sitecore AI** indentifies visitor trends to power personalization, modify pages, and segment customers.
- **Sitecore CDP** stores and manages customer data, complete with real-time data, tracking and integration.
- **Sitecore Cortex** provides marketers with efficient and advanced data processing.