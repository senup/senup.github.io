---
title: Hello，Quantumult X
date: 2023-11-11 23:13:43
tags:
  - tech
  - vpn
draft: false
hideInList: false
feature: 
isTop: false
---

> Quantumult X 是一款VPN软件，因为有分流和重写的功能，所以既能翻墙，也能实现广告过滤、VIP伪装等强大功能。

# 下载配置
推荐墨鱼配置，常用 APP 去广告都有规则，而且更新也比较勤快。  
[https://github.com/ddgksf2013](https://github.com/ddgksf2013)  

![IMG_1860.jpg](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311112340370.jpg)
![IMG_1859.jpg](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311112341041.jpg)


# 重写规则
有些小众 APP 再从这个组里面找需要的 APP 规则：  
[https://t.me/Aa28413761](https://t.me/Aa28413761)

![IMG_1857.jpg](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311112339518.jpg)

![IMG_1858.jpg](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311112338375.jpg)


# 导入节点订阅
目前用的是魔戒，按量订阅，缺点是偏慢

# 配置证书
打开设置的MitM开关，生成证书并去设置里面配置证书
![IMG_1861.jpg](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311112337506.jpg)




<!--more-->
# 重写规则配置

```bash
# 🟢>>>>>>>>功能重写<<<<<<<<<<<<<<<<<<
[rewrite_remote]
https://raw.githubusercontent.com/ddgksf2013/Rewrite/master/AdBlock/Netease.conf, tag=网易云音乐, update-interval=172800, opt-parser=false, enabled=true
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/script/zheye/zheye.snippet, tag=知乎新版, update-interval=172800, opt-parser=false, enabled=true
https://raw.githubusercontent.com/WeiRen0/Scripts/main/wyun.js, tag=by-伟人,网易云音乐, update-interval=172800, opt-parser=true, enabled=false
https://raw.githubusercontent.com/ddgksf2013/Rewrite/master/AdBlock/StartUp.conf, tag=去开屏, update-interval=172800, opt-parser=false, enabled=true
https://raw.githubusercontent.com/senup/QuantX/main/rule.conf, tag=个人配置, update-interval=172800, opt-parser=true, enabled=false
https://raw.githubusercontent.com/zwf234/rules/master/QuantumultX/qxrules.conf, tag=齐心规则, update-interval=172800, opt-parser=true, enabled=false

https://raw.githubusercontent.com/Moli-X/Resources/main/Rewrite/Collections.conf, tag=𝑪𝒐𝒍𝒍𝒆𝒄𝒕𝒊𝒐𝒏𝒔, update-interval=172800, opt-parser=true, inserted-resource=true, enabled=false
https://raw.githubusercontent.com/RuCu6/QuanX/main/Rewrites/Cube/amap.snippet, tag=高德净化, update-interval=172800, opt-parser=false, inserted-resource=true, enabled=true
https://raw.githubusercontent.com/Moli-X/Resources/main/Script/Bilibili/AD_Bilibili.conf, tag=哔哩广告, update-interval=172800, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/Cainiao.conf, tag=菜鸟裹裹, update-interval=172800, opt-parser=true, enabled=false
https://raw.githubusercontent.com/Moli-X/Resources/main/Rewrite/XHS.conf, tag=小红书, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/Moli-X/Resources/main/Rewrite/Search.conf, tag=超级搜索, update-interval=172800, opt-parser=true, enabled=false
https://raw.githubusercontent.com/Moli-X/Resources/main/Rewrite/ADBlock.conf, tag=ADBlock, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/Moli-X/Resources/main/Rewrite/TikTok/TikTok-US.conf, tag=𝑻𝒊𝒌𝑻𝒐𝒌, update-interval=86400, opt-parser=true, enabled=false
https://raw.githubusercontent.com/app2smile/rules/master/module/youtube.sgmodule, tag=油管广告, update-interval=172800, opt-parser=true, enabled=false
https://raw.githubusercontent.com/Maasea/sgmodule/master/YoutubeAds.sgmodule, tag=油管画中画, update-interval=172800, opt-parser=true, enabled=false
https://raw.githubusercontent.com/WeiRen0/Scripts/main/ZHVIP.js, tag=知乎会员, update-interval=172800, opt-parser=true, enabled=false
https://raw.githubusercontent.com/WeiRen0/Scripts/main/wxds.js, tag=微信读书, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/Moli-X/Resources/main/Rewrite/Cookie.conf, tag=Cookie, update-interval=172800, opt-parser=true, enabled=false

# ======================================
# https://gitlab.com/ioshkj/quantumultx/-/raw/main/vipjs/ylgy.conf, tag=𝑺𝒉𝒆𝒆𝒑, update-interval=172800, opt-parser=true, enabled=false
# https://raw.githubusercontent.com/zwf234/rules/master/QuantumultX/price.conf, tag=京东淘宝比价, update-interval=172800, opt-parser=true, enabled=true
# https://raw.githubusercontent.com/NobyDa/Script/master/QuantumultX/TestFlightDownload.conf , tag=TestFlight区域限制解除, update-interval=172800, opt-parser=false, enabled=true
# https://raw.githubusercontent.com/zZPiglet/Task/master/UnblockURLinWeChat.conf, tag=微信跳过中间界面, update-interval=172800, opt-parser=true, enabled=true
# https://raw.githubusercontent.com/yqc007/QuantumultX/master/DuolingoPlusCrack.js, tag=𝑫𝒖𝒐𝒍𝒊𝒏𝒈𝒐, update-interval=172800, opt-parser=true, enabled=true
# https://raw.githubusercontent.com/Moli-X/Resources/main/Rewrite/Bilibili/AutoBilibili.conf, tag=哔哩换区, update-interval=172800, opt-parser=false, enabled=true
# ======================================
```



# 本地任务配置
可以参考[圈x脚本 - 菜鸟辉哥](https://www.cnblogs.com/zh76412950/p/17207805.html)讲了**本地任务**和**抓包**的使用
相关脚本可以参考[Telegram: Contact @nobyda](https://t.me/nobyda)
```bash
# 🟢>>>>>>>>>>>本地任务<<<<<<<<<<<<<<<<<
[task_local]
# ===============莫离收集===============
0 36 6,14,23 * * * https://raw.githubusercontent.com/chouchoui/QuanX/master/Scripts/testflight/Auto_join_TF.js, tag=TestFlight自动加入, img-url=https://raw.githubusercontent.com/Orz-3/mini/master/Color/testflight.png, enabled=false
0 36 6,14,23 * * * https://raw.githubusercontent.com/dompling/Script/master/jd/jd_cookie_search.js, tag=京东检测, img-url=https://raw.githubusercontent.com/FoKit/Quantumult-X/main/images/check.png, enabled=false
30 7,11,15,19 * * * https://raw.githubusercontent.com/id77/QuantumultX/master/task/jdWuLiu.js, tag=京东物流, img-url=https://raw.githubusercontent.com/NobyDa/mini/master/Color/jd.png, enabled=false
30 18,20 * * * https://raw.githubusercontent.com/ChuheGit/1/main/Script/jd_scripts/jd_unsubscribe.js, tag=京东取关, img-url=https://raw.githubusercontent.com/NobyDa/mini/master/Color/jd.png, enabled=false
30 8,12,16,20 * * * https://raw.githubusercontent.com/ChuheGit/1/main/Script/jd_scripts/jd_bean_change.js, tag=京豆变动, img-url=https://raw.githubusercontent.com/ChuheGit/1/main/QuantumultX/Gallery/API-Icon/jd_bean_change.png, enabled=false
0 0 1 5 * https://raw.githubusercontent.com/WSL33099/QuantumultX/main/Script/JD/ClCart.js, tag=清空购物车, img-url=https://raw.githubusercontent.com/Orz-3/mini/master/Color/jd.png, enabled=false
5 0 * * * https://raw.githubusercontent.com/NobyDa/Script/master/JD-DailyBonus/JD_DailyBonus.js, tag=京东签到, img-url=https://raw.githubusercontent.com/NobyDa/mini/master/Color/jd.png, enabled=false
30 7-22 * * * https://raw.githubusercontent.com/evilbutcher/Quantumult_X/master/check_in/appstore/AppMonitor.js, tag=软件监控, img-url=https://raw.githubusercontent.com/WSL33099/QuantumultX/main/Icon/Test/App-Store.PNG, enabled=false
```





 # 参考
 [GitHub - kjfx/QuantumultX: Quantumult X 新手入门教程](https://github.com/kjfx/QuantumultX/)
 [Quantumult实现京东签到](https://www.youtube.com/watch?v=QUNzXesYMOo)
 [Quantumult X 不完全教程](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917)