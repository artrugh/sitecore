## Sitecore Security

The Sitecore security model enables you to grant or deny access to almost every aspect of the website.

To do this, you must use **security accounts** and **security domains** to control access that users have to **items and content** on their website as well as the access they have to Sitecore.

- Security Account
    - User
        - Name
        - Domain
        - Email
        - Password
    - Role
        - Collection of Users

- Security Domain
    - Collection of security accounts
    - Rules and Procedures

Globlal Roles that are used accross domains.
- *App_Config/Security/GlobalRoles.config*

- Engine: .NET Security Engine
    - plug and play Microsof features.
    - abstraccion from real data source.
    - provides an option replace or extend the default config with custom providers.
    - performance speed of a puse ASP.NET Solution.
    - keep accounts in identifiable storage areas by using several providers simultaneously.

### Security tools

- User Manager
- Role Manager
- Security Editor
- Access Viewer
- Domanin Manager
- Content Editor
- Security Tab

#### User Manager

- create, edit and delete user.
- change password.
- enable and disabled users.
- lock and unlock user.

#### Role Manager

- create and delete role.
- add and remove users and roles as members of a role.

#### Security Editor

- assig the access right that roles and users should have to the items in the content tree.
- assig access right to the security accounts.
- protect and unprotect items.
- open the **Access Viewer** and the **User Manager**.

#### Access Viewer

- overview of the access rights.
- explanation of how the current settings have been resolver.
- open **Security Editor** and **User Manager**.

#### Domain Manager

- create and delete domain (each user can have only one domain).
- especify domain is global or local *App_Config/Security/Domain.config*

#### Content Editor Security Tab

- assign access right to security accounts.
- overview of roles and users that have access right to individual items.
- change ownership of an item.
- open **Access Viewer** and **User Manager**.

#### Update Center

It is used to download, install and update.

Info:
- version number.
- breaking changes.
- note realease.
- pre and post installation.

The Sitecore configuration is divided into four layers:

- Sitecore
- Modules
- Custom
- Environment

### Password Policy

*C:/Inetpub/wwwroot/SitecoreWebsite/Website/Web.config*

- Min Required Password Length: 1
- Min Required Non Alphanumeric Characters
- Max Invalid Password Attempts

### Emails

Send email message to users who use the **Forgot your Password**.

*Sitecore.config*
<setting name="MailServer" value="email.server.net"/>
Using Security Socket Layer (SSL) 
`<system.net> <mailSettings> <smtp deliveryMethod="Network"> <network enableSsl="true"/>`

#### Edit Subject and Content of Emails

- In Content Editor / sitecore / System / Settings / Security / Password Recovery / Password Recovery Email
    - Sender Email Address: Enter a valid email address.
- Configure SMTP server to allow emials to be sent from the address.

### Enable FIPS

FIPS compliants algorithms for encryption, hashing, and signing security policy in Windows.

- File Explorer: */Website/bin/Sitecore.Kernel.dl/*
- Click properties and copy version.
- Open machine.config and edit version in crytoClass tag AESPROXY attribute.

### Item Buckets

User has not access at either the user/rolelevel or at the item/ancestor level, an itme is not retrieved.

However **Security** is not apply for search facet.

Users can see the items buckets but not edit them.

In the **Security Editor**:
- create a bucket
- revert a bucket.

### History Table and History Engine

The History Engine saves information about changes made to items in the History table. All Sitecore content databases contain this table.

By default the table is diabled for performance reasons.

Enable => remove eexample extention from the *App_Config/Include/Examples/Sitecore.HistoryEngine.config.example* file.

Tracked Item Operations:

- AddedVersion
- RemovedVersion
- CopiedItem
- CreatedItem
- DeletedItem
- MovedItem
- SavedItem
