## Create and patch error pages

There are **two primary error pages** that a user may come across: 404 and 500.

`404` The user has reached a request domain, but the URL path provided no information.

`500` It indicates an internal server error.

### 404 Page

Create a custom 404 Page

1. create a custom 404 page within the content tree **home**, page item called **notfound**.

2. develop a custom pipeline processor within the HTTP begin pipeline.

Inject a handler into HTTP request pipeline

```csharp
using SItecore.IO;
// inject the Pipeline
using Sitecore.Pipeline.HttpRequest;

namespace Redirects
{
    public class NotFoundHandler
    {
        public void Process(HttpRequestArgs args)
        {
            // if not site has been resolved jump out
            if(Sitecore.Context.Site == null) return;
            // item was found jump out
            if(Sitecore.Context.Item != null) return;

            // grab the site-local path to the item that will be shown when the requested item cannot be found
            var notFoundPath = Sitecore.Context.Site.Properties["notFoundItem"];

            // create an opt-in strategy to only continue if the notFounItem attribute is present and populated ont the context site
            if(string.IsNullOrEmpty(notFoundPath)) return;

            // construct both, the start path and full path to the item in the database and find the item in the context database
            var sitePath = Sitecore.Context.Site.StartPath;
            var path = FileUtil.MakePath(sitePath, notFoundPath);
            var notFoundItem = Sitecore.Context.Database.GetItem(path);

            // ensure that the notFound item is found
            if(notFoundItem != null)
            {
                // set the context item as the not found item and let the request be handled normally
                Sitecore.Context.Item = notFoundItem;
                // set the HTTP status code to 404
                args.HttpContext.Response.StatusCode = 404;
            }
        }
    }
}
```

3. Add in the Sitecore.config the **notFoundItem** into the site definition as an attribute.

```xml
<configuration>
    <sitecore>
       <sites>
            <site name="website" set:htmlCacheSize="300MB" .... notFoundItem="/notfound"/>
       </sites>
    </sitecore>
</configuration>
```

4. create a **configuration patch** to tie the **customer processor HTTP pipeline**
into your build. This applies the code after ItemResolver `patch:after`

"C:\inetpub\wwwroot\<website>\App_Config\Include\" 

```xml
<configuration>
    <sitecore>
        <pipelines>
            <httpRequestBegin>
                <processor type="Redirects.NotFoundHadler, Redirects"
                    patch:after="processor[@type='Sitecore.Pipeline.HttpRequest.ItemResolver, Sitecore.Kernel']">
                </processor>
            </httpRequestBegin>
        </pipelines>
    </sitecore>
</configuration>
```

5. Deploy to your sitecore site.

```diff
+ Check this process in the documentation before implement it. There are more steps which should be done.
```

### 500 Pages

Create a **static 500 Page** to protect the site from getting stuck in a loop, if a major server issue occurs.

1. create a static error ASPX page file in the root of your site (error.aspx).
2. within your **web.config.file**, turn custom errors ON to ensure that you see the custom error page. 
    - Development: <customErrors mode="On">
    - Production: <customErrors mode="RemoteOnly">
3. Change the error status code to 500 and specify the redirect to your static error HTML file. 
```xml
<customErrors mode="On">
    <error statusCode="500" redirect="˜/error.aspx">
</customErrors>
```
4. Save and deploy to your site.

### Sitecore version 10

1. create a custom 404 and 500 page within the content tree **home**, page item called **notfound** and **error**.

2. Navagate to `/Content/your-site/Settings/SiteGrouping/your-site`.

3. Scroll to the Service page URLs section and set the value in each feild (ex: /not-found).

`Only works in integrated mode.`