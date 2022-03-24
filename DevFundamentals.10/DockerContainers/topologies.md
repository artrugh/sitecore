## Sitecore Topologies

Sitecore XP 10.0 has 3 specific topologies designed for containers: **XP Workstation**, **XM Server**, and **XP Server**.

### Sitecore Experience Platform Workstation

It is design to be used as a **Developer workstation for Docker** if you are looking to **reduce memory overhead, download size, or complexity**, and to **improve startup or shutdown time**.

Roles in **non-production** environment:

- Content Management (standalone)
- xConnect Server (standalone)
- xDB Search Worker
- Marketing Automation Engine
- Sitecore Cortex Processing Engine
- Microsoft SQL Server
- Apache Solr
- RedisLabs Redis Server
- Traefik Revers Proxy

### Sitecore Experience Manager Server

It is designed to be use in **production and non-production environments** for Docker. It **reduces deployment time** and **lower the resource overhead** in **non-production** environments.

This is accomplished by **removing the Content Delivery role** from the Docker Compose Configuration.

Roles in **production** environment:

- Content Management
- Content Delivery
- Sitecore Identity Server

Roles in **non-production** environment:

- Microsoft SQL Server
- Apache Solr
- RedisLabs Redis Server
- Traefik Revers Proxy

### Sitecore Experience Server

It is designed for **production and non-production** environments for Docker. It is used to mimic the **exact configuration** that is used in production. The resources to run this configuration are significant.

Roles in **production** environment:

- Content Management (standalone)
- Content Delivery
- Sitecore Identity Server
- xDB Processing
- xDB Reporting Service
- xDB Collection Service
- xDB Search Service
- Marketing Automation Service
- xDB Reference Data Service
- Sitecore Cortex Processing Service
- Sitecore Cortex Reporting Service
- xDB Search Worker
- Marketing Automation Engine
- Sitecore Cortex Processing Engine

Roles in **non-production** environment:

- Microsoft SQL Server
- Apache Solr
- RedisLabs Redis Server
- Traefik Revers Proxy