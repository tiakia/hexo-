---
title: Nodejs之querystring
tags: [nodejs]
date: 2018-04-11 11:07:36
categories: Nodejs
description:
thumbnail:
keywords:
---
##### const querystring = require('querystring')

##### 序列化 querystring.stringify( obj, para1,para2 );
`obj`是`query`的对象
`para1`是参数之间的连接符。默认为"&"
`para2`是`key`和`value`之间的连接符。默认为"="
```
queryString.stringify({name: 'scott',course:['jade','node'],from:''});
```
输出结果
```
'name=scott&course=jade&course=node&from='
```
<!-- more -->
第二个参数
```
queryString.stringify({name: 'scott',course:['jade','node'],from:''},',');
```
输出结果
```
'name=scott,course=jade,course=node,from='
```
第三个参数
```
queryString.stringify({name: 'scott',course:['jade','node'],from:''},',',':');
```
输出结果
```
'name:scott,course:jade,course:node,from:'
```
##### 反序列化 querystring.parse(string,para1,para2);
`string`是`url`的`query`的字符串
`para1`是连接符
`para2`是`key`和`value`之间的连接符
```
querystring.parse('name=scott,course=jade,course=node,from=',',');
```
输出结果
```
{
    name: 'scott',
    course: ['jade','node'],
    form: ""
}
```
