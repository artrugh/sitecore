## Predeployment

### Security hardening

**Security hardening** is the practice of **configuring a computer system** or **website** to protect **sensitive data** and **reduce vulnerabilities**.

General Security hardening:

1. Keep your **Operation System** updated.
    - ensure to have the most-up-to-date security features.

2. Have a strong **password policy**.
    - before deployment:
        - reset the admin password.
        - create a new **admin account** and grant it **administrator priviliges**.

3. Separate **Content Management** and **Content Delivery** servers.
    - separatly deploy the internal-facing **Content Management** server and the external-facing **Content Delivery** server in a production environment.
    - never expose your **Content Management** environment to the Internet. Doing so **increase the data's vulnerability**. If for some reason you should expose it:
        - Use **HTTPS** to secure the **Content Management** server.
        - Considering using **IP Filtering** so that only **white-listed clients** can connect to the **Content Management** environment.
        - Considering using the **Dynamic IP Address Restrictions** feature available in [**Internet Information Services**](https://en.wikipedia.org/wiki/Internet_Information_Services) IIS.

4. Protect the section in **web.config** file.
    - Sitecore stores **sensible information** in the <connectionStrings> section of the web.config
    - you can use **Microsoft ASP.NET IIS Registration Tool** (aspnet_regiss.exe) to **encrypt this section** with the -pe or -pef options, in case an unauthorized user gains access to the web.config file.
    - **Microsoft ASP.NET IIS Registration Tool** uses the machine key to perform the encryption, so you will need to perform the encryption process for each computer you have Sitecore installed on. This applies to **on-premise** deployment only.

5. Secure MongoDB.
    - Sitecore uses the SQL xDB Collection provider by default, but you can choose to use the MongoDB xDB Collection provider with Sitecore. MongoDB offers a range of features you can use to ensure the security of your deployment, including authentication and access control.

6. Ensure xConnect Security.
    - the service layer, xConnect, sits between the **xDB** and any **trusted client, device, or interface** that wants to read, write, or search xDB data. Communication must happen over HTTPS adn clients need to have **appropiate carticate thumbprint**.

7. Check Security Settings Related to Users.
    - Sitecore controls **security access** at three levels: 
        - users (individuals)
        - roles(a collection of users)
        - and domain(a collection of security accounts)
    - Sitecore strongly recommends you assign **security access** right to **roles** rather than individual users. This minimizes the risk of accidentally giving someone access to features of Sitecore, they should not have.
    - Use the **Role Manager** in the **Sitecore Experience Platform Launchpad** to create user roles.

8. Develop a Disaster Recovery Plan.
    - develop a **disaster recovery plan** to get the website back up as quickly as possible.
        - a plan to obtain temporary or new equipment.
        - a plan to restoring content backups.
        - a way to test the overall plan and ensure the organization is familiar with what to do in the event of a catastrophic loss or failure.

### Performance Configuration Checklist

1. Verify SQL Server Index Fragmentation
2. Clean Database Tables.
3. Verify Scalable Solr Configuration.
    - You must configure the indexes you need on each server. You will only require the indexes that correspond with the databases you are using on the server you are configuring. Example: Content Delivery Server, Web database, sitecore_web_index.
4. Verify Site Analytics.
5. Turn Off Debug Mode.
6. Verify Custom [Error Pages](2_errorPages.md).
7. Configure and [Tune Caches](4_catching.md).
8. Verify Index Rebuild Strategy.
    1. RebuildAfterFullPubish
    2. OnPublishEndAsync
    3. OnPublishEndAsyncSingleInstance
    4. IntervalAsynchronous
    5. Synchronous
    6. RemoteRebuild
    7. Manual
9. Finalize Host Name Patching.
    - Sitecore.config `<site name="website" .../>``
    - Any patch files that configure Sitecore for a specific environment, such as QA or Development, must be placed int the /App_Config/Environment folder.
    - for each website, configure the website attributes depending on the purpose of the website.
10. Deploy Sitecore Client License.


