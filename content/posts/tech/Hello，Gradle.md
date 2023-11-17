---
title: Hello，Gradle
date: 2023-11-17 18:05:10
tags:
  - tech
  - hello
  - gradle
draft: false
hideInList: false
feature: 
isTop: false
---
## 下载

[gradle官方网站](https://gradle.org/install/#manually)

点击上方连接进入到官方网

手动安装的话，点击releases page 选择自己想要安装的包下载

我安装的是6.5，选择binary-only下载，下载好了之后解压放在自己想要放的位置，我这里放在的是/Users/butcher/code/tools/gradle-6.5/bin

## 配置环境变量

1.通过命令打开环境编辑文档，输入i进入编辑模式

`vim ~/.bash_profile`

2.在文档的尾部追加gradle的环境配置

`export PATH=$PATH:/Users/butcher/code/tools/gradle-6.5/bin

英文状态下，按esc键，然后输入`:wq`保存并退出文档

3.让配置的文档生效

`source ~/.bash_profile`

4.验证gradle安装成功

`gradle -v`

出现gradle的版本信息证明安装成功。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311171858040.png)



<!--more-->

## idea 配置
