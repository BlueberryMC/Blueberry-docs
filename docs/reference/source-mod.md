# Source mod

!!! warning
    This feature is experimental, use at your own risk.

    ## Known issues

    - Recompiling the mod breaks registered values (such as items, blocks, etc) because Blueberry cannot unregister the values which were previously registered. \([#16](https://github.com/BlueberryMC/Blueberry/issues/16))
    - The live compiler directory is not being removed on exit \([#15](https://github.com/BlueberryMC/Blueberry/issues/15))

    ## Limitations

    - Mixins are not applied
    - javac can't find the external dependencies (in other words, there is no way to add classpath other than default ones)

Source mod feature allows you to load mod without building .jar file manually.
This feature can be enabled by adding some properties on your `mod.yml`.

## Requirements
- `tools.jar` (included in JDK)
    - If blueberry fails to detect `tools.jar` automatically, you can specify via JVM argument:
      `-Dnet.blueberry.common.bml.tools.path=</absolute/path/to/tools.jar>`
    - Source mod feature will not compile the code if `tools.jar` is unavailable.

## Usage
1. Copy mod.yml to project root and add these lines to mod.yml in project root
  ```yaml title="mod.yml"
  source: true # tells mod loader to enable source mod feature for this mod
  sourceDir: <source root that contains .java files>
  include: <additional resource directory than source mod directory>
  ```
2. Put your project directory to `mods` folder
3. There should be at least two mod.yml files present in your project, at `/mod.yml` and `/src/main/resources/mod.yml` for example.
