---
title: Hello，MacOS
date: 2023-11-07 23:23:28
tags:
  - tech
  - mac
  - finder
  - hello
draft: false
hideInList: false
feature: 
isTop: false
---

 # Finder

找出 当前文件夹或子目录下面所有的  pdf 文件并拷贝放到pdf文件夹下面
```
find ./  -name  "*.pdf" -exec mv {} ./pdf \;
```


## 剪切
其实访达中也可以实现剪切功能，只不过剪切的行为不是发生在开始，而是发生在粘贴时。

按下`command+C`快捷键之后，在目标目录按下`option+command+V`就可以将刚才复制的文件和目录移动到目标目录，即实现了剪切功能。





## [PopClip](https://github.com/tisfeng/Easydict/blob/main/README.md) 


开启 easydict。你需要先安装 [PopClip](https://pilotmoon.com/popclip/)，然后选中以下代码块，`PopClip` 会显示 "安装扩展 Easydict"，点击它即可。（By **[liziqiang](https://github.com/liziqiang)**）

```shell
# popclip
name: Easydict
icon: iconify:ri:translate
interpreter: zsh
shell script: |
  result=$(ps aux | grep Easydict.app | wc -l)
  if [[ $result -lt 2 ]];then
    open /Applications/Easydict.app
    sleep 2
  fi
  open "easydict://query?text=$POPCLIP_TEXT"
```

> 参考：[https://www.popclip.app/dev/shell-script-actions](https://www.popclip.app/dev/shell-script-actions)


<!--more-->