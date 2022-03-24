## Container

Containers are **executable units of software**, where code is packaged in, along with **libraries and dependencies**.

A container can be run anywhere, whether on a **developer's workstation**, an **on-prem server**, or in the **cloud**.

It can be deployed **easily and consistently**, regardless of the target environment.

Containerization of an application provides a clean **separation of concerns**.

The **developers** focus on their **application logic** and **dependencies**, while **deployment teams** focus on **deployment and management**.

Instead of **virtualizing the hardware stack**, containers virtualize at the **operating system level**, with multiple containers running at the top the OS kernel directly.

Advantages:

- **Lightweight**: Small size on disk and very low overhead.

- **Portability**: A container runs on any machine that supports the runtime environment of the container. You can build locally and easily move to **on-premise** or **cloud environments**.

- **Isolation**: It keeps application isolated from the underlying system.

- **Loose coupling**: Containers are **highly self-sufficient and encapsulated**, so you can replace or upgrade one container without disrupting others containers.

- **Scalability**: container are lightweight and are loosely coupled, you can scale quickly by creating new containers.

- **Control over the build environment**: The solution owns which build dependencies and versions are used.

- **Efficiency**: Docker's build cache optimizes rebuilds.

- **Builds can be triggered using Docker commands**: Retrieving build artifacts for use in other images is simple with Dockerfile FROM instructions.

### Docker

Docker is an **open source project** for building applications on containers.

### Docker teminology

- **Image**: A package with all code and dependencies that serves as the blueprint for creating a container.

- **Dockerfile**: A file that contains instructions for assambling a Docker image.

- **Registry**: A place where you store Images.

- **Repository**: A collection of images with the same name, labeled with tags to indicate the version or variant.

- **Tag**: A reference to a specific image within a repository. It is often use for a version number. By default the tag is assign to **latest**.

- **Container**: An instance of an image. An execution environment, and a standard set of instructions.

- **Compose**: A **CLI tool** and **text document format** created by **Docker**. It is used to define how a multi-container application runs.

- **Orchestration**: A management tool for containers. It helps to **deploy** and **manage** containers in production (Kubernetes).

### Benefits of using Container-based Sitecore development

- No needed installation modules using SIF (Sitecore Installation Framework), SIM (Sitecore Instance Manager), or SIA (Sitecore Install Assistant).

- Multi-project efficiencies - You can run **multiple Sitecore instances** simultaneously without worrying about things like conflicting versions of SQL or Solr.

- Simplified onboarding - Install prerequisites, clone your code repository, run docker-compose up.

- Environment consistency - Eliminate issues due to environment inconsistencies, because you have complete control of the build environment.

- Environment stability - Because containers are immutable, no worries about running your local Sitecore instance.

### Sitecore images

Container images for all roles and topologies are available at src.sitecore.com, the Sitecore Registry (SCR).

### Docker Compose files

The **Docker Compose files** contain the instrucctions to build one or more containers.

- **docker-compose.yml**: It is the main configuration file used by the **docker-compose command**. It contains information about the containers (referred to as services) and their configurations.

- **.env file**: This environment file contains **values** that represent the default values for any **environment variables** referenced in the Compose file or used to configure Compose.

