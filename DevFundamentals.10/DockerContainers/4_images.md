## Create your own Images

Configure your **development environment** for deploying files into running containers.

To build your solution image, you must customize Sitecore Images based on your **Solution Image**.

The same **build output** needs to be layered on top of multiple base Sitecore runtime images.

You can use 

- Navigate to *C:\Sitecore\docker-example\custom-images*
    - inside there are example solutions for creating custom Sitecore images.
    - Docker Compose files for running Sitecore instances in various topologies.
    - init.ps1 file.
    - .env
    - docker-compose.override.yml
    - docker-compose.yml  
    - Dockerfile
- run `.\init.ps1 -LicenseXmlPath C:\License\license.xml

### DockerFile

- Portability, you don't need to have any install other than **Docker**.
- Control over the build environment.
- Efficiency, Docker's build cache optimizes rebuilds.
- Play nice in Docker ecosystem.

A **typical single Visual Studio Solution** creates build artifacts for multiple roles (Website and XConnect assemblies).

Using containers, **Dockerfile** is focused solely on building your solution and storing the output as **structured build artifacts** on the resulting image.

The **solution build Dockerfile** produces an image that consists only of build artifacts.

The resulting solution image is never intended to be run in a Docker container.

Such images are sometimes called asset images.

The **Dockerfile** needs to be sent through the Docker build command.

### docker-compose-override.yml

- Navigate to *C:\Sitecore\docker-example\custom-images*

The **docker-compose-override.yml** file is where the **solution image build is define**. It extends the main docker-compose.yml file with the overrides and extensions neccesary for suctom Sitecore image build.

All the Compose files merge together into a single merge definition.

### Build Solution Image

run **docker-compose build solution**

### Docker Build Folder

The **docker/build** folder contains files and folders to support Docker development and contains each of the **Sitecore service topologies**. Each of the services represents a container.

At a minimum, the **service folders** contain a Sitecore runtime **Dockerfile** which is used as the Docker build context for the corresponding service in the **Docker Compose** file.

This is recommended so that there is a **dedicated layer** to make hotfixes or future customizations.

### Execute configuration transforms

#### Transforms apply to all core Sitecore roles

Sitecore implementation requires **modifications** of config files that can not be changes through **Sitecore config patching**.

Multiple transformation for the same config file can be made using XDT transform file.

Configuration transforms that apply to all core Sitecore roles will be stored directly in the solution structure. It supports multiple transforms for the same config file, which is common in **Sitecore Helix Solution**

- Solution Transform: \src\DockerExamples.Website\Web.config.xdt

In **Dockerfile** the transform files (.xdt extension) are collected within the builder stage and dropped at *C:/out/tranforms*

```yml
RUN Invoke-Expression 'robocopy C:\build\src C:\out\transforms /s /ndl /njh /njs *.xdt' 
```
They are copied in from the builder stage to the final image with the following structure: *\artifacts\transforms*

```yml
COPY --from=builder C:\out\transforms .\transforms\
```

#### Transforms apply to an specific Sitecore role

They are stored inside that role's dedicated docker/buil folder

Open *C:\Sitecore\docker-example\custom-images\docker\build\cm\Dockerfile*

The tranforms folder content are being copied in from the Docker build context, landing \transforms\role\

```yml
COPY .\transforms\ \transforms\role\
```

The transforms are applied after solution transforms

```yml
RUN C:\tools\scripts\Invoke-XdtTransform.ps1 -Path .\ -XdtPath C:\transforms\role' 
```

- Role Transform: *\docker\build\cm\transforms\Web.config.xdt*
