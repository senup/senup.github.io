---
title: Hello，Spring
date: 2023-11-20T12:51:42
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

这个 resolver 有什么用？XML 的配置文件头经常会引用 dtd 和 xsd 的校验规则，但是存在一个问题，就是使用的时候需要去网络下载，如果网络出现问题就会影响整个流程。为此，spring 把这些校验文件都放在 jar 包里面了，需要的时候就会从 jar 包加载成 bean 出来，而 resolver 就是用于规范和校验 XML 格式的类。

至此，流程图为这样。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311182349751.png)


上图中底部俩 resolver 分别规范和校验 dtd 和 xsd 的校验格式；
- Dtd 的 resolver 会有两个入参：publicId 和 systemId。SystemId 是 XML 文件里面的一个 HTTP 链接。怎么根据这俩参数获取具体的位置? 首先构建 classPathResource 的时候 getClass 方法传入了 BeansDtdResolver 的相对应的 resources 文件夹下面就有 dtd 文件。文件名是默认的 spring-beans. Dtd。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311190052326.png)

- xsd 文件也有 publicId 和 systemId。不太相同的地方在于不需要 publicId 。其查找过程是将 “META-INF/spring. Schemas”文件解析成一个 map <systemId,xsd 路径>的结构，然后通过当前 XML 文件里面的 systemId 获取到对应的 xsd 路径，也能找到。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311190057718.png)

区别是哪种类型？XML 中引用的校验文件只有 dtd 和 xsd, 因此一旦发现 xml 里面包含了“DOCTYPE”字符串，那么就是 dtd 格式的校验规则，否则就是 xsd.


 XML区别如图：
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311190102960.png)
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311190103948.png)

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311190103273.png)


能加载校验文件后，就会开始对文件进行一步步解析。这里关注的是 spring 会拿到 document，然后遍历去解析节点。在执行解析的时候，会将具体工作交给一个代理类 delegate，代理类会针对 document 的每一个节点，区别是默认标签还是自定义标签，这一步是通过判断 namespace URI 判断的，默认链接如下图。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311192014968.png)

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311192015745.png)

---

### bean 初步解析

解析到一个标签的时候，会有四个 if 判断标签属性是 Bean、beans、alias、import。后两个如今在 XML 用得少了，重点放在前两个上面。

假设判断是 bean 标签，那么就开始解析标签属性，比如 Id 和 name 直接解析出来，name 因为是由逗号拼接而成，所以这里需要对字符串切割后放进一个数组里面...... 接下来，开始初步放进 beanDefinition 接口的实现类里面，用于存放标签解析结果。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311192021344.png)

### BeanDefinition
BeanDefinition 是一个接口，用于封装 bean 的信息。他的继承关系如下：
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311192041677.png)

如图自上而下，左侧先被一个抽象类继承，其下还有三个具体的实现类，其中 rootBeanDefinition 代表只有单个的 XML 标签，不能含有 parent 属性；而 childBeanDefinition 代表拥有 parent 属性的标签。这两种是早期的 spring 版本用的，目前用的多的是通用的 genericBeanDefinition。

右侧分支是一路走注解的实现。

### 子标签解析
spring 会罗列出可能的所有子标签，然后每种子标签就写一个方法，只要判断标签的 key 匹配，就会走流程：解析出每一个键值对，然后放进 beanXXXAttribute 或者 BeanDefinition 中。
这个过程十分复杂繁琐，可能需要避免 property 重名、description 和 meta 等标签剔除不处理等。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311192058014.png)



### Bean 注册

BeanDefinitionHolder 可以封装 BeanDefinition 和别名 aliasArray。

spring 容器也就是 BeanDefinitionMap，注入容器就是相当于拿着 holder 里面的 beanName 和 BeanDefinition 往 map 里面添加。如果同名则覆盖，默认是支持覆盖的。之后若发现之前的 Bean 容器有这个 Bean 或者这个已经根据 beanDefinition 创建出了对象，那么就会对 Bean 的缓存进行重置，我猜这里是为了及时性。

