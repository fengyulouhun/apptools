Android多渠道打包工具
========

支持跨平台、命令行、多渠道、多平台

1. 环境设置保证apktool运行正常
========
可参考官方项目：https://code.google.com/p/android-apktool/

2.打包流程
========
1.设置当前process 的环境变量，保证 apktool 可以正常工作<br />
2.执行 apktool d --no-src -f xxxx.apk temp 拆解apk<br />
3.替换 AndroidManifest.xml 中的 channelFlag字符为指定渠道<br />
4.执行 apktool b temp unsigned.apk 重新打包apk<br />
5.执行 jarsigner 生成签名后的 apk 文件<br />
6.执行 zipAlign 生成对齐优化后的 apk 文件<br />
7.回到 3 替换新的渠道<br />
8.完成打包<br />


3.工程目录结构
========
源码形式：<br />

> ├apktool<br />
> &nbsp;&nbsp;├src<br />
> &nbsp;&nbsp;├bin<br />
> &nbsp;&nbsp;├.classpath<br />
> &nbsp;&nbsp;├.project<br />
> &nbsp;&nbsp;├linux<br />
> &nbsp;&nbsp;├macosx<br />
> &nbsp;&nbsp;├windows<br />
> &nbsp;&nbsp;├map.properties<br />
 
命令行形式：<br />
> ├pro java -jar xxx.jar<br />
> &nbsp;&nbsp;├xxx.jar<br />
> &nbsp;&nbsp;├linux<br />
> &nbsp;&nbsp;├macosx<br />
> &nbsp;&nbsp;├windows<br />
> &nbsp;&nbsp;├map.properties<br />


4.使用教程
========
1.配置map.properties<br />
2.更改自己要打包项目的AndroidManifest.xml(可参考apps demo)中的渠道号字符替换为map.properties中配置的channelFlag
指定字符 打好包后放到map.properties配置的指定路径<br />
3.直接源码eclipse中右键运行打包工具<br />
4.可打jar包命令行运行打包工具<br />

5.注意事项
========
1.如果您的电脑以前使用过apktool工具请删除工具生成老的framework.jar 路径(windows平台):
c:\Documents and Settings\%current user%\apktool\framework\*

2.请保证java与android环境变量不存在空格，如有请在代码执行命令前直接写上路径后运行比如：
D:\android-sdk-windows\tools\zipalign

3.不支持Java jar包中包含有资源文件的apk项目，受apktool工具本身功能限制(如有jar包源码，可尝试把jar中的资源文件放进assets使用Android函数加载)
