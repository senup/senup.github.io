---
title: Hello，MacOS
date: 2023-11-07 23:23:28
tags:
  - tech
  - mac
  - finder
  - hello
draft: true
hideInList: false
feature: 
isTop: false
---

 # Finder

找出 当前文件夹或子目录下面所有的  pdf 文件并拷贝放到pdf文件夹下面
```
find ./  -name  "*.pdf" -exec mv {} ./pdf \;
```

<!--more-->