---
title: Nodejs之URL
tags: [nodejs]
date: 2018-04-11 11:02:09
categories: Nodejs
description:
thumbnail:
keywords:
---
### parse
###### 语法
```
url.parse(urlString,bool,bool);
第二个参数决定query部分以字符串返回还是以对象形式返回，默认为字符串返回即第二个参数默认为false;
第三个参数表示在没有完整协议串的时候（即无http:/https:）的时候‘//’之后的字符如何解释，若为false即将‘//’之后的当做路径解释，若为true则会将‘//’与‘/’之间的字符串解释为主机
```
例子：
```
var url = require(url);
var _url = "http://www.imooc.com:8080/course/list?from=scott&course=node#floor1";
url.parse(_url)
```
<!-- more -->
输出结果
```
{
    protocol: 'http',// 表示url采用什么协议
    slashed: true,// 是否有斜线
    auth: null,
    host: 'imooc.com:8080',//表示主机
    port: '8080',//端口
    hostname: 'imooc.com',//主机名称
    hash: '#floor1',//#后面的内容，包含#
    serach: '?from=scott&course=node',//？后面#之前的内容包含？（查询字符串）
    query: 'from=scott&course=node',// search不包含？的内容（给http服务器发送数据）
    pathname: '/course/list',//路径的名称，一般指主域名之后的内容
    path: '/course/list?from=scott&course=node',//路径
    herf: 'http://imooc.com:8080/course/list?from=scott&course=node#floor1'
}
```
第二个参数
```
//第二个参数bool值，处理query字段,默认是false
url.parse(_url,true)
```
输出结果（看query)
```
{
    protocol: 'http',
    slashed: true,
    auth: null,
    host: 'imooc.com:8080',
    port: '8080',
    hostname: 'imooc.com',
    hash: '#floor1',
    serach: '?from=scott&course=node',
    query: {from: 'scott', course: 'node' },//成了对象
    pathname: '/course/list',
    path: '/course/list?from=scott&course=node',
    herf: 'http://imooc.com:8080/course/list?from=scott&course=node#floor1'
}
```
没有第三个参数
```
url.parse('//imooc.com/course/list',true);
```
输出结果
```
{
    protocol: null,
    slashed: null,
    auth: null,
    host: null,
    port: null,
    hostname: null,
    hash: null,
    serach: '',
    query: {},
    pathname: '//imooc.com/course/list',
    path: '//imooc.com/course/list',
    herf: '//imooc.com/course/list'
}
```
有第三个参数
```
url.parse('//imooc.com/course/list',true,true);
```
输出结果
```
{
    protocol: null,
    slashed: true,
    auth: null,
    host: 'imooc.com',
    port: null,
    hostname: 'imooc.com',
    hash: null,
    serach: '',
    query: {},
    pathname: '/course/list',
    path: '/course/list',
    herf: '//imooc.com/course/list'
}
```
