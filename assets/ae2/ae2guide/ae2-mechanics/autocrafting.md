---
navigation:
  parent: ae2-mechanics/ae2-mechanics-index.md
  title: 自动合成
  icon: pattern_provider
---

# 自动合成

### 大家伙

<GameScene zoom="4" interactive={true}>
  <ImportStructure src="../assets/assemblies/autocraft_setup_greebles.snbt" />
  <IsometricCamera yaw="195" pitch="30" />
</GameScene>

自动合成是 AE2 的基本功能之一。不像需要手动合成正确数量的子原料的*原始人*，你可以叫 ME 系统帮你完成。要么自动合成物品并且导出到某处。要么通过智能的应急措施自动保持库存中一定数量的物品。
它也支持流体，在安装了对应附属模组的情况下还支持其他模组的材料类型，比如《通用机械》的化学品。挺棒的。

这是个复杂的话题。让我们准备好了就出发。

一个自动合成系统包括以下三个部件：
- 发送合成请求的东西
- 合成 CPU
- <ItemLink id="pattern_provider" />。

是这样的：

1.  某物创建了合成请求。可以是你在终端中点击了某些可以自动合成的物品，或者是一个装了合成卡的 ME 输出总线或 ME 接口请求了它们设置好要输出/存储的物品。

*   （**重要：**使用你用来“选取方块”（通常是鼠标中键）的按键来请求你库存中已有的物品，但这可能与物品栏排序模组冲突）

2.  ME 系统计算为了满足请求需要的原料和前置合成步骤，并把它们储存在选定的合成 CPU 中。

3.  有对应 [样板](../items-blocks-machines/patterns.md) 的 <ItemLink id="pattern_provider" /> 把样板指明的原料推入任何附近的容器。
    如果是合成样板，这会是 <ItemLink id="molecular_assembler" />。
    如果说处理样板，这会是其他方块或机器或复杂的红石控制的设施。

4.  合成结果以某种方式回到系统，可能是通过输入总线、ME 接口或把结果推回样板供应器。
    **注意：一个“物品进入系统”事件必须发生，不能直接把物品送回一个连接了 <ItemLink id="storage_bus" /> 的箱子。**

5.  如果这个合成是另一个合成的依赖项，这些物品将被存入合成 CPU，并在那个合成中使用。

# Patterns

<ItemImage id="crafting_pattern" scale="4" />

Patterns are made in a <ItemLink id="pattern_encoding_terminal" /> out of blank patterns.

There are several different types of pattern for different things:

*   <ItemLink id="crafting_pattern" />s encode recipes made by a crafting table. They can be put directly in a <ItemLink id="molecular_assembler" /> to make it
    craft the result whenever given the ingredients, but their main use is in a <ItemLink id="pattern_provider" /> next to a molecular assembler.
    Pattern providers have special behavior in this case, and will send the relevant pattern along with the ingredients to adjacent assemblers.
    Since assemblers auto-eject the results of crafts to adjacent inventories, an assembler on a pattern provider is all that is needed to automate crafting patterns.

***

*   <ItemLink id="smithing_table_pattern" />s are very similar to crafting patterns, but they encode smithing table recipes. They are also automated by a pattern
    provider and molecular assembler, and function in the exact same way. In fact, crafting, smithing, and stonecutting patterns can be
    used in the same setup.

***

*   <ItemLink id="stonecutting_pattern" />s are very similar to crafting patterns, but they encode stonecutter recipes. They are also automated by a pattern
    provider and molecular assembler, and function in the exact same way. In fact, crafting, smithing, and stonecutting patterns can be
    used in the same setup.

***

*   <ItemLink id="processing_pattern" />s are where a lot of flexibility in autocrafting comes from. They are the most generalized type, simply
    saying "if a pattern provider pushes these ingredients to adjacent inventories, the ME system will recieve these items at some point in the
    near or distant future". They are how you will autocraft with almost any modded machine, or furnaces and the like. Because they are so
    general in use and do not care what happens between pushing ingredients and receiving the result, you can do some really funky stuff, like inputting
    the ingredients into an entire complex factory production chain which will sort out stuff, take in other ingredients from infinitely-producing
    farms, print the entirety of the Bee Movie script, the ME system does not care as long as it gets the result the pattern specifies. In fact,
    it doesn't even care if the ingredients are in any way related to the result. You could tell it "1 cherry wood planks = 1 nether star" and have
    your wither farm kill a wither upon receiving a cherry wood planks and it would work.

Multiple <ItemLink id="pattern_provider" />s with identical patterns are supported and work in parallel. Additionally, you can have a pattern say,
for example, 8 cobblestone = 8 stone instead of 1 cobblestone = 1 stone, and the pattern provider will insert 8 cobblestone into
your smelting setup every operation instead of one at a time.

## The Most General Form of "Pattern"

There is actually an even more "general" form of "pattern" than a processing pattern. A <ItemLink id="level_emitter" /> with a crafting card can be set
to emit a redstone signal in order to craft something. This "pattern" does not define, or even care about ingredients.
All it says is "If you emit redstone from this level emitter, the ME system will recieve this item at some point in the
near or distant future". This is usually used to activate and deactivate infinite farms which require no input ingredients,
or to activate a system that handles recursive recipes (which standard autocafting cannot understand) like, for example, "1 cobblestone = 2 cobblestone"
if you have a machine that duplicates cobblestone.

# The Crafting CPU

<GameScene zoom="4" background="transparent">
  <ImportStructure src="../assets/assemblies/crafting_cpus.snbt" />
  <IsometricCamera yaw="195" pitch="30" />
</GameScene>

