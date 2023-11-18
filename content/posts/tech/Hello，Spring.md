---
title: Hello，Spring
date: 2023-11-18 12:51:42
tags:
  - tech
  - hello
  - spring
  - Java
draft: true
hideInList: false
feature: 
isTop: false
---


## Resource
Resource 是对各种文件资源的一个抽象接口，包含了判断文件是否存在、是否可读、是否属于文件类型、是否可打开等抽象方法。

resource 还继承了 inputStreamSource，inputStreamSource 接口有一个 getInputStream 的方法，所以理论上所有资源类都能轻松获取对应的输入流。

> 那么，获得输入流之后会有一个 XML 的 bean factory 去做，怎么才能变成 bean 呢？ 为什么要忽略感知接口？感知接口是什么？构造器第二个参数的 parentBeanFactory 有什么用？指定 bean 工厂？



## xmlBeanFactory

### 父类方法
拿一个例子来说说 beanNameAware 的用处，就是构造 bean 的时候手动注入 bean 的名称。也就是说感知接口是在自动装配 bean 的时候方便开发者注入需要的内容。

比如student 实现了 beanNameAware 的接口，然后重写 setBeanName 方法，在里面打了一行 sout: 当前 beanName 是 $name。现在，在 main 函数 getBean("李四")，得到的结果就是会打印一句「当前 beanName 是李四」。

但是这里面 spring 做了一个限制。他会把三个感知接口放在一个 set 里面，然后判断当前类是否实现了其中某个接口+类某个属性存在相同的重写方法，如果有，那么自动装配创建 bean 的时候就不会注入值。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311181342195.png)

<!--more-->

比如下面这个例子，刻意满足了两个条件，实现了 beanNameAware 接口+存在同名的 setBeanName 方法，name 这个时候就不会注入属性值。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311181339671.png)

为什么要做这种限制呢？我理解 spring 是为了确保类属性值的 setter 方法和感知接口的重写方法重名的时候，优先级肯定是当前类属性值优先，防止外部注入来改变，确保了 bean 名称的唯一性。同时，确保只能由内部接口注入，不能由外部的 XML 来变更。

---

### reader 加载 beanDefinition
上面一步是继承父类在某些情况要忽略感知接口。这一步是将传进来的 resource 类添加编码，转化成输入流，再对流做处理，正式开始加载 beanDefinition。

目前的路径：XML 文件->resource->inputStream-><span style="background:#d3f8b6">document->beanDefinition</span>❓

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311181409602.png)


### 解析成 document

文件流最终转化成了内存中的数据结构，这一步可以了解到 DOM 是如何解析的。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311181444338.png)


### document 前置的 entitySolver
注意到上面的第二个参数传入了 entitySovler，发现他是单纯通过 get 方法无参获取的。实际是 xmlBeanDefinitionReader 的父类初始化的时候传进来了一个 xmlBeanDefinitionReader.register，这个 register 不属于 resourceLoader，因此被赋予了 PathMatchingResourcePatternResolver。因此不为空，所以下图这里获取到的 resolver 是第一个。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311181457611.png)
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311181510070.png)

