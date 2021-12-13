# Mixin

Mixin allows you to modify classes easily at runtime.

Basically, you can just follow the same steps as [Creating a mod](../../getting-started/creating-a-mod/),
but use [ExampleMixinMod](https://github.com/BlueberryMC/ExampleMixinMod) when cloning the repository.

ExampleMixinMod contains everything to create a mod with mixin, but there is one thing you have to remember:
**Always** disable remap like this: `@Mixin(value = ..., remap = false)` or make sure remap don't run at least!
