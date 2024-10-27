---
navigation:
  title: 入门 (1.20+)
  position: 10
---
<div class="notification is-info">
    以下信息只适用于 Minecraft 1.20 和以上的《应用能源 2》。
</div>

# 入门

## 获取基础材料

<GameScene zoom="4" background="transparent">
  <ImportStructure src="assets/assemblies/meteor_interior.snbt" />
</GameScene>

为了开始应用能源 2 之旅，你必须先找到一个[陨石](ae2-mechanics/meteorites.md)。它们很常见，而且会在地表留下一个大坑，所以你在旅途中很可能遇到它们。
如果没有，你可以合成一个 <ItemLink id="meteorite_compass" />，它会指向最近的 <ItemLink id="mysterious_cube" />。

一旦找到陨石，请挖掘到它的中心，里面有赛特斯石英簇、赛特斯石英芽，各种 [赛特斯石英母岩](items-blocks-machines/budding_certus.md) 和正中间的神秘方块。

挖掘赛特斯石英簇和赛特斯石英块。你也可以挖掉赛特斯石英母岩，但是如果没有精准采集，它们会降级 1 级。

不要破坏任何无瑕的赛特斯石英母岩，因为即使有精准采集，它们也会降级为有瑕的赛特斯石英母岩，并且无法修复。

还要挖掉中间的神秘方块来获得全部四个压印模板。

## “种植”赛特斯石英

<GameScene zoom="4" background="transparent">
<ImportStructure src="assets/assemblies/budding_certus_1.snbt" />
</GameScene>

赛特斯石英芽会从 [赛特斯石英母岩](items-blocks-machines/budding_certus.md) 中生长，就像紫水晶，如果你破坏一个赛特斯石英芽，它会掉落一个 <ItemLink id="certus_quartz_dust" />，与时运无关。如果你破坏了一个成熟的赛特斯石英簇，它会掉落四个 <ItemLink id="certus_quartz_dust" />，时运会增长这个数字。

赛特斯石英母岩有四个等级：无瑕的、有瑕的、开裂的和损坏的。

<GameScene zoom="4" background="transparent">
<ImportStructure src="assets/assemblies/budding_blocks.snbt" />
<IsometricCamera yaw="195" pitch="30" />
</GameScene>

每当一个芽生长一个阶段，母岩都有可能降级一级，也可能变成一个普通的赛特斯石英块。通过与一个或多个 <ItemLink id="charged_certus_quartz_crystal" /> 一同丢入水中，可以修复它们。

<RecipeFor id="damaged_budding_quartz" />

无瑕的赛特斯石英母岩不会降级，而会无限生长赛特斯石英，但是它们不能合成或用镐移动，即使有精准采集。（它们可以通过 [空间塔](ae2-mechanics/spatial-io.md) 移动）

仅通过它们自己，赛特斯石英芽生长很慢。然而，把<ItemLink id="growth_accelerator" /> 放在母岩旁可以显著加快其生长。你应该把建造一些这种结构作为首要任务。

<GameScene zoom="4" background="transparent">
<ImportStructure src="assets/assemblies/budding_certus_2.snbt" />
<IsometricCamera yaw="195" pitch="30" />
</GameScene>

如果你没有足够同时制作 <ItemLink id="energy_acceptor" /> 和 <ItemLink id="vibration_chamber" /> 的石英，
你可以制作一个 <ItemLink id="crank" /> 并把它放在催生器上。
这是 [自动收获赛特斯石英的方法](example-setups/simple-certus-farm.md)。

## Fluix 简介

需要的另一个材料是福鲁伊克斯，在你制作催生器时已经遇到了。它是通过向水中投入充能赛特斯石英水晶、红石粉和下界石英得到的。完成这一自动化的任务“留给读者”。

如果你没有，为了生产 <ItemLink id="charged_certus_quartz_crystal" />，还需要 <ItemLink id="charger" />。

## 压印一些处理器

在陨石的战利品中，有四个来自神秘方块的“压印模板”。它们被用来在 <ItemLink id="inscriber" /> 中制作三种处理器。

<ItemGrid>
  <ItemIcon id="silicon_press" />

<ItemIcon id="logic_processor_press" />

<ItemIcon id="calculation_processor_press" />

<ItemIcon id="engineering_processor_press" />
</ItemGrid>

压印器是一种有方向的机器，就像原版熔炉。上方或下方插入的物品会出现在上方或下方的格子里。
从侧方或后方插入的物品会出现在中间的格子。产物从侧方或后方取出。

