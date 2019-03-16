#交错订单策略
以一定的时间间隔下大量的买卖订单，包括从非常低的价格到非常高的价格的订单。只要用户打算执行策略，这个范围就应该涵盖所有可能的价格。这可能是从-100x到+100x（-99%到+10000%）。利润将从价格变动中获得，而这一策略会对价格变动产生摩擦。它给市场带来深度，让它们看起来更好。它从不“亏本出售”，而是总是以利润出售。

这种策略在不在线的笔记本电脑和电脑上运行良好。如果你一天运行几次，一周或一个月运行一次，它会非常好地工作。如果它一直在线的话，可能会获得更多的利润，但即使这样也不确定。这取决于市场条件。

##参数和配置

- Mode:山顶，中性，谷底，阶梯挂买单，阶梯挂卖单。解释较低。
- Spread: 你的最高卖单价和最低卖单价之间的差价（%）
- Increment: 订单的增量（%）
- Lower bound:你预计价格会降到多低？采购订单将从中心价格降到这个价格。以base资产计量的quote资产的价格。
- Upper bound: 你预计价格会升到多高？采购订单将从中心价格升到这个价格。以base资产计量的quote资产的价格。
- Allow instant fill:当多个订单完成，价格立即返回时，bot必须下可能立即完成的订单。如果启用此选项，目标利差将很容易恢复，并将立即获得一些利润。如果这被禁用，bot将不得不删除一些订单以获得继续运行所需的资金。默认设置为“开”，我们建议保持此设置。
- Operational depth:要在帐簿上维护的实际订单数。不要让所有的订单都覆盖整个范围，只保留N个订单深度。

## 逻辑
首次下单

每次启动时，策略都会检查指定市场上是否有买入和卖出订单。如果没有订单，策略将从远端（下限和上限）开始一个接一个地下达买卖订单。这将导致获得尽可能最好的价格，即使中心价格不在预期的位置或在启动后移动。

订单的价格是的距离price * (1 + increment)。订单金额自动计算。范围越大，订单量就越小。增量越小，订单量越小。
## 盈利方式

机器人程序发出指令，以相同的总价格买回更多的资产，以更高的价格买回所有的资产。这样，每次价格向相反的方向移动时，利润就会实现。当价格来回变动时，会产生一点或多点小利润，并立即进行再投资以增加未来利润。只要价格在任何地方变动，并且价格保持在指定范围内，这种情况就可以继续下去。

##价差、增量和利润

增量是订单之间的距离，价差是最高买入价和最低卖出价之间的距离。实际利润将不等于您可能认为的名义价差。利润将介于价差和价差增量之间。为什么？因为由此产生的利润是差价交易和波动性交易的组合。让我们来看一个简单的例子来理解这一点。
示例设置：
价差：10%
增量：4%
订单价格：83 87 91 95<center>105 109 113 117

虽然价格不会在任何地方变动，但您可以从价差中获利（105-95=10），这将得到最大利润百分比。然后假设95的购买订单已经成交。下一个销售订单的价格为101。如果也成交了，实现利润为101-95=6

注：在重大价格变动中，非阶梯模式实际上带来更大的利润。
## 订单完全成交
一边的订单成交将导致另一边新建订单。新建的订单接近于`price * (1 + increment)`
##部分成交订单
当一方有部分完成的订单时，策略不会立即分配新得的资金。相反，它将保留下一个更接近中心价格的订单所需的金额。
此外，如果买卖双方都存在导致双方订单部分完成的交易，那么如果有足够的资金，策略将用新的完整订单取代这些订单。
##额外资金分配
新的可用资金可能来自交易利润和/或来自其他账户的转账。在这两种情况下，这些资金将通过扩大范围（如果需要）或/和增加现有订单大小来分配。
## 作业深度

交错订单策略的作用范围很广，比如-100x到+100x。要覆盖如此大的范围，可能需要数百甚至数千个订单。维护这样的订单数量会给策略执行时间、区块链（按订单下达和取消交易）带来很大的开销，而且初始订单下达还需要大量的时间。此外，使用价差和增量也需要替换所有订单。

由于实际的交易是围绕市场中心价格进行的，因此只需在中心附近保留N个订单就可以处理近中心范围内的价格变动。
设置作业深度时应考虑的基本因素：
- worker在线百分比。在线worker越少，处理价格变动所需的深度就越大。
- 增加大小。使用的增量越小，所需的深度就越大。否则，worker可能无法从购买或出售大中获益。
操作深度逻辑如下：
- 当初始订单放置发生时，只有n个深度的订单被放置到订单簿中，其余的订单作为“虚拟”订单保存在内存中。
- 每次重新启动时，该策略将根据当前最远的实际订单量恢复所有虚拟订单。
- 在价格变动方面，虚拟订单根据需要替换为实际订单，以保持市场上不少于n个实际订单。
- 当价格变动指向一边时，另一边可能累积过多的订单（n+x）。如果此侧的实际订单数超过n+阈值（阈值在代码中定义，稍后可以更改，因此此处省略当前值），则这些过量订单将自动替换为虚拟订单。请注意，最远的实际订单只有在其金额与靠近中心的下一个订单相同时才会被替换。这种情况是一种不得打破正常资产平衡分配的交易方。
##范围扩展
用户可以随时调整范围边界。该策略将通过交易利润或从外部转移的资金追加订单，以覆盖新的范围。如果边界缩小，新的可用资金将用于增加订单大小。

