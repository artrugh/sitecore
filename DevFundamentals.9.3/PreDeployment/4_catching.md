## Catching

A **cache** is a **high-speed data storage layer** which stores a subset of data, increasing performance by storing copies of frequently-accessed data from external systems in a high-performance subsystem.

Sitecore offers:

- Site caching.
- Database caching.
     
### Cache layers

1. HTML cache
2. Item cache
3. Data cache
4. Prefetch cache

#### HTML cache

It plays a key role in **improving the frontend performance**. It is able to cache generated data from **lower levels of caching**, so sitecore doesn't need to reprocess the entirety of the request.

#### Item cache

It retrieves **item information**. Within the item chache, there are objects in the Sitecore class `Sitecore.Data.Items.Item`. If you requests an item that is not present within the **Item cache**, the data will be retrieved from **Data cache** and then populated and stored within the **Item cache** as an item for future use.

#### Data cache

Its primary goal is to **minimize round trips to the database**. It pulls item information from Sitecore. It doesn't pull item information until requested.

It is responsable for **holding all data retrieved from the database** in order to **reduce the number of database requests**.

If the data is not in the **Data cache**, it will first look to retrieve the information from the **Prefetch cache**. If the item is available to be retrieved, it will then be stored in the** Data cache as ItemInformation**.

#### Prefetch cache

It loads all the frequently loaded data up front and hold onto it for later.

It stores items that Sitecore will need to access during and just after initialization of instance. As each piece of data not currently existing in the Prefetch cache is requested, it is stored in the Prefetch cache.

### Cycle

html => Item => Data => Prefetch =>
                                    Database
html <= Item <= Data <= Prefetch <=

### Configure Cache

Overwrite the default sitecore.config file.

#### Item and Data Cache

- create a patch file for chache size values: **ItemDataCache.config.**
- This file will overwrite the sitecore.config file.
- use rule-based configuration to target different environments (web database, master database).
- deploy your configuration file:
    *C:\inetpub\wwwroot\<website>\App_Config\Include\*
    you can check your changes by visiting */sitecore/admin/showconfig.aspx* and searching for path:source="ItemDataCache.config"


```xml
<configuration>
    <sitecore>
        <databases>
            <!-- targeted environments -->
            <database id="web">
                <cacheSizes role:require="ContentDelivery or Standalone">
                    <data>1000MB</data>
                    <items>1000MB</items>
                </cacheSizes>
            </databse>
            <!-- targeted environments -->
            <database id="master">
                <cacheSizes role:require="ContentManagement or Standalone">
                    <data>1000MB</data>
                    <items>1000MB</items>
                </cacheSizes>
            </databse>
        </databases>
    </sitecore>
</configuration>   
```

#### Prefetch Cache

- create a patch file for chache size values: **PrefetchCache.config**
- use rule-based configuration to target different environments (web databse, master database).
- deploy your configuration file:
    *C:\inetpub\wwwroot\<website>\App_Config\Include\*
    you can check your changes by visiting */sitecore/admin/showconfig.aspx* and searching for path:source="PrefetchCache.config"
- set the configuration elements necessary to optimze the initial population of the prefetch caches.

```xml
<configuration>
    <sitecore>
        <databases>
            <database id="web" role:require="ContentDelivery or Standalone">
                <dataProviders> 
                    <dataProvider param1="$(id)">
                        <prefetch hint="raw:AddPrefetch">
                            <!-- include the most frequently accessed items  -->
                            <template desc="sample">{<template GUID>}</template>
                            <item desc="root">{<item GUID>}</item>
                            <children desc="main sections">{<item GUID>}</item> 
                             <!-- limit the amount of children items -->
                             <childLimit >
                               100
                            </childLimit>
                        </prefetch>
                    </dataProvider> 
                </dataProviders>    
            </databse>
           <database id="master" role:require="ContentManagement or Standalone">
                <dataProviders> 
                    <dataProvider param1="$(id)">
                         <prefetch hint="raw:AddPrefetch">
                           <path:delete />
                        </prefetch>
                        <prefetch hint="raw:AddPrefetch">
                             <cacheSizes >
                               1000MB
                            </cacheSizes>
                            <childLimit>100</childLimit>
                            <logStats>false</logStats>
                        </prefetch>
                    </dataProvider> 
                </dataProviders>    
            </databse>
        </databases>
    </sitecore>
</configuration>
```

#### HTML Cache

- create a patch file for the <sites> element in the sites node of: **App_Config\Sitecore.config\App_Config\Sitecore\CMS.Core|Sitecore.Sites.config**
- set the **htmlCacheSize** attribute for each of your sites of the site node.
- add options locally or globally.
    - Locally: open the item in the Content Editor, click Details on the Presentation tab, then click the rendering you want to set options for.
    - Globally: open the rendering definition item (sitecore/Layout/Renderings) and navigate to the options in the Caching section.
- use rule-based configuration to target different environments (web databse, master database).
- deploy your configuration file:
    **C:\inetpub\wwwroot\<website>\**
    you can check your changes by visiting /sitecore/admin/showconfig.aspx and searching for path:source="custom.caching.config

```xml
<configuration>
    <sitecore>
       <sites>
            <site name="website" set:htmlCacheSize="300MB"></site>
             <site name="customsite" set:htmlCacheSize="300MB"></site>
       </sites>
    </sitecore>
</configuration>
```

#### Disable Cache Limit

`not recommended in production`

- allows sitecore to take advantage of any available memory within your solution.
- create a patch file for chache size values: **DiasableCacheLimits.config**
- deploy your configuration file:
    "C:\inetpub\wwwroot\<website>\App_Config\Include\" 

```xml
<configuration>
    <sitecore>
       <settings>
            <setting name="Caching.DisableCacheSizeLmits" set:value="true"></setting>
       </settings>
    </sitecore>
</configuration>
```

#### Clear cache

- By default the cache is clear in each publish.
- To avoid the default behavoiur create a patch file for chache size values: **PreventHtmlCacheClear.config**
- deploy your configuration file:
    "C:\inetpub\wwwroot\<website>\App_Config\Include\" 

```xml
<configuration>
    <sitecore>
       <sites>
            <site name="website" cacheHtml="true" preventHtmlCacheClear="true"></site>
             <site name="customsite" set:htmlCacheSize="300MB"></site>
       </sites>
    </sitecore>
</configuration>
```

### Cache Tuning

It is the process of **monitoring and adjust** your caches based on the needs of your site.

- Choose a load testing tool.
- Start a load test that hits all items in all languages.
- Browse to the */sitecore/admin.cache.aspx* page and check values
    - Content Delivery
        - ```web[data](Data chache)```
        - ```web[item](Item chache)```
        - ```SqlDataProvider-Prefetch data(web)(Prefetch chache)```
     - Content Management
        - ```master[data](Data chache)```
        - ```master[item](Item chache)```
        - ```SqlDataProvider-Prefetch data(master)(Prefetch chache)```
- click refresh on the */sitecore/admin/cache.aspx*
    - check the amount of memory
- repeat the steps until the caches are stable
    - the cache is consider stable when the cache size is between 70% and 80%.


Be sure that your Sitecore Solution has the sufficient RAM to cache the entire database.