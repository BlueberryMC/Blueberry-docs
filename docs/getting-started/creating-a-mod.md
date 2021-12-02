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

To test your mod, simply run:
```
gradlew runClient
```
