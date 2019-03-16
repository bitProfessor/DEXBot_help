#MacOSX10.12或更高版本安装指南
##请注意，仅OSX 10.12+及以上版本支持DexBot。

>2018年10月24日-在OSX 10.13.6上为python 3.7确认

在MacOS High Sierra 10.13.6上测试，向下滚动查看Sierra 10.12.6版本
##安装
打开终端
首先，确保从https://python.org安装了python3版本。此安装将不适用于默认的python v2

通过在要检查的命令行中键入python3来确保python3安装在您的路径中。
```
$ python3
Python 3.7.0 (v3.7.0:1bf9cc5093, Jun 26 2018, 23:26:24) 
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```
其次，检查openssl的版本及其位置:
```
$ openssl version -a 
OpenSSL 1.0.2p  14 Aug 2018
```
如果未安装，可以使用以下命令进行安装:
```
$ brew install openssl
$ cd /usr/local/include 
$  ln -s ../opt/openssl/include/openssl .
```
检查openssl版本现在是否正确。如果不正确，则需要通过添加~/.bash_配置文件来修复路径。
```
export PATH="/usr/local/opt/openssl/bin:$PATH"
```
如果您对操作系统做了很多修改，我们建议您在虚拟环境中构建。
要创建一个虚拟环境，请确保在源代码上方的目录中创建它：
```
$ gunzip DEXBot-0.7.9.tar.gz 
 $ tar -xvpf DEXBot-0.7.9.tar
 $ ls
  DEXBot-0.7.9 
  DEXBot-0.7.9.tar

 $ python3 -m venv env
 $ source env/bin/activate
 (env)$ cd DEXBot-0.7.9
```
想进一步了解virtualenv吗？请看：https://realphython.com/python-virtual-environments-a-primer/
从dexbot目录中，将以下命令一次复制并粘贴到终端中一行，然后按Enter键。不要复制$-符号，因为它只表示您以普通用户而不是超级用户的身份运行该命令。
一定要添加到您的路径：~/library/python/3.6/bin/，因为这是安装dexbot gui和cli的地方。
```
$ cd DEXBot-0.7.9
$ make check 
$ pip install --upgrade pip (if needed) 
$ git clone https://github.com/Codaone/DEXBot.git dexbot
$ cd dexbot   
$ make install-user
$ dexbot-gui or dexbot-cli
```
如果运行make install user时出现错误，并且错误消息显示：
```
TEST FAILED: /Users/<>/Library/Python/3.7/lib/python/site-packages/ does NOT support .pth files error: bad install directory or PYTHONPATH
```
然后需要复制并粘贴到命令行中：
```
$export PYTHONPATH=/Users/<<YOUR USERNAME>>/Library/Python/3.7/lib/python/site-packages/
```

然后检查export是否有效：确保用安装程序建议的路径替换上面的路径。
`$ echo $PYTHONPATH` 应该返回如下链接：
`/Users/<>/Library/Python/3.7/lib/python/site-packages/`
再次运行:`$ make install-user`
如果您只需要不带gui的CLI版本（它将在更多系统上工作),运行如下命令：
`pip3 install --user -e .`(包括.)
##故障排除

如果您在构建方面有问题，那么可能存在环境问题。也许您需要考虑使用虚拟env。以下是您需要做的：
在与下载的源代码相同的顶级目录中
如果在DexBot GUI启动时出错：ssl:certificate_verify_failed with python3:
转到安装python的文件夹，例如，在我的示例中，它安装在文件夹名为“python 3.6”的应用程序文件夹中。现在双击“install certificates.command”。
##以下在Macos Sierra 10.12.6上测试
（Sierra with python version 3.6.3 with openssl 0.9.8zh 14 Jan 2016）

###安装
1.打开终端
首先，确保从https://python.org安装了python3版本。此安装将不适用于默认的python版本2
将以下命令一次一行地复制并粘贴到终端中，然后按Enter键。不要复制$-符号，因为它只表示您以普通用户而不是超级用户的身份运行该命令。
```
$ make check 
$ pip install --upgrade pip (if needed) 
$ git clone https://github.com/Codaone/DEXBot.git dexbot
$ cd dexbot   
$ make install-user
```
如果您只需要不带gui的CLI版本,运行如下命令：
`pip3 install --user -e .`(包括.)