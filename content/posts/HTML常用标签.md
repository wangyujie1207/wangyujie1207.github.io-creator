---
title: "HTML常用标签"
date: 2020-02-19T20:59:42+08:00
tags: ["html"]
---
### a标签的用法
```
什么是a标签?
a标签的作用: 就是用于控制页面与页面之间跳转的
a标签的格式: <a href="指定需要跳转的目标界面">需要展现给用户查看的内容</a>

a标签中有一个叫做target属性, 这个属性的作用就是专门用于控制如何跳转
_self: 用于在当前选项卡中跳转, 也就是不新建界面跳转. 默认就是_self
_blank: 用于在新的选项卡中跳转, 也就是新建界面跳转

a标签中还有一个属性, 叫做title. a标签中的title和img标签中的title一样, 都是用来控制鼠标悬停时显示的提示文本的
鼠标放在链接上面时会出现title，并且利于蜘蛛爬行时抓取，方便蜘蛛识别

注意点:
1.a标签不仅可以让文字可以点击, 还可以让图片也能够被点击
2.一个a标签必须有一个href属性, 否则a标签不知道要跳转到什么地方
3.如果通过a标签的href属性指定一个URL地址, 那么必须在地址前面加上http://或https://
4.a标签的href属性除了可以指定一个网络地址以外, 还可以指定一个本地地址
```
### img标签的用法
```
<img src="/i/eg_tulip.jpg"  alt="上海鲜花港 - 郁金香" />
```
### table定义
```
定义和用法
<table> 标签定义 HTML 表格。
简单的 HTML 表格由 table 元素以及一个或多个 tr、th 或 td 元素组成。
tr 元素定义表格行，th 元素定义表头，td 元素定义表格单元。
更复杂的 HTML 表格也可能包括 caption、col、colgroup、thead、tfoot 以及 tbody 元素。
```
### table标签的用法
```xhtml
<table border="1">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>
```