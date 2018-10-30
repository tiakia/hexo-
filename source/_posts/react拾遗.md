---
title: react拾遗
date: 2018-10-23 14:39
categories: react
tags: [react]
keywords:
- react
clearReading: true
thumbnailImage:
thumbnailImagePosition: left  //缩略图显示的位置，上下左右都可以
autoThumbnailImage: true
metaAlignment: center  //文章页图片上的文字居中显示
coverImage: http://ostu98x74.bkt.clouddn.com/cover/cover.jpg
coverCaption:
coverMeta: in
coverSize: full
comments: true
---

总结一些 react 中常见的面试题吧，同时也是让自己多学习学习 react 相关的知识。查漏补缺。

<!-- more -->
##### 组件的命名
基于路径命名的方式，举个例子，组件的路径如果是 `components/User/List.jsx`，那么它就被命名为 `UserList`。

#### !!()
!!(a)的作用是将a强制转换为布尔类型
```
let a = 123;
console.log(!!a); // true

let b = '';
console.log(!!b); //false

let c = 'null';
console.log(!!c); //true

let d = null;
console.log(!!d); //false
```
