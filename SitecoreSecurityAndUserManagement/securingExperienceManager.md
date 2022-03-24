## Securing Experience Manager

### Allow or deny user access to web resources

You can set up access privileges for web resources with the *location* tag in the *Web.config* file.

**allow** and **denied** tags.

```xml
<location path="sitecore">
    <sistem.web>
        <authorization>
            <deny users="*"/>
            <allow users="admin, webmaster"/>
        </authorization>
    </sistem.web>
</location>
```

### Enable and disable an administrative tool

For security reason, the admin tools:

- Always disable as part of deployment process.
- Always diable when you are not using them.
- Never enable on the CD, xDB Reporting, and xDB Processing roles.
- Only enable on Content Management roles that are not exposed to the internet.

They are in the ASPX files with .aspx extension. *webroot/sitecore/admin* folder and subfolders.

To enable, go to the administrative tools folder and create an empty file named *enabled*. The *SqlShell.aspx* tool checks for the presence of this file.

To enable the *unlock_admin.aspx* tool:

1. Go to the administrative tools folder.
2. Open the *unlock_admin.aspx* file.
3. Locate the *enableUnlockButton* property.
4. Change the value from false to true. `private bool enableUnlockButton = true`
5. Save the *unlock_admin.aspx* file.

### Disable client RSS feeds

1. Open web.config file.
2. Locate the <httpHandlers> section or <Handlers>
3. Remove the handler:
```xml
<add verb="*" path="sitecore_feed.ashx" type="Sitecore.Shell.Feeds.FeedRequestHandler, Sitecore.Kernel"/>
```

### Disable SQL Server access from XSLT

Sitecore includer an xslExtension helper for use with SQL Server.

It is recommended to disable the xslExtension helper if:

- it is not needed.
- Sitecore XSLT renderings are not used.

[More Securing Experience Manager](https://doc.sitecore.com/xp/en/developers/93/platform-administration-and-architecture/securing-experience-manager.html)