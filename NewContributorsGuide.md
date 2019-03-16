#新贡献者指南
##介绍

你好，新贡献人，欢迎来到DexBot。我们是一个利用Bitshares DEX进行开源开发的团队。开始之前，请注意以下事项：
有关dexbot的一般信息，请访问网站- <a href="www.dexbot.info" target="_blank">www.dexbot.info</a>

如果你想参与进来，你可以加入我们的电报dexbot聊天室，在那里你可以问问题和获得帮助。
有关为该项目提供资金的工人提案的信息可在此处找到。- <a href="https://www.dexbot.info/2018/12/12/cabinet-multisig-dexbot-wp2/" target="_blank">https://www.dexbot.info/2018/12/12/cabinet-multisig-dexbot-wp2/</a>

Key project members are:
- Project Manager: @permie
- Lead Developer: @octomatic
- Supporting Developer: @vvk123
- Build Maintainer: @joelva
- Quality Assurance : [ Role is open ]
##贡献者行为准则协议
请参见- <a href="CODE_OF_CONDUCT.md" target="_blank">《献者行为准则协议》</a>。本行为准则改编自bitshares-ui和the Contributor Covenant,，版本1.4。
##开发过程
本项目周期为2019年1月1日至2019年6月30日。这个周期的路线图可以在dexbot工作流电子表格中查看。
##请求一个功能特性
- 检查问题列表，如果有人已请求该功能，则签入问题
- 在问题列表中创建新功能特性的描述
##报告错误
- 检查问题列表，是否有人已经报告了错误。
- 使用描述性名称创建新问题。
- 描述如何重现错误。如果可能，使用图像或GIF。
##参与发展
一般流程如下：sprint->review&merge->release

- 根据需要发布构建版本，并由项目经理宣布。我们目前估计构建将每两周发布一次。
- 发布候选人在发布前坐1-2周供公众评估
- bugs总是在增强之前工作
- 开发人员应该根据对应于问题git checkout-b 123 fix gui按钮的编号分支来处理每个问题，该按钮将引用问题123。有关详细信息，请参阅《Git工作流指南》。
- 我们为尚未提出要求的问题支付奖金。如果你按照这些准则来解决这个问题，并且你的公关被接受了，你将赢得奖金。
- 如果您是新来的，请查看已标记为“Good First Issue”的问题。在开始开发之前，请对这个问题发表评论，提交一个您将为完成开发而收取的价格。
- 
另外，请致电T.ME/DEXBOBTS与我们联系。对不要求赏金的工作是不会得到报酬的。

- 要声明一个问题，只需在工作请求和工时估计中留下一条评论。或者，通过电报联系项目经理。

- 如果问题已被分配，不要试图再要求它。外部开发人员声明的问题将没有分配的开发人员，但在括号中有开发人员的名称。如果您无法在里程碑名称上指示的日期之前完成问题，请不要提出请求。如果某个问题错过了预期的里程碑完成，请务必对您的进度进行解释，包括延迟的原因。这个问题被推到下一个里程碑。如果不进行解释或完成问题，将导致版本发布的问题。

以下是正在进行的项目和bugs和开发的列表：<a href="https://github.com/Codaone/DEXBot/projects/" target="_blank">bugs和开发列表</a>

##Bug 修复列表
一个例子：<a href="https://github.com/Codaone/DEXBot/projects/5" target="_blank">bug修复例子</a>
##其他支持活动
您是新加入开源的吗？以下是一个很好的指南：https://opensource.guide/
##你能做出什么贡献？
-文档？
-用户体验？
-策略？
-数据分析？
-绘图？
-信息图表？
-视频？
-用户帮助？
用电报联系项目组。我们准备支付有意义的贡献。
##code风格准则
我们的风格指南基于PEP-8标准https://www.python.org/dev/peps/pep-0008/除了一些例外：
- 行不需要严格为80个字符，最多可接受120个字符。
- 编写一般可读的代码，例如避免使用短的单字母变量，而是使用更具描述性的代码。
- Git提交风格指南-https://chris.beams.io/posts/git-commit/
-如果您想使用IDE，我们推荐Pycharm。如果您希望使用不同的IDE，还有许多PEP-8标准代码验证器。
一般编码指南：
- 保持简单。试着考虑未来维护的发展。
- 必要时编写单元测试
- 如果希望使用比当前项目实现更新的新库或包，请首先与项目经理和开发人员联系。
- 使用相应的setuptools、setup.py和requirements.txt添加新包。
##构建环境

我们强烈建议在本地开发环境中使用virtualenv。有关如何将virtualenv与python 3.6结合使用的更多信息，请参见：
https://docs.python.org/3.6/tutorial/venv.html网站
Git工作流：
请参阅https://github.com/codaone/dexbot/wiki/git-workflow
