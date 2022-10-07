### Deploy, Develop & Debug

#### Deploy

- **ENTRYPOINT**: It is a command to execute when a container is first run. All sitecore runtime images have a default one, configured in the Dockerfile instructions.

**WATCH:** In Docker for Windows, you have to watch for changes in a separate mounted "hot" folder and then copy those changes into the Sitecore webroot.

Override the entrypoint and use the **sitecore-docker-tools-assets image** to start the **watch process** as background job.

| Script type | path | Use |
| --- | --- | --- |
| Watch script| *C:\tools\scripts\Watch-Directory.ps1* | Watches source path for file changes and updates the destination path accordingly. |
| ENTRYPOINT script| *C:\tools\entrypoints\iis\Development.ps1* | A development ENTRYPOINT script to use for IIS-based roles(CM, CD, xConnect. |
| ENTRYPOINT script| *C:\tools\entrypoints\worker\Development.ps1* | A development ENTRYPOINT script to use for .NET Core-based worker roles (xdbsearchworker, cortexprocessingworker). |

##### Deploy files into a running container

Entrypoints allows to execute script when a container is already created and running.

This allows you to **publish changes made in your solution to your containers** without have to stop and recreate them.

But, instead of sending files directly to the webroot, you send them to docker/deploy. 

Inside *docker/deploy* there are:
- website: CM/CD.
- xconnect:

In the solution in VS:
- NameOfTheProject.Website
    - DockerDeploy.pubxml
- NameOfTheProject.XConnect
    - DockerDeploy.pubxml

It is critical that the ENTRYPOINT script and the watch script are copied to the image, which makes them available at runtime.

1. Copy the scripts in the image, DockerFile in *docker/build/cm*.

```Dockerfile
FROM ${TOOLING_IMAGE} as tooling
# copy the folder
COPY --from=tooling \tools \tools\
```

2. Use them in the docker-compose *docker-compose.override.yml** file.

```yml
cm:
    build:
        args:
            # it is configured to use the sitecore-docker-tools-assets image
            TOOLING_IMAGE: ...
...
    entrypoint: powershell -Command "& C:tools\entrypoints\iis\Develoment.ps1"
```

*LOCAL_DEPLOY_PATH* variable is set to the relative path of the *docker\deploy* website environment subfolder *.\docker\deploy\website* to the running container at the default watch script source folder *C:\deploy* with a Docker volume.

#### Debug

- Containers window in VS.

1. In the list, right-click in the one you want to debug.
2. click **Attach to Process**, the dialog will appear and shows the available processes that are running in the container.
3. Select the process.
4. Click **Attach**.
5. In VS set the breakpoint.
6. Refresh the site to trigger a request to hit the breakpoint you've set in your code.

- Debug menu

1. Top Debug menu, select **Attach to Process**.
2. For Connection type, select **Docker (Windows Containers).
3. For Connection target, click the **Find** button. Running containers will appear in the list.
4. Select the container you would like to debug.
5. Click **OK**.
6. For Attach to, ensure **Managed Code (v4.6, v4.5, v4.0)** is selected. Should be by default.
7. Select the w3wp.exe process.
8. Click **Atach**.
9. In VS set the breakpoint.
10. Refresh the site to trigger a request to hit the breakpoint you've set in your code.

