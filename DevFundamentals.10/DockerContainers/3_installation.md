## Intall Sitecore using containers

Clone the [Repo from Sitecore.](https://github.com/Sitecore/docker-examples).

After that:

You can run a script names: **init.ps1** that performs all preparation steps automatically.

```sh
.\init.ps1 -LicenseXmlPath C:\License\license.xml
```

or follow the next steps to do a manual installation.

### SitecoreDockerTools

It contains various **cmdlets** to support Docker-based Sitecore development.

cmdlets: a lightweight command that is used in the PowerShell environment.

```sh
 Register-PSRepository -Name "SitecoreGallery" -SourceLocation "https://sitecore.myget.org/F/sc-powershell/api/v2"
 Install-Module SitecoreDockerTools
``` 

### Populate Environment File

- SITECORE_ADMIN_PASSWORD

- SQL_SA_PASSWORD

    As another option you can use "sa" login`

- TELERIK_ENCRYPTION_KEY

    As an Administrator from the same folder as your .env file run this to populate **TELERIK_ENCRYPTION_KEY** 

    ```sh
    Import-Module SitecoreDockerTools
    Set-DockerComposeEnvFileVariable "TELERIK_ENCRYPTION_KEY" -Value (Get-SitecoreRandomString 128)
    ```

    Import the **SitecoreDockerTools module** into the session and sets the **TELERIK_ENCRYPTION_KEY** variable utilizing two of the **cmdlets**:

    - Set-DockerComposeEnvFileVariable - sets a variable value in a Docker Compose **.env** file.
    - Get-SitecoreRandomString - returns a random string to be used as a password or key.

- SITECORE_IDSECRET / SITECORE_ID_CERTIFICATE / SITECORE_ID_CERTIFICATE_PASSWORD

    Set up the Identity Server token signing certificate

    Identity Server requires a private key certificate to sign the tokens that are passed between the server and the clients.
    
    Generate the certificate, Base63 encode it in a string form and pass it to the container as an environment variable.

    Encode the certificate and create a SitecoreIdentityTokenSigning.txt containing the certificates.

    Populate the SITECORE_ID_CERTIFICATE with the certificate from the file.

    In an Administrator PowerShell from the same folder as your .env file run to populate variables.

    ```sh
    Import-Module SitecoreDockerTools
    Set-DockerComposeEnvFileVariable "SITECORE_IDSECRET" -Value (Get-SitecoreRandomString 64 -DisallowSpecial)
    $idCertPassword = Get-SitecoreRandomString 12 -DisallowSpecial
    Set-DockerComposeEnvFileVariable "SITECORE_ID_CERTIFICATE" -Value (Get-SitecoreCertificateAsBase64String -DnsName "localhost" -Password (ConvertTo-SecureString -String $idCertPassword -Force -AsPlainText))
    Set-DockerComposeEnvFileVariable "SITECORE_ID_CERTIFICATE_PASSWORD" -Value $idCertPassword
    ```

    **Get-SitecoreCertificateAsBase64String** generates a new self-signed certificate and returns the certificate in its password-protected, Base64 encoded form.

- SITECORE_LICENSE

    - Compressing

        The sitecore license file gives access to certain [topologies](topologies.md).

        Compress Base64 encode the **license** file to conform with the maximum size allowed by Windows.

        Run as an Administrator from the same folder as your .env file and populate **SITECORE_LICENSE**

        ```sh
        Import-Module SitecoreDockerTools
        Set-DockerComposeEnvFileVariable "SITECORE_LICENSE" -Value (ConvertTo-CompressBase64String -Path "C:\License\license.xml")
        ```

    - Mounting

        Populate the SITECORE_LICENSE_LOCATION environment variable on each service with a volume-mounted path containing the **Sitecore license key**. You can use a HOST_LICENSE_FOLDER variable to config the path on the container host which contains the **license.xml**

        ```yml
            volumes:
                - ${HOST_LICENSE_FOLDER}:c:\license
            environment:
                SITECORE_LICENSE_LOCATION: c:\license\license.xml
        ```

        In xConnect role

            ```yml
            volumes:
                - ${HOST_LICENSE_FOLDER}:c:\license
            environment:
                SITECORE_LICENSE_LOCATION: c:\license\
            ```

### Configure HTTPS Certficates and Windows Host File

#### Examine Traefik folder

Sitecore uses **Traefik** to serve as the **default reverse proxy** or **edge router** for **Docker Compose**

/getting-started/traefik
        
- certs
    An empty folder to place generated certificates.
- config/dynamic/certs_config.yaml
    A Traefik configuration file which is used by the Traefik container.

The **Traefik folder** is exposed to the container with a Docker volume in the **docker-compose.yml** file.

The Traefik service maps the relative ./traefik folder to running container at C:\etc\traefik.

This path is then used by the Traefik service configuration, setting the --providers.file.directory to C:\etc\traefik\config\dynamic (where the certs_config.yaml file resides).

### Generate Certificates

Transport layer security TLS/HTTPS certificates ensure secure communication between the **browser** and the **HTTPS reverse proxy container**.

- Generate the **Content Management role**
- Generate the **Identity server certificates** 

**Mkcert** is a simple tool for making locally-trusted development certificates. It requires no configuration.

1. Download the latest Windows executable (mkcert-v1.4.1-windows-amd64.exe)
2. Rename the file to mkcert.exe
3. Move the file to the .env path location.
4. In the powershell as administrator mode run:

```sh
    mkcert -install
```

5. In **C:\sitecore\docker-examples\getting-started** folder, run:

```sh
mkcert -cert-file traefik\certs\xp0cm.localhost.crt -key-file traefik/certs/xp0cm.localhost.key "xp0cm.localhost"
mkcert -cert-file traefik\certs\xp0id.localhost.crt -key-file traefik/certs/xp0id.localhost.key "xp0id.localhost"
```

### Add Windows Hosts File Entries

Once you generated the certificates, you can add "xp0cm.localhost" and "xp0id.localhost" hostnames to your **Windows hosts** file. This file enables you to access the **Sitecore environment** using the IP addesss.

In containers, the [reverse proxy](./../../glosary.md) is used to resolve the hostnames using HTTPS for multiple container.

Update the hosts file with the new hostnames.

1. Open C:Windows\System32\drivers\etc\hosts
2. Add the following entries:
    - 127.0.0.1 xp0cm.localhost
    - 127.0.0.1 xp0id.localhost
3. Save

or run

```sh
    Add.HostsEntry"xp0cm.localhost"
    Add.HostsEntry"xp0id.localhost"
```

The hostnames are set to point to the [loopback IP address of 127.0.0.1](./../../glosary.md).

The default hostnames are determined by the topology you deploy.

#### Default Topology Hostnames

| Topology | Hostnames | IP address |
| --- | ---- | --- |
| XM Server | xm1cm.localhost | 127.0.0.1 |
| XM Server | xm1cd.localhost | 127.0.0.1 |
| XM Server | xm1id.localhost | 127.0.0.1 |
| --- | ---- | --- |
| XP Workstation | xp0cm.localhost | 127.0.0.1 |
| XP Workstation | xp0cd.localhost | 127.0.0.1 |
| XP Workstation | xp0id.localhost | 127.0.0.1 |
| --- | ---- | --- |
| XP Server | xp1cm.localhost | 127.0.0.1 |
| XP Server | xp1cd.localhost | 127.0.0.1 |
| XP Server | xp1id.localhost | 127.0.0.1 |

## Start Sitecore

1. In the same folder as the **Compose** file, run docker-compose up -d

    - Download all required images from Sitecore Container Registry.
    - Create a default network to use.
    - Create a container for each configured service.
    - Start the containers with their configured ENTRYPOINTS.

2. Browse to **https://xp0cm.localhost**
3. Browse to **https://xp0cm.localhost/sitecore/login** and verify if you can login in to Sitecore.
    - use **admin** as username.
    - use the SITECORE_ADMIN_PASSWORD from the **.env** file.
4. You can additionaly access additional containers:

| container | hostname | port |
| ---- | --- | --- |
| Sitecore Content Management (cm) |  **https://xp0cm.localhost** | |
| Sirecore xConnect Server (xconnect) |   **https://localhost:8081** | |
| Sitecore Identity Server (id) |  **https://xp0id.localhost** | |
| Apache Solr (solr) |  **http://localhost:8984** | 8984 |
| Microsoft SQL Server (mssql) | **localhost, 14330** | 14330 |
| Traefik | **http://localhost:8079** | 443 - 8079 |

