# mod.yml format

## Properties

| Name | Type | Optional | Default Value | Notes |
| --- | --- | --- | --- | --- |
| id | string | ❌ | | Mod ID used internally and rarely displayed to the user (accepts uppercase characters for now, but not recommended) |
| name | string | ⭕ | `id` in mod.yml | Mod Name that would be displayed to the user (defaults to id) |
| version | string | ❌ | | Mod version (type is string but you can specify number) |
| main | string | ❌ | | Main class of your mod (specify the class which extends BlueberryMod) |
| author | string | ⭕ | null | If `authors` is present, `author` will be inserted at the last entry of the `authors`. |
| credit | string | ⭕ | null | If `credits` is present, `credit` will be inserted at the last entry of the `credits`. |
| authors | string list | ⭕ | null | If `author` is present, `author` will be inserted at the last entry of the `authors`. |
| credits | string list | ⭕ | null | If `credit` is present, `credit` will be inserted at the last entry of the `credits`. |
| description | string list | ⭕ | null | Must be string list, not string. 1 entry = 1 line |
| unloadable | boolean | ⭕ | false | If true, user can click the `Disable` (equivalent to unload) button in mod list screen. |
| depends | string set | ⭕ | empty set | Set of required mod ids (the mod will not load without satifying the `depends`) |
| softDepends | string set | ⭕ | empty set | Set of optional mod ids (unlike `depends`, the mod can be loaded without satifying the `softDepends`) |
| source | boolean | ⭕ | false | See [Source mod](../source-mod) |
| sourceDir | string | ⭕ | null | See [Source mod](../source-mod) |
| include | string | ⭕ | null | See [Source mod](../source-mod) |

## Very basic example

```yaml title="mod.yml"
id: example_mod
name: ExampleMod # optional but recommended
version: 1.0.0
main: com.example.ExampleMod
```
