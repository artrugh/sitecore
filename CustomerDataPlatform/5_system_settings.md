### System Settings

- Add a user to CDP.
- Edit a user.
- Delete a user form CDP.
- Delete a guest to comply with **Global Data Protection Regulation(GDPR)**. It can take up 24hs to delete the data.
    You must have:
    - Enterprise Admin.
    - Sitecore Support.
    - or Sitecore Service role.
- Enable feature flags - Only Enterprise User Manager role.
    - The feature that you can enable depend on your role. The most common one is **access to the debug feature**.
- Configure company Information.
    - Company name.
    - Time Zone.
    - Currency.
    - Language.
    - Data Format.
    - Cookie Domain.
    - Contact Email.
    - COntact Phone.

#### Manage API

*Only Enterprise Admin Role.

You need:
- client key: Unique identifier that CDP uses to authenticate the client it receiver API cals. Activate JavaScript library on the client side to start capturing guest behaviour.
- API token: Authenticate any of the services.

#### Roles

CDP provides roles that can be assign to users(customer, partners, and employees) to grant permissions to entities.

| Role | Description | Permissions |
| --- | --- | --- |
| Enterprise Admin | external CDP admin. |<ul><li> View guest profiles </li><li> Manage segments </li><li> Dashboards </li><li> API access </li><li> Manage company information </li><li> Manage identity rules </li><li> Manage users </li></ul> |
| Enterprise Designer | external enterprise developers. |<ul><li> View guest profiles </li><li> Manage segments </li><li> Dashboards </li><li> View identity rules </li></ul>|
| Enterprise Reader | external role enables users to view guest profiles, dashboard, etc. |<ul><li> View guest profiles </li><li> Dashboards </li></ul> |
| Sitecore Support | internal role for Sitecore employees. |<ul><li> View guest profiles </li><li> Manage segments </li><li> Dashboards </li><li> API access </li><li> Manage company information </li><li> Manage identity rules </li><li> Manage users </li></ul> |
| Sitecore Services | internal role enables users to demostarte guest profiles and manage users. |<ul><li> View guest profiles </li><li> Manage users </li></ul> |
| Partener Sandbox: API Access But No Role Management | sitecore partner that enables API access. |<ul><li> Manage API access </li></ul> |