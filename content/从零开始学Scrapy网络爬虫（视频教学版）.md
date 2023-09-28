---
doc_type: weread-highlights-reviews
bookId: "26391341"
author: 张涛
cover: https://wfqqreader-1252317822.image.myqcloud.com/cover/341/26391341/t7_26391341.jpg
reviewCount: 2
noteCount: 6
isbn: 9787111634744
category: 计算机-编程设计
lastReadDate: 2020-02-20
---
# 元数据
> [!abstract] 从零开始学Scrapy网络爬虫（视频教学版）
> - ![ 从零开始学Scrapy网络爬虫（视频教学版）|200](https://wfqqreader-1252317822.image.myqcloud.com/cover/341/26391341/t7_26391341.jpg)
> - 书名： 从零开始学Scrapy网络爬虫（视频教学版）
> - 作者： 张涛
> - 简介： 本书从零开始，循序渐进地介绍了目前最流行的网络爬虫框架Scrapy。即使你没有任何编程基础，阅读本书也不会有压力，因为书中有针对性地介绍了Python编程技术。另外，本书在讲解过程中以案例为导向，通过对案例的不断迭代、优化，让读者加深对知识的理解，并通过14个项目案例，提高读者解决实际问题的能力。
> - 出版时间 2019-09-01 00:00:00
> - ISBN： 9787111634744
> - 分类： 计算机-编程设计
> - 出版社： 机械工业出版社

# 高亮划线

## 第4章 Scrapy网络爬虫基础


- 📌 Request(url, headers=self.qidian_headers, callback=self.qidian_ ^26391341-13-5838-5902
    - ⏱ 2020-02-19 12:45:01 

- 📌 Request的定义形式为：        class scrapy.http.Request(url [, callback, method ='GET', headers, body，        cookies, meta, encoding='utf-8', priority=0, dont_filter=False, errback ])其中，参数url为必填项，其他为选填项，下面逐个介绍这些参数。 ^26391341-13-7487-7783
    - ⏱ 2020-02-19 12:46:02 

- 📌 ·css(query)：查找与CSS表达式匹配的节点，并返回一个SelectorList对象。参数query是CSS表达式的字符串。 ^26391341-13-9704-9770
    - ⏱ 2020-02-19 19:32:42 

- 📌 常用的CSS表达式 ^26391341-13-16130-16139
    - ⏱ 2020-02-19 19:43:22 
## 第10章 文件和图片下载


- 📌 图片管道ImagesPipeline用于实现图片的下载。你也可以扩展ImagesPipeline ^26391341-19-13559-13607
    - ⏱ 2020-02-20 09:22:47 

- 📌 yield Request(urls[i], callback=self.parse_image) ^26391341-19-19944-19994
    - ⏱ 2020-02-20 09:26:39 
# 读书笔记

## 第4章 Scrapy网络爬虫基础

### 划线评论
- 📌 extract()：提取文本数据，返回unicode字符串列表。使用xpath()或css()方法将匹配到的节点包装为SelectorList对象后，可以使用extract()方法提取SelectorList对象中的文本，并将其存放于列表中。
·extract_first():SelectorList独有的方法，提取SelectorList对象中第一个文本数据，返回unicode字符串。
·re(regex)：使用正则表达式提取数据，返回所有匹配的unicode字符串列表。
·re_first():SelectorList独有的方法，提取第一个与正则表达式匹配的字符串。  ^29927260-7ffY5yaul
    - 💭 get（）  getall（）
    - ⏱ 2020-02-19 19:33:32
   
# 本书评论

## 书评 No.1 
爬虫入门好书，讲的很细，要是有多ip代理的内容就更好了。 ^29927260-7fgRdFu3c
⏱ 2020-02-20 09:35:19