## 未达到目标价差时的回退逻辑
在一些罕见的情况下，可能会出现所有资金都已分配的情况，但尚未达到目标价差。在这种情况下，该策略将取消最远的买入或卖出订单，并使用这些资金将下一个更靠近中心价格的位置放置，以达到目标价差
## 模式
### 山

-Buy orders same QUOTE
-Sell orders same BASE

山模式将资金更多地集中在中心，因此“现在”它可以获得更多的利润，并更快地增加利润，但如果价格决定大幅波动，这就不太好了。
订单大小增加：最大化订单尺寸，尽可能靠近中心。当所有订单都为最大时，新的增加将从最远的订单开始。

### 谷

Buy orders same BASE
Sell orders same QUOTE

Valley模式用于引导市场或高度波动的市场。如果价格保持在最初的水平，利润微乎其微，但能够承受巨大的变化并喜欢波动。

订单大小增加：首先从中心尽可能地最大化订单大小。当所有订单都为最大时，新的增加最接近中心订单开始。
### 阶梯买单
All orders same BASE (profit comes in QUOTE)
所有订单的base相同（利润来自quote）

阶梯买卖有利于积累其他资产。例如，你可以用这种策略投资5万美元，并通过大量100美元的订单获得利润。就像挤奶市场或“金融独立模式”
订单规模增加：尽可能将订单规模最大化。买单尽可能最大化并远离中心价格（与Valley相同），卖单尽可能接近中心价格（与Mountain相同）。
### 阶梯卖单
All orders same QUOTE (profit made in BASE)
所有订单同一报价（base利润）

订单大小增加：尽可能将订单大小最大化。买单尽可能接近中心价格（与山相同），卖单尽可能远离中心价格（与谷相同）。
###中性的

从远端到中心的买单：lower_order_base * sqrt(1 + increment)

从远端向中心的卖单：higher_order_quote * sqrt(1 + increment)

中性模式适用于任何市场，在山模式和谷模式之间是一个很好的平衡，因为订单量稍微大一些，朝向中心。它将在稳定的时期和极端的运动中很好地工作，让你在任何时候都能安心。

订单大小增加：通过将订单大小增加到中性，尝试将所有内容变平。当一切都正确时，最大化最近的订单，然后增加其他订单以匹配它。
## 其他功能

###崩溃和恢复

该策略不需要记住任何“状态”，只依赖于区块链的实际数据。这可能允许您使用一台计算机启动该策略，在任何时候中断它，然后继续使用另一台计算机。您只需要具有相同的设置。尽管您也可以更改设置并继续，但策略将根据新设置下新订单。
###重新评估

每次行动后，机器人将重新评估整个情况并采取相应的行动。它不会假定一个订单已经成功完成，而是每次都用新的眼光看待这个情况。这消除了一些棘手的情况和奇怪的行为。

###操作模式和范围可随时更改

如果更改了这些，bot将删除定义范围之外的订单，并根据当前配置分配所有资金。如果范围增加，就会导致bot创建新的订单来填充新的范围。改变操作模式会使所有订单保持原样，只会改变未来的行为。
###单边起动

如果用户只从base或quote开始，bot会将订单放在接近市场价格的位置，然后等待一个订单成交，游戏就开始了。利润将用于向另一方添加订单，直到策略完全平衡（根据配置）。

##考虑事项
###范围

最重要的是要使范围（上限和下限）足够宽。如果你不这样做，你最终只会得到更糟糕的资产。你想这样吗？如果没有，使用大范围。我们建议+-100x。是的，10000x范围。使用山地和中立模式，将您的范围从10倍增加到100倍的成本很低，所以做它。对于Valley模式，成本很高，但是如果您开始使用它，您希望它具有巨大的波动性，那么也要这样做。用阶梯买扩展上界是便宜的，而用阶梯卖则相反。

###增量和价差

增量越小，订单完成的频率就越高，但每个订单的利润就越小。（资金数额相同）。

价差越小，订单越多，利润也越小。在某个地方可能有个好地方。如果你愿意的话，你也可以使用像10000%这样的巨大价差，但是你是否需要一个机器人来完成这个价差还是有疑问的，因为一个订单可能每年都要完成一次左右。

如果您打算在一台始终在线的计算机上运行该策略，那么较小的利差和增量可能是有意义的。如果您希望每天运行一次bot，请尝试默认排列（6%）和增量（4%）。如果您打算每周运行一次bot，那么健全的值可能是20%的分布和10%的增量。

注意：避免在不取消所有订单的情况下更改增量和排列。这可能导致损失。参见“分摊、增加和利润”一节。

期初余额

最好从两种资产的“等量”开始策略（如果你有一个对称的范围）。quote金额/价格应为“base金额”。