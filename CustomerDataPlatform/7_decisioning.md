### Decisioning

- Visually define business logic in the canvas.
- Combine rules, AI, and programmable logic.
- Activate real-time customer context from Boxever CDP to support decisions.
- Decision table can be used to map next best actions.

Decision Model:

`Use No Code Templates to allow non technical users to easily create and manage experiences without IT involvement.`

- Input Data:
    - Data from the CDP: Sessions, Guest, Orders, etc. 
- Programmable:
    - Indetify a piece of information from the input: Viewed Products, Get Age, Get Product Properties, Products Purchased.
- Decision Table: Next Best Offer.
    - Each table contains:
        - Inputs for each **Programmable** that can be configured: Age >= 30.
        - Output: Recommendation bases on the config of the Input table: if lastViewdProduct === Car && Age > 30, then recommend "Car Insurance". 
- Knowledge Source: Offers.
- External Systems: Data System, Analitical Model, AI.

