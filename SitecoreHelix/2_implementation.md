## Helix Implementation

Breaking your implementation into multiple logically-grouped Visual Studio Solutions can be especially helpful with large scale implementations. Each Solution can target a specific subsystem such as the Commerce Engine.

Visual Studio Solution should logically group togetjer conceptual modules.

## Multitenancy

A tenant is the group of individuals responsible for maintaining a site or group of sites. (ex content editor in different countries)

You can define a common Feature and Foundation layer in the implementation whili allowing multiple Projects layer modules, one per tenant.

Each tenant should have it own Project layer module, to define their own datasource sets, page-type templates, page layouts, and sublayouts.

By defining organizational roles, users can belog to different tenants and content can be shared or separated.

## Sites

It is a concrete context to which different properties can be attributed. A multisite implementation is an implementation where content can exist in different context.

Site are define by default in the configuration files. web.config <sitecore><sites>, and the site context is resolved as part of the request for each page or context

Multisite is the concept of having multiple sites within one Sitecore implementation. (ex. multiple sites depending on countries).

Features are reusable across multiple sites or multiple tenants i your solution. But the projects modules are likely tenant or possibly site-specific.

