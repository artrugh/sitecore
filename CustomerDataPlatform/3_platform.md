### Customer Data Platform

- Customer Data:
    - guest: all users, current online, anonymous visitors, and identified customers.
    - segments: allows to build custom, unified batch segments which blend real-time behaviours and historical order data.

- Experiencies:
    - Web: add to website and monitor performance.
    - Full stack drives API triggered and Interactive Experience.
    - Experiencies include **flows**. Flows export segments to external third-party systems for highly targeted campaigns.

- Experiements:
    - Web runs A/B tests on your website.
    - Full stack runs A/B tests on API driven triggered and Interactive Experiences.

- Decisioning:
    - Decision models allow to recommend **offers dynamically** based on your **business rules.**
    - Decision engines deliver highly personalized content and offers to customers.
    - Offers create proposal content that can be presented to a guest in multiple channels.

- Library:
    - **Web templates** create reusable marketer-friendly templates for use in web-experiences.
    - **Audience templates** create reusable templates for use in experiences.
    - **Decision templates** create reusable templates for decision models.
    - **Flow templates** define configuration, which will be used in a flow.
    - **Offer templates** create templates for offer content.

- Dashboards:
    - Customer analytics are based on a selection of reports which focus on customer behaviour and trends in your data.
    - Customer journey maps are reported which enable you to see how customers are navigating your channel.

- Connections:
    - Link to third-party systems.

- Sandbox:
    - System Settings
        - Add a user.
        - Edit a user.
        - Delete a user.
        - Delete a guest
            - to comply with **Global Data Protection Regulation(GDPR)**. It can take up 24hs to delete the data.
            - You must have:
                - Enterprise Admin.
                - Sitecore Support.
                - or Sitecore Service role.
        - API Access:
            - *Only Enterprise Admin Role.*
            - You need:
                - **client key:** Unique identifier that CDP uses to authenticate the client receiver API calls. Activate JavaScript library on the client side to start capturing guest behaviour.
                - **API token:** Authenticate any of the services.
    - Tenant
        - Enable feature flags 
            - Only Enterprise User Manager role.
            - The feature that you can enable depend on your role. The most common one is **access to the debug feature**.
        - Configure company Information.
            - Company name.
            - Time Zone.
            - Currency.
            - Language.
            - Data Format.
            - Cookie Domain.
            - Contact Email.
            - Contact Phone.