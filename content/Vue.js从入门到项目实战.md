---
doc_type: weread-highlights-reviews
bookId: "26846821"
author: 刘汉伟
cover: https://cdn.weread.qq.com/weread/cover/53/YueWen_26846821/t7_YueWen_26846821.jpg
reviewCount: 13
noteCount: 1
isbn: 9787302523888
category: 计算机-编程设计
lastReadDate: 2020-02-23
---
# 元数据
> [!abstract] Vue.js从入门到项目实战
> - ![ Vue.js从入门到项目实战|200](https://cdn.weread.qq.com/weread/cover/53/YueWen_26846821/t7_YueWen_26846821.jpg)
> - 书名： Vue.js从入门到项目实战
> - 作者： 刘汉伟
> - 简介： 本书从Vue框架的基础语法讲起，逐步深入Vue进阶实战，并在最后配合项目实战案例，重点演示了Vue在项目开发中的一些应用。在系统地讲解Vue的相关知识之余，本书力图使读者对Vue项目开发产生更深入的理解。 本书共分为11章，涵盖的主要内容有前端的发展历程、Vue的基本介绍、Vue的语法、Vue中的选项、Vue中的内置组件、Vue项目化、使用Vue开发电商类网站、使用Vue开发企业官网、使用Vue开发移动端资讯类网站、使用Vue开发工具类网站。 本书内容通俗易懂、案例丰富、实用性强，特别适合Vue的初学者和从业人员阅读，同时也适合职业生涯遇到“瓶颈”的前端从业人员和其他编程爱好者阅读。另外，本书也适合作为相关培训机构的教材。
> - 出版时间 2019-04-01 00:00:00
> - ISBN： 9787302523888
> - 分类： 计算机-编程设计
> - 出版社： 清华大学出版社

# 高亮划线

## 2.3 数据响应式原理


- 📌 computed: {  // 计算属性 ^26846821-15-3857-3879
    - ⏱ 2020-02-21 19:34:34 
## 4.1 数据和方法


- 📌 [插图]图4.3 使用$set绑定属性到对象中此时的profile被加入Vue的响应式系统，当笔者点击按钮时，视图也发生了变化。最后还要注意的一点是，慎重地将已有内存地址的对象用于data选项，无论以对象还是函数形式，比如以下用法：<div id="app"><button-counter></button-counter>  // 调用两次组件<button-counter></button-counter></div><script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.min.js"></script><script type="text/javascript">let jack = {counter: 0} ^26846821-23-5903
    - ⏱ 2020-02-23 19:45:30 
# 读书笔记

## 2.2 Vue实例介绍

### 划线评论
- 📌 this.title = 'Hello ' + ['China', 'World', 'Universe'][Math.
     floor(Math.random() * 2.999)]  ^29927260-7fiZirLa6
    - 💭 Math.random() 是得到一个0-1之间随机数.
Math.floor(i) 是得到一个数的整数部分
Math.random()*2.999的值是[0-2.999)之间的随机数
就是指随机出来的一个0,1,2,其中的一个
    - ⏱ 2020-02-21 19:11:59

### 划线评论
- 📌 this.$destroy()  ^29927260-7fiZxAIRe
    - 💭 节点上绑定的Vue实例已被销毁。
    - ⏱ 2020-02-21 19:15:43

### 划线评论
- 📌 // 在实例挂载到DOM节点上之后
         mounted () {
            console.log('mounted')
         },  ^29927260-7fiYWB2BW
    - 💭 mount 挂载
    - ⏱ 2020-02-21 19:06:36

### 划线评论
- 📌 生命周期图  ^29927260-7fiZzFztJ
    - 💭 vue生命周期
    - ⏱ 2020-02-21 19:16:13
   
## 2.3 数据响应式原理

### 划线评论
- 📌 let a = 3, b = 4  ^29927260-7fiZYyYxV
    - 💭 let？
    - ⏱ 2020-02-21 19:22:21

### 划线评论
- 📌 computed: {  // 计算属性  ^29927260-7fj0NkHSV
    - 💭 计算属性
    - ⏱ 2020-02-21 19:34:52
   
## 3.2 属性绑定

### 划线评论
- 📌 'color': -1 ? 'gray' : 'black',  ^29927260-7fjSgXtIY
    - 💭 疑惑
    - ⏱ 2020-02-22 09:11:24
   
## 3.4 双向绑定

### 划线评论
- 📌 双向绑定  ^29927260-7fjTNb3vR
    - 💭 针对可输入元素，将输入绑定到输入元素与输出元素上
    - ⏱ 2020-02-22 09:34:37
   
## 3.5 条件渲染和列表渲染

### 划线评论
- 📌 this.order = ++this.order % 3  ^29927260-7flyNETRe
    - 💭 很有意思的写法：后加再整除，得到数值变换
    - ⏱ 2020-02-23 11:47:25

### 划线评论
- 📌 <!-- index作为第二个参数，用以标识下标 -->
            <li v-for="(item, index) in users">{{ index }}.&nbsp;{{ item.name
     }}</li>
         </ul>
       </div>
       <div style="margin-left: 170px;over flow: hidden"> <!-- BFC -->
         <h2>用户列表</h2>
         <ul>
            <!-- uIndex作为第二个参数，用以标识下标 -->
            <li v-for="(user, uIndex) of users">{{ uIndex }}.&nbsp;{{ user.
     name }}</li>  ^29927260-7fm1hIAzl
    - 💭 v-for语法第一个参数为值，第二个为下标，名字可以任意取
    - ⏱ 2020-02-23 19:02:21

### 划线评论
- 📌 ul>
              <!-- key作为第二个参数，用以标识键名 -->
              <li v-for="(value, key) of user">{{ key }}:&nbsp;{{ value }}</li>
            </ul>  ^29927260-7fm1GdY9L
    - 💭 ul li标签的关系
    - ⏱ 2020-02-23 19:08:23

### 划线评论
- 📌 (factor || 1)) + (base || 0)  ^29927260-7fm2bnvMZ
    - 💭 若参数为空，则使用默认值
    - ⏱ 2020-02-23 19:16:04

### 划线评论
- 📌 this.users.reverse()  ^29927260-7fm2wFWJe
    - 💭 ？
    - ⏱ 2020-02-23 19:21:18
   
# 本书评论
