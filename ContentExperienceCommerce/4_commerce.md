
## Commerce

Complete transactions: storefronts and marketplaces, search and merchandizing.

- Sitecore Experience Commerce (XC)
- Sitecore OrderCloud
- Sitecore Discover

### OrderCloud

OrderCloud is a: **cloud-based**, **language agnostic API-first**,
headless marketplace development platform.

It incorporates: **buyers**, **sellers**, and **suppliers** in a solution delivery.

It runs in **Microsoft Azure**.

#### Cloud

| a | b |
| -- | --- |
| XP version | XP 9.0.1 |
| type of environment | dev - prod |
| location of deployment | location of microsoft azure data center or region |
| location of application insight resources to Sitecore | |
| sitecore configurations | XM xs to xm -XP xs to xp, xDB, xs to xDB |
| premium or standard tier | level of service |
| live Microsoft IDs  | email addresses of the technical contacts you want to have access to the Sitecore environment in Microsoft Azure |
| license files | license.xml |

#### Solution Design for Managed Cloud

**Recommendations**

- Estimate amount of webtraffic and use cases of each deployment.
- Consider future scenarios, locations and e-commerce.
- Consideration for spikes: Hom many visits - How to configure scalability reles to scale up and to scale down.
- Deploy Slot in Microsoft Azure Web Apps used for Staged deployments.
- Scalability: Scale servers with traffic spikes. Plan them in advice.
- Service level agreement (SLA).