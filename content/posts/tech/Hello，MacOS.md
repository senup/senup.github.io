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

找出 顶层文件夹 下所有的 m4a 文件并拷贝放到mp3 文件夹下面
```
find 顶层文件夹/  -name  "*.m4a" -exec mv {} 顶层文件夹/mp3 \;
```

<!--more-->