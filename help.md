欢迎使用dexbot wiki！

dexbot是一个做市机器人,它的资金来源是一个BitShares Worker。机器人程序的目的是让任何人都能在比特股去中心化交易所（DEX）的任何市场上轻松提供流动性。该软件将尽可能易于使用。它会有保守和稳健的默认值，以便人们可以轻松开始使用。用户可以把他们的资产使用起来-增加DEX的价值-并有希望获取利润，而不是简单地持有。当然，不能保证获取利润。

该项目的目标是增加DEX的流动性，并通过向普通加密货币持有者提供更多的使用场景来增加bitShares的吸引力。

由于dexbot是由社区作为一个整体资助的，所包含的策略应该增加整体的价值。因此，dexbot将只包括提供流动性的策略。积极的交易策略会降低流动性，增加机器人使用者的价值，但不会增加整体的价值，所以应该由其他机器人提供。

机器人不必不停地运行。所下的订单将保留在帐簿上，一旦再次联机，dexbot将根据策略更新订单。这是有意的，这样任何用户都可以在自己的笔记本电脑上使用机器人。

# 使用

现在，dexbot包含两种策略：

- 相对订单，它将买入订单放在下方，卖出订单放在假定的中心价格之上。它适用于有足够参与者的成熟和活跃的市场。在不活跃和参与度低的市场中，机器人程序肯定会造成损失。

- 交错订单，适用于所有市场，尤其适用于引导市场。它从波动中获利，如果你把它用在一项毫无价值的资产上，它会让你损失所有的钱。

- <a href="home.md" target="_blank">Home</a>
- <a href="CenterPriceOffset.md" target="_blank">基于资产余额的中心价格的偏移量</a>
- <a href="CommonProblems.md" target="_blank">常见问题</a>
- <a href="ConfigFileLocations.md" target="_blank">配置文件位置</a>
- <a href="DynamicCenterPrice.md" target="_blank">动态中心价格</a>
- <a href="FixedCenterPrice.md" target="_blank">固定中心价格</a>
- <a href="FixedOrderSize.md" target="_blank">固定订单大小</a>
- <a href="FixedSpread.md" target="_blank">固定价差</a>
- <a href="GitWorkflow.md" target="_blank">Git工作流程</a>
- <a href="HowtoCustomiseDEXBot.md" target="_blank">怎样定制化DEXBot</a>
- <a href="HowtoDebug.md" target="_blank">怎样调试</a>
- <a href="Install_on_Digital_Ocean_Droplet18.04_LTS.md" target="_blank">Digital_Ocean_Droplet18.04_LTS安装指南</a>
- <a href="NewContributorsGuide.md" target="_blank">新贡献者指南</a>
- <a href="RelativeOrderSize.md" target="_blank">相对订单大小</a>
- <a href="SetupGuideforMacOSX10.12orhigher.md" target="_blank">MacOSX10.12或更高版本安装指南</a>
- <a href="TheRelativeOrdersStrategy.md" target="_blank">相对订单策略</a>
- <a href="TheStaggeredOrdersStrategy.md" target="_blank">相对订单策略</a>
- Setup Guide for Linux
- Setup Guide for Raspberry Pi
- Setup Guide for Windows



