## Requirements

- Software:

    1. Windows 10 Professional or Enterprise version.
    2. Hyper-V
    3. Docker Desktop for Windows.
    4. Docker Compose.
        - **Sitecore for Docker Compose** deployments require two text files to deploy the containers:
            - **docker-compose.yaml**
            - **.env**
    5. Visual Studio and/or Visual Studio Code.

- Hardware:

    1. Running **Hyper-V**:
        - 64-bit processor with second-level address translation (SLAT) and hardware-assisted virtualization.
        - Virtualization support turned on in the BIOS.

    2. Sitecore Development:
        - It depends on the number of instances and topologies you want to run (that is, the number of simultaneously running containers).
            - 32GB RAM XP-1
            - minim 16GB XP-0 XM-1
        - CPU Quad Core or higher.
        - 40GB free disk space (SSD disks stringly recommended).

    3. Networking:
        - verify that the TCP ports that are used by containers do not have any other process accesing them. If the ports are not available, the containers will fail to run (433, 8079, 8080, 8984, 14330).

- Configuration files:

    - Sitecore license file.
    - Environment variable **.env** file.

    The license gives access to the **Sitecore environment** for development.
    The environment variable file is the mechanism used by Sitecore to pass its configuration settings into containers.


