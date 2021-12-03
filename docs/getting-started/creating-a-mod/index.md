# Creating a mod

## Requirements
- JDK 17 or later (you can download from [here](https://adoptium.net/))
- IDE (highly recommended, but not required)

## Quick start
You can clone the [ExampleMod](https://github.com/BlueberryMC/ExampleMod) for the quick start of creating a mod.
Then, run this command to generate some required files.
```
gradlew patchVanillaJar
```

At this point, you can edit the source code to make your own mod.
For `mod.yml` properties, see [mod.yml format](../../reference/mod-yml-format/)

!!! info "Choose mod id wisely!"
    Other mods can depend on your mod id, so if your mod id was changed later, the depending mods will break.

To test your mod, simply run:
```
gradlew runClient
```
