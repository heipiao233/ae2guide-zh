---
navigation:
  title: 提示和技巧
  position: 20
---

# 提示和技巧

一些小提示

* 删除高清修复。
* 你可以旋转或移动有缩放和显示/隐藏注解按钮的情景。
* 保持树状网络，避免循环。
* Full-block [devices](ae2-mechanics/devices.md) in groups of 8 or less unless you deeply understand how [channels](ae2-mechanics/channels.md)
  route through a network
* 为所有 [样板](items-blocks-machines/patterns.md) 选用并坚持一种木头。允许替换有时的确有效，但是在任何地方使用相同木材可以大大减少麻烦。
* 在 <ItemLink id="pattern_access_terminal" /> 中竖直排列你的 [样板](items-blocks-machines/patterns.md)/在你的 [提供器](items-blocks-machines/pattern_provider.md) 间分发样板，
  这样即可并行处理配方。
* 加入一个 [能源元件](items-blocks-machines/energy_cells.md)，这样网络可以应对用电高峰。
* 你可以在 <ItemLink id="condenser" /> 中使用水。
* 最好保持网络整洁的方式是不要把乱七八糟的怪物掉落物（剑和盔甲）放入。
  任何不同的耐久度和附魔的组合都是不同的 [类型](ae2-mechanics/bytes-and-types.md)。
* 一个“物品进入事件”只会在通过 <ItemLink id="import_bus" />，<ItemLink id="interface" /> 或者 <ItemLink id="pattern_provider" />输入生成物时发生。
  你不能只把生成物存入到一个连接了 <ItemLink id="storage_bus" /> 的箱子。
* 不要忘记你可以旋转或移动有缩放和显示/隐藏注解按钮的情景。
* <ItemLink id="pattern_provider" /> 只会把一个配方的所有原料推入一个方向。这保证机器不会只得到部分原料，但是有时希望原料放入多个位置。
  你可以通过 <ItemLink id="interface" /> 实现，要么作为一个 ["管道" 子网络](example-setups/pipe-subnet.md)，要么使用它保存多个不同物品、流体、化学品等的能力，来把它用作一些中间箱子/储罐。
* 你可以旋转或移动有缩放和显示/隐藏注解按钮的情景。
