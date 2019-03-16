checklist

- 创建worker是否使用了私人密钥，而不是钱包密码？

- 你对每个worker都使用单独的帐户吗?

- 您是否用前缀（bridge.ltc、open.eth、bts、usd、stealth等）编写了整个资产名称？

- 你确定这个账户持有待交易的两种资产吗?

- 是否切换“打开/关闭工人”按钮使工人实际工作？

- 你的电脑时钟同步了吗?

1. 时钟问题
如果在错误消息末尾收到以下消息：
bitsharesapi.exceptions.unhandledrpcerror:断言异常：现在<=trx.expiration

同步计算机时钟。修正错误。

2. Signature / key problems
base58CheckDecode
尝试使用以下命令升级python加密包：pip3 install --upgrade cryptography 并再次运行

3. 如果您看到同一帐户的多个私钥有错误，则需要清空钱包。首先删除所有工人。然后运行uptick wipewallet。现在应该没有钱包和钥匙了。从零开始。

4. 升级和安装问题

5. 石墨烯问题

- attributeError:无法设置属性
通过指定graphenelib版本进行修复：pip3 install graphenelib==0.6.2
- Ubuntu 18.04，18.10 Linux-AES，安装命令：make install -user 出错：
>scrypt-1.2.1/libcperciva/crypto/crypto_aes.c:6:10: fatal error: openssl/aes.h: No such file or directory
 #include <openssl/aes.h>
          ^~~~~~~~~~~~~~~
这主要是由于Ubuntu系统找不到scrypt包，sudo apt get install libssl dev可以很容易地修复这个包。

另请参阅steemit安装问题的类似解决方案

- 用make install-user 命令安装出错：
Best match: PyYAML 4.2b4
Processing PyYAML-4.2b4.tar.gz
Writing /tmp/easy_install-fccfyzzf/PyYAML-4.2b4/setup.cfg
Running PyYAML-4.2b4/setup.py -q bdist_egg --dist-dir /tmp/easy_install-fccfyzzf/PyYAML-4.2b4/egg-dist-tmp-bunv4mwn
In file included from ext/_yaml.c:565:0:
ext/_yaml.h:2:10: fatal error: yaml.h: No such file or directory
 #include <yaml.h>
          ^~~~~~~~
compilation terminated.
Error compiling module, falling back to pure Python

修复：pip3 install pyyaml 安装 pyyaml-3.13
-  No such file or directory: 'pyuic5': 'pyuic5'
This means that 'pyuic5' is not in your PATH for some reason. Solution: find where 'pyuic5' is and add it into PATH:

export PATH=~/.local/bin:$PATH
Order placement takes 5 minutes
Uninstall and install scrypt with pip3 uninstall scrypt and pip3 --user install scrypt

Node connection problems
Possible error messages:

socket is already closed


修复：更改config.yml中定义的节点。在下面找到文件位置，查看哪个节点在DEX中的延迟最小，并将其复制到配置文件中。



- DexBot GUI冻结，未创建订单
重新启动bot
- 未知订单类型
在 BTS:MPA（锚定资产，如bitsusd和bitcy）市场中，如果出现爆仓单，DexBot不能识别它，因为它不确定发生了什么。修复这个问题，只需暂停->启用或重新启动整个dexbot GUI。