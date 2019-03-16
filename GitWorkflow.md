我们建议采用以下实践来管理自己和他人的代码版本。Git对很多人来说很奇怪，但是它非常流行和灵活，绝对值得学习。Git有一些快捷命令，我会尽量避免使用它们，因为如果你不理解它们,会导致更多的混乱。
# 准备
## 创建个人Github仓库
1. do it
2. 通过访问`https://github.com/codaone/dexbot`并按“fork”，将dexbot克隆到您的个人仓库。不是“克隆或下载”，而是“fork”。

既然您有了公共仓库，那么必须将其与计算机上的本地副本进行配对：
## 安装和配置Git
`sudo apt install git gitg meld`
GitG是Git的默认图形界面，而Meld是比较文件和Git版本的图形工具。现在，您必须至少使用以下信息配置Git：
- `git config --global user.name "<Name Surname>"`
- `git config --global user.email "<email@domain.tld>"`
##创建公钥并将其添加到GitHub
Git默认使用ssh，GitHub可以通过ssh密钥对对您进行身份验证。这将使您能够使用来自终端的简单命令将代码“推送”到GitHub。
`ssh-keygen`
按Enter键接受默认值。如果您需要额外的安全性，可以提供密码短语。这将要求您在每次使用ssh或push with git时输入它。你也可以让它空着。很安全。现在您将拥有一个私钥：`id_rsa`和一个公钥：`id_rsa.pub`.
现在转到Github设置页面。添加一个新的密钥，并在输入字段中粘贴您的公钥，您可以使用`less ~/.ssh/id_rsa.pub`获得该公钥。只需复制文本并将其粘贴到Github。就是这样。
## 将您的个人Github仓库克隆到您的计算机上
进入要创建“dexbot”文件夹的目录。从个人仓库的“克隆或下载”中复制链接。选择“使用ssh”。然后在您的终端上输入：`git clone<the link you just got>dexbot`。命令中最后一个“dexbot”是将创建的文件夹的名称。你可以用任何你想要的名字。
现在您有了一个带有dexbot的Github存储库和一个具有相同dexbot的本地存储库。使用cd dexbot进入目录。您的计算机现在将Github仓库称为“origin”。现在，您也可以从其他仓库导入版本，因此可以直接从中获取改进：
## 向感兴趣的上游仓库添加引用
我将使用codaone和bitfag作为例子，但您可以使用任何您喜欢的。
- `git remote add codaone git@github.com:Codaone/DEXBot.git`
- `git remote add bitfag git@github.com:bitfag/DEXBot.git`
- `git remote add <some other> <git@some other public repo.git>`
现在您可以将这些仓库称为“codaone”或“bitfag”，而您的个人仓库称为“origin”。使用`git fetch codaone`或`git fetch bitfag`等获取这些文件的本地副本。
#工作流程
## 从其他人那里pull当前状态
`git fetch codaone`将为您提供codaone/dexbot所有分支的本地副本。您可以对bitfag和您添加的任何其他远程仓库执行相同的操作。这不会对当前分支（文件结构中的任何文件）进行任何更改。现在，您将能够chechout（view）任何已配置仓库的任何分支，或者将它们与当前分支进行比较/合并。

签出分支意味着观察或处理该分支中的文件版本。文件和目录将表示该分支，您将看不到来自其他分支的任何内容。使用：`ggit checkout codaone/whatever_branch`或`git checkout some_local_branch`。远程分支需要预先设置远程仓库名称，但本地分支不需要。
我建议不要签出“远程”分支以进行其他测试。您可以进行安装以尝试。每次执行此操作时，dexbot gui/cli都将替换为新的。
## 为自己的工作创建本地分支
我建议你在当地的分支机构做所有你想完成的工作。选择要从哪个分支开始工作。最安全的起点是当前的codaone:master，所以git签出codaone/master，然后用git分支创建一个分支。然后checkout你的新分支。
## 保存当前状态或工作的快照
无论您处理的文件是什么，以及您要保存的文件，都需要添加到版本控制中：`git add<filename.suffix>`中。现在Git正在追踪他们。

您可以看到具有git状态的版本状态。它将告诉您哪些文件已更改或暂存。如果你编辑一个文件并保存它，“git status”会告诉你它已经改变了。您需要使用`git commit -m "what has changed"`单独保存新状态。现在更改已经保存在本地，您可以在将来的任何时候返回到这一点并查看发生了什么。一旦提交，“git status”将不再显示更改的文件，因为它们是新状态的一部分。
##公开您的更改
你可能对你所做的感到满意。您可以将更改作为单独的分支推送到公共仓库中，或者将它们合并到主仓库中并将新的主仓库推送到GitHub中。
## 更新并做出新的贡献
假设您是一个新的贡献者，它将codaone master分叉并添加了remote：
`$ git remote -v`
`codaone    git@github.com:Codaone/DEXBot.git (fetch)`
`codaone    git@github.com:Codaone/DEXBot.git (push)`
`origin    https://github.com/NewDeveloper/DEXBot.git (fetch)`
`origin    https://github.com/NewDeveloper/DEXBot.git (push)`
要从Codaone获取最新的开发分支，请执行以下操作:
`$ git checkout -b devel --track codaone/devel`
然后，在本地对您自己的分支进行功能编辑，例如问题500，用户体验错误：
```
$ git checkout -b  500-user-experience-bugs
$ git add ….
$ git commit -m "……."
$ git push --set-upstream origin 500-user-experience-bugs
```
如果更改出现在devel分支上，在它们能够发出请求之前，为了合并上游更改：
```
$ git fetch codaone devel
$ git merge codaone/devel
```
转到Web并单击“从origin提取/500用户体验Bug到CodaOne/Devel分支”
一般来说，pull=（fetch+merge）
## 向其他人提议您的更改
您可以通过向上游响应机构提出请求来建议分支机构中的更改。
从Github指南创建拉请求：
- 在Github上，导航到仓库的主页。
- 分支下拉菜单在“分支”菜单中，选择包含提交的分支。
- 将请求按钮拉到分支菜单右侧，单击新建请求。
- 用于选择基本分支和比较分支的下拉菜单使用基本分支下拉菜单选择要将更改合并到的分支，然后使用比较分支下拉菜单选择在其中进行更改的主题分支。
- 请求标题和描述字段为请求标题和描述。
- “创建拉请求”按钮若要创建可供审阅的拉请求，请单击“创建拉请求”。要创建拔模请求，请使用下拉列表并选择“创建拔模请求”，然后单击“拔模请求”。有关提取请求草案的详细信息，请参阅“关于提取请求”。
## 废弃你的工作，换成上游版本
您可以通过`git revert`撤消对存储库提交历史记录的更改。
还可以使用其他撤消命令（如`git checkout`和`git reset`）将头引用指针和分支引用指针移动到特定的提交。git revert不移动poiners，但它将创建一个新的“revert commit”
示例：若要还原头中最后第四次提交所指示的更改，可以执行以下操作：
`git revert HEAD~3`
##References略...