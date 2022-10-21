### CDP data retention

CDP uses 4 data storage tier:

#### Technical storage

It keeps **actionable customer data** available for other data layers.

`Events are not store in Technical storage.`

Types of **guest**:

- customer: site visitors that have passed the organization's identity rules.
- visitor: unidentified or anonymous.
- retired: guest profile that matches another guest profile, according to the organization's identity rules.

| data entity | rentention limits | removal frequency |
| --- | --- | --- |
| customer | retains *customers* for an indefinite amount of time. | does not apply |
| visitor | retains for **six months** from the last date they were active. | weekly |
| retired | they are removed. CDP migrates the guest data, creates a retired guest profile. | weekly |
| orders | orders that belong to retired guests are removed | weekly |
| sessions | retains the guest's last 1000 sessions. | weekly |

#### Live Storage

It keeps **subset actionable customer data** available in real-time for using in **personalization.**

It is used for **big data** and powers all the guest context related:
- intelligence.
- decisioning.
- analytics features.

It contains **guest's real-time and historical behaviors and transactional data.**

`Each organization might have different data limits of time durations that apply depending on the industry's regulations.`

Those are the default one:

| data entity | rentention limits | removal frequency |
| --- | --- | --- |
| customer | retains *customers* for an indefinite amount of time. | does not apply |
| visitor | retains for **six months** from the last date they were active. | daily |
| orders | retains the guest's most recent 20 orders. | daily |
| sessions | retains the last 40 sessions within the last 90 days and a max of 10 iffline sessions. | daily |
| events | retains the last 100 events from a session. Events are stores in sessions. Only events from the last 40 sessions within the last 90 days are retained. | daily |
| guest data extensions | retains the last 100 data extensions for a guest | daily |
| guest identifiers | retains the last 50 indetifiers for a guest | daily |

#### Achival Storage

It consists of the CDP data lake. The data retention policy for archival storage **does not apply**. Data is archived and available in CDP data lake for the agreed length of the contract for powering analytics and batch data sync.

#### Data Mart

It includes **subset of data from archival storage** and it is the data store used for reporting, performance analytics, and segmentation.

| location | entity | rentention limits | removal frequency |
| --- | --- | --- | --- |
| segmentation data mart | guest, orders, and sessions | for the life of the contract | upon customer request |
| segmentation data mart | events | max of 2 years | manually |
| segmentation member history | guests | 15 days | daily |