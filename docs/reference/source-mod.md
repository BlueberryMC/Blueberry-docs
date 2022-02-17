# Source mod

!!! warning
    This feature is experimental, use at your own risk.

    Known issues:

    - Recompiling the mod breaks registered values (such as items, blocks, etc) because Blueberry cannot unregister the values which were previously registered.

Source mod feature allows you to load mod without building .jar file manually.
This feature can be enabled by adding some properties on your `mod.yml`.

## Requirements
- `tools.jar` (included in JDK)
    - If blueberry fails to detect `tools.jar` automatically, you can specify via JVM argument:
      `-Dnet.blueberry.common.bml.tools.path=</absolute/path/to/tools.jar>`
    - Source mod feature will not compile the code if `tools.jar` is unavailable.

## Usage
1. Add these lines:
  ```yaml title="mod.yml"
  source: true # tells mod loader to enable source mod feature for this mod
  sourceDir: <source root that contains .java files>
  include: <additional resource directory than source mod directory>
  ```
2. Put your project directory to `mods` folder
