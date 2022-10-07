## Sitecore Content Serialization Packages

**Sitecore Content Serialization Packages** support a **continuos integration (CI)pipeline**.

Packages contain everything a developer needs to **deploy to production**. They contain specify modules and all their serialized items.

They are **build artifacts** used in the CI pipeline.

You will generally create **one package per Solution** for **Production**.

1. Create a Package

    **Sitecore Module Explorer**

    - Add a build project to the solution

        - right-click in **solution**.
        - add **New Project**.
        - select **Sitecore for Visual Studio Project**.
        - click next.
        - Add:
            - Name: MyProject.build
            - Location: Dev/MyProject/src
        - click **Create**.
        - Save.
        - Close Visual and Open it again.


    - Edit the build project to build a **serialized item package**.

        - right-click MyProject.build.
        - click Properties.
        - In the **Serialized Items Package** tab, select the **Build Serialized Items Package** checkbox.
        - In the **Package Modules** section, select **Include All modules**.
        - Save.
        - Build and create the package.

    **Sitecore CLI**

    - go to the project folder where *sitecore.json* file is located.
        
    ```sh 
        dotnet sitecore ser pkg create -o MyProject.build
    ```

2. Configure for **client credentials authentication.**

    The **Sitecore Command Line** allows to console communication with **Sitecore instance**.

    For **non-interactive client logins** using **client credential flows for the Sitecore instance**, you must add aditional configuration to the **Identity Server** and **Content Management instance**.

    - Create a new configuration patch for the **Sitecore Indentity Server** in \docker\build\id.

        - name the file **Sitecore.IdentityServer.MyProject.xml**
        - paste the code from Sitecore

    ```xml
        <?xml version="1.0" encoding="utf-8"?>
        <Settings>
            <Sitecore>
                <IdentityServer>
                    <Clients>
                        <!-- used to authenticate servers with client id and client secret -->
                        <!-- You can name it as you like -->
                        <CliServerClient>
                            <ClientId>SitecoreCLIServer</ClientId>
                            <ClientName>SitecoreCLIServer</ClientName>
                            <AccessTokenType>0</AccessTokenType>
                            <AccessTokenLifetimeInSeconds>3600</AccessTokenLifetimeInSeconds>
                            <IdentityTokenLifetimeInSeconds>3600</IdentityTokenLifetimeInSeconds>
                            <RequireClientSecret>true</RequireClientSecret>
                            <AllowOfflineAccess>false</AllowOfflineAccess>
                            <AllowedGrantTypes>
                                <!--
                                    client_credentials authenticates with client ID and client secret
                                    which is good for CI, tools, etc. However, it's not tied to a USER,
                                    it's tied to a client ID.
                                -->
                                <AllowedGrantType1>client_credentials</AllowedGrantType1>
                            </AllowedGrantTypes>
                            <ClientSecrets>
                                <!--<ClientSecret1>SUPERLONGSECRETHERE</ClientSecret1>-->
                            </ClientSecrets>
                            <AllowedScopes>
                                <!-- this is required even if not a 'user' for Sitecore to like us -->
                                <AllowedScope1>sitecore.profile.api</AllowedScope1>
                            </AllowedScopes>
                        </CliServerClient>
                    </Clients>
                </IdentityServer>
            </Sitecore>
        </Settings>

    ```

    This patch defined a **new login client** for **automated login** using **client credentials**.

3. Add directives to the Identity Server DockerFile.

    In *\docker\build\id\Dockerfile* paste

    ```Dockerfile
    WORKDIR c:\indentity
    COPY Sitecore.IdentityServer.MyProject.xml .\Config
    ```

4. Add **environment variable** to id services.

    Add environment variable to **id services** in the **docker-compose.override.yml** file which configure the **client secret**.

    It uses **ASP.NET Core's** ability to configure via environment variables to set the client secret value to an environment variable on the host, **MY_PROJECT_DEPLOYMENT SECRET**.

    - Add as a new environment variable to the id service in docker-compose.override.yml.

    ```yml
    Settings_Sitecore__IdentityServer__Clients__CliServerClientt__ClientSecrets__ClientSecret1: ${MY_PROJECT_DEPLOYMENT_SECRET}
    ```

    ```yml
    {
        id:
            environment:
                SITECORE_LICENSE_LOCATION: c:\license\license.xml
                Sitecore_Sitecore_IndentityServer_Clients_CliServerClient_ClientSecrets_ClientSecret1: ${ MY_PROJECT_DEPLOYMENT_SECRET}
    }
    ```

    - Add a value to **MY_PROJECT_DEPLOYMENT_SECRET** variable in the Docker Compose .env

    ```
    # Client Credentials Auth
    MY_PROJECT_DEPLOYMENT_SECRET=whatever
    ```

5. Add a new **configuration path file** to Platform web project.

    This Configuration patch adds a claim mapping to th **CM role**, which indicates that users who have logged in via the MyProjectDeployment client ID should be granted **Admin** rights.

    - go to Solution/Platform/App_Config/Include/ folder of the platform web project.
    - create a new config path file: **MyProjectDeployment.ClaimMapping.config**
    - Paste code from Sitecore.

    ```xml
        <?xml version="1.0" encoding="utf-8"?>
        <configuration xmlns:patch="http://www.sitecore.net/xmlconfig/" xmlns:role="http://www.sitecore.net/xmlconfig/role/" xmlns:set="http://www.sitecore.net/xmlconfig/set/">
            <sitecore role:require="Standalone or ContentDelivery or ContentManagement">
                <federatedAuthentication>
                    <identityProviders>
                        <identityProvider id="SitecoreIdentityServer" type="Sitecore.Owin.Authentication.IdentityServer.IdentityServerProvider, Sitecore.Owin.Authentication.IdentityServer" resolve="true">
                            <transformations hint="list:AddTransformation">
                                <transformation name="admin-ify client credentials users" type="Sitecore.Owin.Authentication.Services.DefaultTransformation, Sitecore.Owin.Authentication">
                                    <sources hint="raw:AddSource">
                                        <!-- add the client id -->
                                        <claim name="client_id" value="SitecoreCLIServer" />
                                    </sources>
                                    <targets hint="raw:AddTarget">
                                        <claim name="name" value="sitecore\superuser" />
                                        <claim name="http://www.sitecore.net/identity/claims/isAdmin" value="true" />
                                    </targets>
                                    <keepSource>true</keepSource>
                                </transformation>
                            </transformations>
                        </identityProvider>
                    </identityProviders>
                </federatedAuthentication>
            </sitecore>
        </configuration>
    ```

6. Launch the environment.

    In the powershell run one of these scripts:

    - .\up.ps1
    - docker-compose build
    - docker-compose up -d

6. Install the **Sitecore Content Serialization package** in the delivery pipeline.

    ```sh
    dotnet sitecore ser package install -f src\MyProject.buil\bin\Debug\MyProject.build.itempackage
    ```