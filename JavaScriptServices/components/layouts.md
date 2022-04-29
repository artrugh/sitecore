## Page composition in JSS apps using Sitecore data

JSS applications render pages creates in Sitecore sites.

Every page in Sitecore uses a layout.

Sitecore's layout engine works by defining named **placeholders** that can host multiple components.

JSS leverages the **dynamic placeholders** feature of Sitecore and extends the author-driven, component-based layout model of Sitecore to front-end applications.

To be editable, a page must define at least one root (page-level) placeholder. **Content Authors** define layout data and save the layout data to the database as **XML**.

Like the **Sitecore layouts**, the **Layout component in JSS** defines at least one **placeholder component** called **root placeholder**.

The component hierarchy is **unknown** to JSS application because it is defined **dynamically** by Sitecore layout data. The JSS application must define components matching the Sitecore renderings used in the page.

Dynamic Layout enables JSS apps to support layouts defined by Content Authors and support data-driven personalization and multivariate testing. This requires that the layout composed by the Content Authors in Sitecore has a matching structure in the JSS application.

When a JSS app accesses a page/route, it fetches **JSON-formatted data** from Sitecore endpoints with the help of custom **route handling and data fetching** functionality.

Developers can use the JSON-formatted layout data to implement front-end applications with any technology capable of consuming JSON data.

### Routes

Routes in JSS app are similar to website pages or Sitecore items in the site root. They are expected to fully support Sitecore URL mapping.

Site hostnames and rules for how to map page names to URL segments are defined in XML configs.