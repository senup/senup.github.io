---
doc_type: weread-highlights-reviews
bookId: "730634"
author: 郝佳编著
cover: https://wfqqreader-1252317822.image.myqcloud.com/cover/634/730634/t7_730634.jpg
reviewCount: 1
noteCount: 1
isbn: 9787115325686
category: 计算机-计算机综合
lastReadDate: 2021-09-13
---
# 元数据
> [!abstract] Spring源码深度解析
> - ![ Spring源码深度解析|200](https://wfqqreader-1252317822.image.myqcloud.com/cover/634/730634/t7_730634.jpg)
> - 书名： Spring源码深度解析
> - 作者： 郝佳编著
> - 简介： 　　《Spring源码深度解析》从核心实现和企业应用两个方面，由浅入深、由易到难地对Spring源码展开了系统的讲解，包括Spring的设计理念和整体架构、容器的基本实现、默认标签的解析、自定义标签的解析、bean的加载、容器的功能扩展、AOP、数据库连接JDBC、整合MyBatis、事务、SpringMVC、远程服务、Spring消息服务等内容。
　　《Spring源码深度解析》不仅介绍了使用Spring框架开发项目必须掌握的核心概念，还指导读者如何使用Spring框架编写企业级应用，并针对在编写代码的过程中如何优化代码、如何使得代码高效给出切实可行的建议，从而帮助读者全面提升实战能力。
　　《Spring源码深度解析》语言简洁，示例丰富，可帮助读者迅速掌握使用Spring进行开发所需的各种技能。《Spring源码深度解析》适合于已具有一定Java编程基础的读者，以及在Java平台下进行各类软件开发的开发人员、测试人员等。
> - 出版时间 2013-09-01 00:00:00
> - ISBN： 9787115325686
> - 分类： 计算机-计算机综合
> - 出版社： 人民邮电出版社

# 高亮划线

## 第2章 容器的基本实现


- 📌 自动装配时忽略给定的依赖接口，典型应用是通过其他方式解析Application上下文注册依赖，类似于BeanFactory通过BeanFactoryAware进行注入或者ApplicationContext通过ApplicationContextAware进行注入。 ^730634-6-16814-16947
    - ⏱ 2021-09-13 17:47:18 
# 读书笔记

## 第2章 容器的基本实现

### 划线评论
- 📌 ● src/main/java用于展现Spring的主要逻辑。
● src/main/resources用于存放系统的配置文件。
● src/test/java用于对主要逻辑进行单元测试。
● src/test/resources用于存放测试用的配置文件。
2.4.2 核心类介绍
通过beans工程的结构介绍，我们现在对beans的工程结构有了初步的认识，但是在正式开始源码分析之前，有必要了解一下Spring中最核心的两个类。
1.DefaultListableBeanFactory
XmlBeanFactory继承自DefaultListableBeanFactory，而DefaultListableBeanFactory是整个bean加载的核心部分，是Spring注册及加载bean的默认实现，而对于XmlBeanFactory与DefaultListableBeanFactory不同的地方其实是在XmlBeanFactory中使用了自定义的XML读取器XmlBeanDefinitionReader，实现了个性化的BeanDefinitionReader读取，DefaultListableBeanFactory继承了AbstractAutowireCapableBeanFactory并实现了ConfigurableListableBeanFactory以及BeanDefinitionRegistry接口。  ^29927260-7thT6CIFX
    - 💭 默认的 beanFactory 实现了配置 bean 工厂和 bean 定义注册的接口
    - ⏱ 2021-09-13 17:00:52
   
# 本书评论
