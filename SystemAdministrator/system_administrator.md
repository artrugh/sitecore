## Sitecore default topologies

The **Experience DB** contains all the contact interaction data about visitors to your website and also provides valuable information to enable highly-advanced marketing funtionality.

Process, aggregate and index data is the basis for **personalization**.

Sitecore Experience Manager, combined with **data collection** and **reporting functionalities of xConnect and xDB**, helps to deliver best experiences and products.

Sitecore contains more than 50 logical system roles or entities. They can be grouped and described from different perspectives:

- by product
- by type
- by combination

Two key roles:

- **Content Delivery** 
    - It handles requests from website visitors and to serve and render the content in the correct format.
    - It determines which content to serve and renders output in the relevant format for the channel.
    - It can be hosted IIS or the Azure App Service.
- **Content Management**
    - It serves the Sitecore management interface and enables Content Authors to create, manage, and publish content.

Two important services:

- Experience Database (xDB): the collection of services and storage roles that store and process experience data.

- xConnect: set of services that sits between xDB and any trusted client, device or interface that wants to collect and search experience data over HTTPS.

Topologies:

- Web Deploy Packages, zip files that contain everything you need to set up a role or role combinations.

- Configuration files (or Azure Resource Manager templates in Azure) for each role or resource that define parameters used during installation.

### Sitecore Experience Manager

XM allows to run Sitecore Experience Platform without enabling xDB or puchasing xDB licenses.

You can create, manage and publish content to your websites.

However, any functionality that depends on data collection will be unavailable, and a number of applications, will be incompatible with the Content-Management-System-only-mode. Features such as personalization or Sitecore Forms will be limited.

It is a good choice when **personalization** is not desire.

It requires:

- Sitecore XP 9.1 or later.
- A SQL server.
- A server environment that has a content management and content delivery.
- A valid Sitecore XM license.

#### Stand-Alone Services

- Data Exchange framework: enables to synchronize data to and from Sitecore and any other database or system.

- Private Session State Store: Temporary storage related to session data for active visitors, which includes metadata for active visitors and active visists for personalization. It can be hosted on SQL Server, Redis, Azure SQL, or Azure Redis.

- Shared Session State Store storages information about the current contact state and related data, including all data unique to a contact that can be shared across simultaneous sessions.

- Device Detection role: A SaaS Cloud service that provides continuosly updated information on hardware and is based on User Agent string.

- IP Geolocation role: Web service that looks up the approzimate geographic location of an IP address.

- Content Publishing role publishes content from the Master database to Web database and it is an optional replacement for the Sitecore publishing methods that are part of the Content Management role. You can scale it, having multiple Content Publishing instances.

### Sitecore Experience Platform

It contains the roles, application pools, and instances that belog to Sitecore Experince Manages, as well as xDB instances and roles. It can be single or scaled. It is recommended to use XP Single only for local environments.

Sitecore Experience Platform is usuful when a client needs personalization in real time. 

For better performance the CD servers can be arrange into clusters.

### Content Manager Role

It has access to multiple DBs, such as **CoreDB**. This DB is used by CM role to store and retrieve the configuration and settings. It is also used to store state information, such as users preferences, and to host the standard Microsoft ASP.NET membership database for security users and roles.

It also has access to the **Master DB**, which stores the master copy for all versions of every content item or media, unpublished or published.

When content is updated or added to the Master database, the Content Management role adds the updated content to the Master index.

### Sitecore Experience Commerce

It provides all the tools to manage e-commerce storefront and allows marketers and merchandisers to fully personalize the end-to-end shopping experience at all stathes od a transaction.

It also provides individual customer data (services placed int the cart, purchase history). This allows to customize user experince on run time.


### Basic building blocks

- templates
- items
- fields


Sitecore uses **items** to store information that can make up the content on a website.

They can be created, edited and deleted via de Experience Editor or the Content Editor.

It implements a hierchical database model that organize data in three structures:

- Content tree.
    - try to mirror the site structure to simplify the building of navigation and applying security.

    - Content should be place under Home Item

    - Always use **Insert Options** to allow Content Authors to create content. They defines the type of item users can create as a child of that item.

- Templates
    - they are items that define items structure.
    - store templates using folders (base templates, page templates)

## Sitecore Experience Editor