之前注入 Bean 是往 map<name,BeanDefinition>添加，现在别名注入是往 map<alias,beanName>这个里面添加。并且，如果打算要注册的别名key已经在 map 里面存在了，那么就不再注册了。
如果打算注册的别名 key 和 value 不同，但是 map 里面已存在这个键值对，且这个时候不允许覆盖，那么这个时候就会抛异常。

别名可能会有循环，所以会有个循环检测。相当于同时存在：alias 1 到 name 1，alias 1 到 name 2，name 2 再到 name 1 这两个关系，出现了两个起点和重点都相同的循环了，这样就造成了别名循环的问题就会抛异常。

- [ ] <span style="background:#fff88f">理清为什么别名循环不允许存在</span>


补充：创建 Bean 的时候只能使用 spring 普通的方式创建，或者使用工厂方法来创建，两者如果都有，那么这个时候就会抛出异常。


![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311200034697.png)

## ApplicationContext
理清了 xmlBeanFactory, 接下来看一个功能更全的类——ClassPathXmlApplicationContext。它也是 ApplicationContext 的一个具体实现类。

1. 简单来使用一下 ApplicationContext，作源码分析的入口
2. 接下来再来看下 ApplicationContext 对环境变量以及路径占位符解析的准备工作
3. 最后再来定位下 ApplicationContext 中，最核心的方法是在什么位置，为下一步的源码分析做准备


![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201413240.png)

- 父类构造方法设置了成员变量 parent
- 支持传入多个 configLocations，同时支持使用占位符来对 placeHolder 进行解析，如果找不到占位符那么就报错
- Refresh 默认为 true 
- refresh 方法是核心方法。

- [ ] Refresh 待验证

### prepareFefresh 初始化上下文信息
提供一个拓展方法方便在上下文环境中解析参数占位符。

使用方法：提前设置占位符的键值对，方便后续操作直接使用占位符的键即可找到。比如使用“$｛username｝”。


```
Public class NewClassPathXmlApplicationContext extends ClassPathXmlApplicationContext ｛
Public NewClassPathXmlApplicationContext（String... ConfigLocations） ｛
Super（configLocations）；
｝

@Override
Protected void initPropertySources（）｛
System. Out. PrintIn（"重写 initPropertySource 方法."）；
getEnvironment（）. setSystemPropenties（）. Put（"username”，"zhangsan"）；
｝
｝
```

接下来就会校验必要的环境变量值是否为空，如果为空则报错。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201432263.png)


### 初始化容器 beanFactory

首先调用了获得并刷新 Bean 工厂的 obtainFreshBeanFactory 方法，返回了一个 ConfigurableListableBeanFactory。这个是继承 BeanFactory 的一个接口。具体可以看下下方的继承关系图。

ObtainFreshBeanFactory 如它的名字一样，就是包含了刷新和获取的方法。刷新的方法在前，也是重点关注的部分。刷新的 refreshBeanFactory 方法会判断 BeanFactory 是否存在，如果存在，那么就会销毁所有的 Bean，再销毁关闭 Bean 工厂，然后走新增 BeanFactory 的逻辑。

新增 BeanFactory：首先创建一个初级的 Bean 容器，DefaultListableBeanFactory，这个是 XMLBeanFactory 的父类。然后提供了一个 customize 的客制化方法，这里提供了两个拓展方法。

- 是否允许同名的 BeanDefinition 在容器 beanDefinitionMap 中被覆盖
- 是否允许存在循环依赖

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201516076.png)

接下来，有了初始的 Bean 容器，那么就会开始解析资源。
中间提供了一个去拓展 reader 的方法。


