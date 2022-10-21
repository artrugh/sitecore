### Cookies

A cookie is a small file that your organization places on a user’s device (such as a PC, tablet, or mobile phone) to perform identity and data capture.

The Boxever JavaScript Library places the following cookies on the site visitor's device:

- **bid_{clientKey} cookie**
    It persists the browser ID between sessions. It generates a Universally Unique Identifier (UUID) that is unique per browser until the cookie expires or is deleted, then a new UUID is generated. Sitecore CDP data capture cookies expire after two years of inactivity.

- **bx_bucket_number cookie**
    To facilitate experimentation in Sitecore Personalize, Sitecore CDP assigns a bucket number to every user of your website. The web browser stores the bucket number as a **bucket number cookie.**

    This cookie allocates the Guest to a specific variant when using audience allocation. It performs allocation for each **Web Experiment** that is live on your site during the particular session.

    It is possible that the bucket number in Sitecore CDP changes, but the bucket number cookie in the web browser remains unchanged.

    If you integrate with Sitecore CDP using the Boxever JavaScript Library, you can fix this by using the **Boxever.getBucketNumber()** function. This function updates the bucket number cookie in the web browser to match the latest bucket number in Sitecore CDP. We recommend that you call this function after an IDENTITY event.

- **boxever_test cookie**
    It checks that the other cookies are working as expected, then is immediately removed from the visitor's device.

- **Third parties cookies**
    There are scenarios when a Sitecore CDP session cookie is similar to a third-party cookie, for example, when you enable cross-domain support. This is true when the cookie is set by a website that is distinct from the website that appears in the web address bar.

    If this applies, a value is set against api.boxever.com and then the value is used in local storage to set first-party cookies across all domains.

    The Boxever JavaScript Library versions 1.4.6 includes the optional _boxever_settings.itp_cross_domain setting which automatically applies the cross-domain setting only in respect to Intelligent Tracking Prevention (ITP) browsers, most commonly Safari. This ensures first-party cookies are used otherwise.

### Local Storage

- **bid_{clientkey}** - the UUID (browser ID) stored against your organization's client key.

- **bx_bucket_number** - the bucket number between 1 and 120 inclusive that is stored in the session. This only pertains to Sitecore CDP tenants that have web experiments enabled and where you want to set the traffic allocation for the variant.

### TTL

The Boxever JavaScript Library versions 1.4.2+ provide a property, *_boxever_settings.cookie_expiry_in_days*, that enables you to change the cookie and local storage expiry from the **default of two years.**