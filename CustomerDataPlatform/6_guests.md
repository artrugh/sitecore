### Guests in CDP

CDP creates a guest profile for every person that interacts with the brand, regardless of the channel. 

Each guest has a **unique guest profile** that contains behavioral and transactional data.

This data depends on the organization requirements and identity rules.

Organizations configure identity rules to check for a matching unique identifier that is internal to the organization (layalty number, unique ID, browser reference, guest reference).

Some organizations thatuse the 2.0 data model can use **Personally Identifiable Information(PII)** to identify guests.

After indentifing the guest, CDP updates **Guest Type** from **Vistor** to **Customer**.

#### Guest types:

- Customer:
A customer is a guest that provided enough identity information according to your organization's identity rules.
- Visitor:
A visitor is a guest who has not provided enough identity information or has provided partial identity information but not enough to meet the organizations's identity rules.
- Retire:
A retired guest profile is archived because it contained data that was migrated to another guest profile. You cannot access a retired guest profile.
- Travaller *Travel Org:
It is a guest who is consumer of a flight order but has not provided enough identifiable information, usually because they did not purchase the ticket.

#### Identity Resolution in CDP.

Identity resolution is the process of identifying **anonymous guests** in CDP.

CDP uses **indetity rules** to identify guests