然后，applicationContext 允许传入多个字符串，因此会遍历字符串数组去解析每一个路径。有了 BeanFactory，就能作为参数传给 reader，reader 就能读取路径，路径就能获得 resource，根据 resource 加载对应的 document 对象，解析对象，再解析 XML 中的各种标签属性，将得到的属性和方法信息封装在 beanDefinition 中，最后注册到 Bean 容器 beanDefinitionMap 中。


![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201514650.png)


![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201448356.png)


到此，需要记住一点就是，spring 源码中出现 protected 修饰的方法，一般都是客制化的拓展方法。

- [ ] 罗列出拓展接口并进行最佳实践

### prepareBeanFactory

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201531517.png)

拓展点：
- 第二步设置了 spel 表达式的解析器，全称就是 spring expression language。用于解析比如 XML 里面的一些#{}，当然，这些变量可以放在一个统一的文件中集中管理。
- 第三步添加了很多属性编辑器，这个主要是因为 XML 的局限所致的。比如 XML 有些属性的值是字符串，但是使用到的时候就都需要转化成各种 stream 使用，因此这里就提供了各种各样的属性编辑器。
- 第四步添加了各种 aware 接口的后处理器。如果判断不是这些接口，那么就会直接返回当前的 Bean。否则，就会执行实现了这些 aware 感知接口的方法去修改 Bean。这里拓展的是后置处理器的前置处理。
- 第五步添加需要忽略的感知接口，<span style="background:#fff88f">简单来说，如果一个 bean 实现了传入 ignoreDependencyInterface 方法的这些感知接口，Spring 是不允许外界注入任何的依赖到 bean 中的，只允许 Spring 容器内部调用感知接口的方法来注入相应的依赖。</span>
- 第六步添加接口指定的依赖。这个东西就是说获取这几个 Bean 的时候，可能会找 Bean 对应的一个实现类。假设这个时候自己写了一个实现类，但是 spring 获取 Bean 的时候还是按照它内部自己生成的这个 Bean 提供给你而不是使用我自己写的实现类，为了确保这些关键的接口，它的实现类只能是 spring 内部指定的一些对象。




![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201551755.png)

### PostProcessBeanFactory
那方法 postProcessBeanFactory 留给子类具体是要去实现什么样的功能呢？通过方法的注释我们可以知道，方法 postProcessBeanFactory 是 Spring 暴露给子类去修改容器 beanFactory 的。
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201615884.png)


### BeanFactoryPostProcessor
可以看到，BeanFactoryPostProcessor 中的方法和我们刚才看到的空实现方法 postProcessBeanFactory 几乎是一模一样的，目的也是一样的，也就是给了我们一次机会，允许我们通过参数 beanFactory 去获取相应的BeanDefinition 并修改相应的信息。
![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201616556.png)

- [ ] 上面这两个东西有什么区别？

### BeanFactoryPostProcessor 的执行顺序

首先，明确有两种 PostProcessor：一种是 regular 普通的，一种是 registry 注册类的。从这儿可以了解到 Bean 除了常规解析 XML 得来的，还可以自定义 beanDefinition，然后走 register 的接口注册到容器里面。

然后，按照是否是注册类来将两种类型的 postProcessor 分类到两个数组里面。

接下来找个 currentRegisterProcessors 的数组。用来存放数量众多的一批 register 且同时实现了 priority 接口的 Bean 。收集完对数组进行优先级的排序，越小的优先级越排前面，然后添加到 registryProcessors 的数组里面，开始实现 beanDefinition 的 postProcessor，清空 currentRegisterProcessors，接着循环去整下一轮。


第二轮处理的是属于 registry 且实现类 ordered 接口的 Bean，具体方式同上。

第三轮会讲前两轮剩下的属于 registry 的Bean 做处理，方式也同上。

最终，对两种 PostProcessor 分别执行了后处理器的方法来修改 beanDefinition。

上面这个过程适用于参数、容器的 registry、容器的普通 processor 三种，情况还是较多的。

![image.png](https://bestkxt.oss-cn-guangzhou.aliyuncs.com/img/202311201716119.png)



### BeanPostProcessor
