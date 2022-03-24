## Command Line Interface

It enable Developers to communicate with a Sitecore instance from the command line.

```sh
dotnet sitecore -h
```

- log in to a **remote Sitecore instance** pushing content and serialize items.
    - Login is **OAuth-based**, which allows for two flows: 
        - interactive/device-code based.
        - non-interactive client credentials.
- publish content.
- serialize items.
    - track and synchronize database changes by combining the best of two serialization tools, Uniconr and TDS.

### Install

Locally

```sh
dotnet new tool-manifest
dotnet tool install Sitecore.Cli --version 2.0.0 --add-source http://sitecore.myget.org/F/sr-package/api/v3/index.json
```

Globally

```sh
dotnet new tool-manifest
dotnet tool install Sitecore.Cli -g --version 2.0.0 --add-source http://sitecore.myget.org/F/sr-package/api/v3/index.json
```

Once it is installed, a **dotnet-tools.json** file is created in the project folder. Now sitecore command can be used.

Init

```sh
dotnet sitecore init
```

### Login Sitecore Instance with Sitecore CLI

Sitecore CLI allows two flows of **authentication** and **authorization**:

1. An **interactive user login**, using a device code flow.
2. A **non-interactive client login**, using a client crendentials flow. This is used by clients such as Continuous Integration servers.

1. User

To log as a User you need:

- The URL of the identity authority (The Sitecore Identity Server or other identity service)
- The URL of the Sitecore instance
- Your name
- Your password

```sh
dotnet sitecore login --authority https://<identity.authority or identity.server> --cm http://<sitecore.bakend.instance> --allow-write true
```

```sh
dotnet sitecore login --authority https://id.myproject.localhost --cm http://cm.myproject.localhost --allow-write true
```

It opens a **login web page in your browser**. Enter username and password and click OK.

The sitecore login stores your **login arguments** in the **sitecore\user.json** file together with an **access token**.

`do not commit the user.json file to source control as it contains priviliged information`

2. Client

To log as a Client you need:

- The URL of the identity authority (The Sitecore Identity Server or other identity service).
- The URL of the Sitecore instance.
- The client ID.
- The client secret.

```sh
dotnet sitecore login --authority https://<identity.authority or identity.server> --cm http://<sitecore.bakend.instance> --allow-write true --client-credentials true --client-id <client id> --client-secret <client secret>
```

### Command reference for Sitecore CLI

| command | Description |
| --- | --- |
| sitecore login | log into Sitecore |
| sitecore login -h | log commands info |
| sitecore init | initializes a **project configuration** in the current folder |
| sitecore publish | publishes all content for the **MasterDB** to the **WebDB** |
| sitecore ser diff | compares the content items of two Sitecore instances |
| sitecore ser explain | Explains whether a content item path is included and why |
| sitecore ser info | Shows serialization configuration |
| sitecore ser package | Lists serialization package commands |
| sitecore ser package create | Creates a package of serialized content items |
| sitecore ser package install | Installs a package of serialized content items in Sitecore instance |
| sitecore ser pull | Serializes content items from a Sitecore instance to your file system |
| sitecore ser push | Pushes serialized content items from your file system to a Sitecore instance |
| sitecore ser validate | Checks serialized content items for validity. Can fix common issues with --fix |
| sitecore ser watch | Monitors changes to content items in a Sitecore instance and automatically serializes the changes to your file system |

```diff
+ the -h flag return info about the commands
```

### Validate serialized content items

Each time you run the serialization commands, SCS system automatically validates the content items in the **file system** against the content items in a **Sitecore instance**.

To make a manual validation:

```sh
dotnet sitecore ser validate
```

If you get an error, run:

```sh
dotnet sitecore ser validate --fix
```