---
title: Hello，shellclash
date: 2023-11-12 01:17:06
tags:
  - life
  - vpn
draft: false
hideInList: false
feature: 
isTop: false
---
> shellclash刷入路由器后，可以实现节点代理、节点分流等功能，让家中所有联网设备共享代理后的节点，十分方便。
# 环境配置
路由器：红米ax6000
固件：官方固件

红米ax6000可以直接在官方固件的基础上解锁ssh,然后在termius上连接并下载shellclash。

其中作者给出的下载链接有三个，如果遇到下载失败的时候可以反复重试，或者尝试切换脚本和核心重试即可。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311120120164.png)
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311120121640.png)
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311120124891.png)


# 界面讲解
代理界面有selector和URLTest的两种类型。
selector代表节点组汇总，URLTest代表单个节点组下面的所有节点。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311120126445.png)
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311120127617.png)


# 使用场景
比如spotify free 账号档案使用的是香港地区，那么家里的Apple tv设备就默认要使用代理里面的香港节点，我们从上图连接菜单下可以看到目前spotify使用的是国外媒体这个节点链，那么就在代理菜单下面的国外媒体选择香港节点组。

同时，iPhone可以平时就挂着Quantumult X+蜂窝流量使用，这样IP地址归属于香港，spotify就能在离开了shellclash后独立使用，不会报14天离开归属地的弹窗从而登录不了。

<!--more-->