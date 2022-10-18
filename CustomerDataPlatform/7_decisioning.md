### Decisioning

- Visually define business logic in the canvas.
- Combine rules, AI, and programmable logic.
- Activate real-time customer context from Boxever CDP to support decisions.
- Decision table can be used to map next best actions.

Decision Model:

`Use No Code Templates to allow non technical users to easily create and manage experiences without IT involvement.`

- Input Data:
    - Data from the CDP: Sessions, Guest, Orders, etc that is passed into the Programmable element. 
- Programmable:
    - Collects all the data and returns a JavaScript object, output reference "map".
    - Indetify a piece of information from the input:
        - Viewed Products
        - Get Age
        - Get Product Properties
        - Products Purchased
- Decision Table: Next Best Offer.
    - Each table contains:
        - Inputs for each **Programmable** that can be configured: Age >= 30.
        - Output: Recommendation bases on the config of the Input table: if lastViewdProduct === Car && Age > 30, then recommend "Car Insurance". 
- Knowledge Source: Offers.
- Offer: the Decision Table is linked to an Offer node.
- External Systems: make requests to external services and use the reponse to inform the decision.
    - Data System, Analitical Model, AI.

There are two ways of returning content from the Decision Model into the experience.
- One or more Offers.
- Accessing the output of a Programmable node.
