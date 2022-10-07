### Deployment

Packages support **continuous integration pipeline**.

#### Sitecore content serialization

SCS contains specifies modules and all their serialized items.

It use packages as **build artifacts** tin the CI pipeline, by creating them in the **build pipeline** and installing them in the **delivery pipeline**.

- Create item packages.
- Install them into the delivery pipeline.

#### Tools
[deeper-info](./../ContentSerializationSystem/2_serializationTools.md)

- Sitecore CLI.
    - you can log into the remote Sitecore instance:
        - publish content.
        - serialize items.
        - create item packages.
    - [more-info](./../ContentSerializationSystem/3_commandLineInterface.md)

- Sitecore for VS.
    - GUI wrapped around Sitecore CLI.
    - [more-info](./../ContentSerializationSystem/4_sitecoreForVisualStudio.md)