Crafting CPUs manage crafting requests/jobs. They store the intermediate ingredients while crafting jobs with multiple steps are
being carried out, and affect how big jobs can be, and to some degree how fast they are completed. They are multiblocks, and
must be rectangular prisms with at least 1 crafting storage.

Crafting CPUs are made out of:

*   (Required) [Crafting storages](../items-blocks-machines/crafting_cpu_multiblock.md), available in all the standard cell sizes (1k, 4k, 16k, 64k, 256k). They store the ingredients and
    intermediate ingredients involved in a craft, so larger or more storages are required for the CPU to handle crafting jobs
    with more ingredients.
*   (Optional) <ItemLink id="crafting_accelerator" />s, they make the system send out more ingredient batches from pattern providers.
    This allows, say, a pattern provider surrounded by 6 molecular assemblers to send ingredients to (and thus use) all 6 at once instead of just one.
*   (Optional) <ItemLink id="crafting_monitor" />s, they display the job the CPU is handling at the moment. They can be colored via a <ItemLink id="color_applicator" />
*   (Optional) <ItemLink id="crafting_unit" />s, they simply fill space in order to make the CPU a rectangular prism.

Each crafting CPU handles 1 request or job, so if you want to request both a calculation processor and 256 smooth stone at once, you need 2 CPU multiblocks.

They can be set to handle requests from players, automation (export busses and interfaces), or both.

# Pattern Providers

<Row>
<BlockImage id="pattern_provider" scale="4" />

<BlockImage id="pattern_provider" p:push_direction="up" scale="4" />

<GameScene zoom="4" background="transparent">
  <ImportStructure src="../assets/blocks/cable_pattern_provider.snbt" />
</GameScene>
</Row>

<ItemLink id="pattern_provider" />s are the primary way in which your autocrafting system interacts with the world. They push the ingredients in
their [patterns](../items-blocks-machines/patterns.md) to adjacent inventories, and items can be inserted into them in order to insert them into the network. Often
a channel can be saved by piping the output of a machine back into a nearby pattern provider (often the one that pushed the ingredients)
instead of using an <ItemLink id="import_bus" /> to pull the output of the machine into the network.

Of note, since they push the ingredients directly from the [crafting storage](../items-blocks-machines/crafting_cpu_multiblock.md#crafting-storage) in a crafting CPU, they
never actually contain the ingredients in their inventory, so you cannot pipe out from them. You have to have the provider push
to another inventory (like a barrel) then pipe from that.

Also of note, the provider has to push ALL of the ingredients at once, it can't push half-batches. This is useful
to exploit.

Pattern providers have a special interaction with interfaces on [subnets](../ae2-mechanics/subnetworks.md): if the interface is unmodified (nothing in the request slots)
the provider will skip the interface entirely and push directly to that subnet's [storage](../ae2-mechanics/import-export-storage.md),
skipping the interface and not filling it with recipe batches, and more importantly, not inserting the next batch until there's space in storage.

Multiple pattern providers with identical patterns are supported and work in parallel.

Pattern providers will attempt to round-robin their batches to all of their faces, thus using all attached machines in parallel.

## Variants

Pattern Providers come in 3 different variants: normal, directional, and flat. This affects which specific sides they push
ingredients to, receive items from, and provide a network connection to.

*   Normal pattern providers push ingredients to all sides, receive inputs from all sides, and, like most AE2 machines, act
    like a cable providing network connection to all sides.

*   Directional pattern providers are made by using a <ItemLink id="certus_quartz_wrench" /> on a normal pattern provider to change its
    direction. They only push ingredients to the selected side, receive inputs from all sides, and specifically don't provide a network
    connection on the selected side. This allows them to push to AE2 machines without connecting networks, if you want to make a subnetwork.

*   Flat pattern providers are a [cable subpart](../ae2-mechanics/cable-subparts.md), and so multiple can be placed on the same cable, allowing for compact setups.
    They act similar to the selected side on a directional pattern provider, providing patterns, receiving inputs, and not
    providing a network connection on their face.

Pattern providers can be swapped between normal and flat in a crafting grid.

## Settings

Pattern providers have a variety of modes:

*   **Blocking Mode** stops the provider from pushing a new batch of ingredients if there are already
    ingredients in the machine.
*   **Lock Crafting** can lock the provider under various redstone conditions, or until the result of the
    previous craft is inserted into that specific pattern provider.
*   The provider can be shown or hidden on <ItemLink id="pattern_access_terminal" />s.

## Priority

Priorities can be set by clicking the wrench in the top-right of the GUI. In the case of several [patterns](../items-blocks-machines/patterns.md)
for the same item, patterns in providers with higher priority will be used over patterns in providers with lower priority,
unless the network does not have the ingredients for the higher priority pattern.

# Molecular Assemblers

<BlockImage id="molecular_assembler" scale="4" />

The <ItemLink id="molecular_assembler" /> takes items input into it and carries out the operation defined by an adjacent <ItemLink id="pattern_provider" />,
or the inserted <ItemLink id="crafting_pattern" />, <ItemLink id="smithing_table_pattern" />, or <ItemLink id="stonecutting_pattern" />,
then pushes the result to adjacent inventories.

Their main use is next to a <ItemLink id="pattern_provider" />. Pattern providers have special behavior in this case,
and will send information about the relevant pattern along with the ingredients to adjacent assemblers. Since assemblers auto-eject the results of
crafts to adjacent inventories (and thus into the return slots of the pattern provider), an assembler on a pattern provider
is all that is needed to automate crafting patterns.

<GameScene zoom="4" background="transparent">
<ImportStructure src="../assets/assemblies/assembler_tower.snbt" />
<IsometricCamera yaw="195" pitch="30" />
</GameScene>
