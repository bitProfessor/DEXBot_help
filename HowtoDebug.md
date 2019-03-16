# 如何调试
## DEXBot日志
默认情况下，dexbot使用信息级日志记录。您可以查看dexbot.log文件，参见文件位置。
##如何调试dexbot
当在dexbot执行期间出现错误时，通常需要在bugreport中提供调试日志。要提供基本级别的调试，需要使用以下命令在CLI模式下运行dexbot：

`dexbot-cli -v4 run`

-v4开关提升日志级别到debug。
##调试级别
- 1-4: dexbot only
- 5-8: debug grapheneapi (python-graphenelib library)
- 9-13: debug graphenebase (python-graphenelib library)