为了实现基于漏斗的自动化（并且减少乱麻般的管道），压印器可以用 <ItemLink id="certus_quartz_wrench" /> 旋转。

制造一点各种处理器是为下一步制作一个基础的 ME 系统的准备。自动化生产“留给读者作为练习”。

## “物质-能量”（Matter Energy）科技：ME 网络和存储

### ME 存储是什么？

“ME” 按英文字母读法发音，意为 “物质-能量”。

“物质-能量” 是《应用能源 2》的主要部分，就像一个疯狂科学家版的多方块箱子，可以革命你的存储现状。ME 和 Minecraft 中其他存储系统大相径庭。
而它需要付出一点出格的思考才能驾驭；但是一旦你开始在小空间内大量存储，多地址终端只是可能性的冰山一角。

### 我需要知道什么？

首先，ME 在 [存储元件](items-blocks-machines/storage_cells.md) 中储存其他物品；存储元件有 5 级，级别越高储存空间越大。
为了使用存储元件，它必须放在一个 <ItemLink id="chest" /> 或 <ItemLink id="drive" /> 中。

<ItemLink id="chest" /> 直接显示元件里的物品，而且你可以直接放入或取出物品，就像在 <ItemLink id="minecraft:chest" /> 里一样，
区别在于物品实际储存在存储元件中，而不是 <ItemLink id="chest" /> 本身。

尽管 <ItemLink id="chest" /> 是个很好地了解 ME 观念的方法，但是为了真正取得好处，你需要建立 [ME 网络](ae2-mechanics/me-network-connections.md)。

## 你的第一个 ME 系统

现在你有了使用《应用能源 2》的所有基础材料和机器，可以制作你的第一个 ME（物质-能量）系统。
它非常基础，没有自动合成，没有物流，只是个简单、好用、可搜索的存储。

<GameScene zoom="6" interactive={true}>
<ImportStructure src="assets/assemblies/tiny_me_system.snbt" />

</GameScene>

* 原料清单：
  * 1x <ItemLink id="drive" />
  * 1x <ItemLink id="terminal" /> 或 <ItemLink id="crafting_terminal" />
  * 1x <ItemLink id="energy_acceptor" />
  * 一些 [线缆](items-blocks-machines/cables.md)，可以是玻璃的、智能的、包层的，但不能是致密的。
  * 一些 [存储元件](items-blocks-machines/storage_cells.md), 建议用 4k 的，它综合存量和类型限制
    （如果以 1k 和 4k 混合的方式 [分区](items-blocks-machines/cell_workbench.md) 更好，但那是我们目前不需要掌握的）

---

1. 放下驱动器
2. 能源接收器 （和其他 AE2 [设备](ae2-mechanics/devices.md)）有方块和面板两种模式。它们可在合成方格中切换。如果你的能源接收器是方块，把它放在驱动器旁。
    如果是面板，在驱动器旁放一个线缆，再把接收器放在上面。
3. 从你喜欢的发电模组上接一根线缆/管道/导线到能源接收器上。
4. 在驱动上方放一个线缆（或者其他在眼睛那层的地方），把终端或合成终端放上去。
5. 把存储元件放入驱动器
6. 获益于此
7. 瞎改终端设置
8. 享受你的无上力量
9. 意识到这个网络宏观来讲非常渺小

### 扩展你的网络

现在，你有了一些基础存储和对存储的访问。这是个好的开始，但是你可能考虑自动化一些处理。

一个很好的例子是把 <ItemLink id="export_bus" /> 放在熔炉上方来放入原矿，把 <ItemLink id="import_bus" /> 放在下方来取出成矿。

<ItemLink id="export_bus" /> 让你从网络导出物品到附着的物品栏，而 <ItemLink id="import_bus" /> 从附着的物品栏导入物品到网络。

### 克服限制

这时你可能有接近 8 个 [设备](ae2-mechanics/devices.md)，一旦达到 9 个你需要管理 [频道](ae2-mechanics/channels.md)。
大部分（不是全部）设备需要一个频道来工作。

默认一个网络支持 8 个频道，一旦打破这个限制，你需要向网络加一个 <ItemLink id="controller" />。这让网络极大地扩展。
[智能线缆](items-blocks-machines/cables.md) 让你看到频道怎么在网络中路由。如果你想了解频道如何工作或者有太多红石和荧石，可以广泛使用它们。
