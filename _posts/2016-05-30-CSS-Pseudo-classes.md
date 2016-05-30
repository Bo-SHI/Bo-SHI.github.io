---
layout: post
title: "CSS Pseudo classes"
date: 2016-05-30
---

# CSS 伪类 (Pseudo classes)

> CSS伪类用于向某些选择器添加特殊的效果

> 语法
  - selector:pseudo-class {property:value;}
  - selector.class:pseudo-class {property:value;}

### 锚伪类

* 在支持CSS的浏览器中，链接的不同状态都可以以不同的方式显示，这些状态包括:
  - 未被访问状态 a:link
  - 已被访问状态 a:visited
  - 鼠标悬停状态 a:hover
  - 活动状态：   a:active

### 伪类与CSS类

> 伪类可以与CSS类配合使用

### CSS2 :first-child 伪类

> 可以使用 :first-child 来选择元素的第一个子元素

> 必须声明<!DOCTYPE> :first-child 才可以在IE中生效

列子1 匹配第一个&lt;p&gt;元素:

    <head>
      <style type="text/css">
        p:first-child {color:red;}
      </style>
    </head>
    <body>
      <p>This is the first-child</p>
      <p>This is not</p>
    </body>

列子2 匹配所有&lt;p&gt;元素中的第一个&lt;li&gt;元素

    <head>
      <style type="text/css">
        p > i:first-child {color:red;}
      </style>
    </head>
    <body>
      <p><i>This is the first-child</i>.<i>This is not</i></p>
      <p><i>This is the first-child</i>.<i>This is not</i></p>
    </body>

列子3 匹配第一个&lt;p&gt;元素中的所有i元素

    <head>
      <style type="text/css">
        p:first-child > i{color:red;}
      </style>
    </head>
    <body>
      <p><i>This is the first-child</i>.<i>This is the first-child</i></p>
      <p><i>This is not</i>.<i>This is not</i></p>
    </body>

### CSS :lang伪类

> :lang 使你有能力为不同的语言定义特殊的规则


### CSS :focus伪类

> :focus 向拥有箭牌输入焦点的元素设置样式

> :focus 无法再IE中使用
