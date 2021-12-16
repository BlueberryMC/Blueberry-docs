# Registering an item

## Simple item

Registering a very simple item that does not have any item specific code:

```java title="ExampleMod.java"
public class ExampleMod extends BlueberryMod {
  @Override
  public void onPreInit() {
    registerItems();
  }

  private void registerItems() {
    BlueberryRegistries.ITEM.register(
      "example_mod", // namespace
      "my_item", // item id
      new SimpleBlueberryItem(
        this, // mod
        new Item.Properties()
          .stacksTo(1) // max stack count
          .tab(CreativeModeTab.TAB_MISC) // Custom creative mode tab is not supported yet, so don't try.
          .rarity(Rarity.EPIC), // light purple color
        item -> new BlueberryText("example_mod", "item.my_item") // Use TextComponent if you don't use language files like: new TextComponent("Item name goes here")
      )
    );
  }
}
```

Minecraft will try to find the item texture from `/assets/(namespace)/textures/item/(item id).png` and `/assets/(namespace)/models/item/(item id).json`.
For example, if the item was registered with namespace of `example_mod` and item id of `my_item`, Minecraft would try to find texture from `/assets/example_mod/textures/item/my_item.png` and `/assets/example_mod/models/item/my_item.json`.

Minimal model json would be this:
```json
{
  "parent": "minecraft:item/generated",
  "textures": {
    "layer0": "(namespace):item/(item id)"
  }
}
```

Also see [ExampleItem.java](https://github.com/BlueberryMC/ExampleMod/blob/933797dd32aae4c225200bfbe4b7ea075e95a9bb/src/main/java/com/example/exampleMod/items/ExampleItem.java) for more complex item implementation.
