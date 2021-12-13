# Creating a mod

## Requirements
- Basic Java knowledge (strongly recommended)
- JDK 17 or later (you can download from [here](https://adoptium.net/))
- IDE (if you do not have one, IntelliJ IDEA is recommended)

## Quick start

!!! note
    If you'd like to use mixin, use [ExampleMixinMod](https://github.com/BlueberryMC/ExampleMixinMod) when cloning repository.
    Also see [this page](../../reference/mixin) when creating a mod with mixin.

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
