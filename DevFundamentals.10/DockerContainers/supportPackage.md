## Sitecore Container Support Package

1. Switch to **Docker Windows container mode**.
2. Download Sitecore Container Support Package and store it in your local workstation.
3. Access the Topology locating the folder for the topology and open the **Docker Compose topology folder**.
4. Update the .env configuration file.
5. Generate Transport layer security (TSL) Reverse Proxy Certificates.
6. Install Self-Signed Root Authority Certificate.
7. Open the docker-compose.yaml file for a better understanding.
8. Open the folder that the docker-compose.yaml is and run **.\docker-compose.exe up -detach**.
9. Check docker container status **.\docker.exe container list -all** or **docker-compose ps**.
10. Access the **Content Management** instance on the browser: **https://xp0cm.localhost**.
11. Log to the **Sitecore Admin**. On the browser: **https://xp0cm.localhost/sitecore/login**.
12. Populate the managed schema for indexes for the **Core**, **Master** and **Web** search indexes. In the **Contro Panel** click **Populate Solr Managed Schema**.
13. Rebuild search indexes for the **Core**, **Master** and **Web** databses. In the **Contro Panel** click **Rebuild search indexes**.
14. Clean up the workstation. In containers you can: stop or completely remove a workstation environment.
    -  stop a workstation environment whithout removing its content: **.\docker-compose.exe stop**.
    -  stop and remove a workstation environment and its content: **.\docker-compose.exe down**.
    - to remove persistant data stored in volumes (mssql-data | solr-data) run the clean.ps1 script: **.\clean.ps1**



