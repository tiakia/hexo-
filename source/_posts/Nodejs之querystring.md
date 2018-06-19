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
{% tabbed_codeblock  test.js %}
<!-- tab js -->
queryString.stringify({name: 'scott',course:['jade','node'],from:''});
<!-- endtab -->
<!-- tab result -->
'name=scott&course=jade&course=node&from='
<!-- endtab -->
{% endtabbed_codeblock %}

<!-- more -->
第二个参数
{% tabbed_codeblock  test.js %}
<!-- tab js -->
queryString.stringify({name: 'scott',course:['jade','node'],from:''},',');
<!-- endtab -->
<!-- tab result -->
'name=scott,course=jade,course=node,from='
<!-- endtab -->
{% endtabbed_codeblock %}

第三个参数

{% tabbed_codeblock  test.js %}
<!-- tab js -->
queryString.stringify({name: 'scott',course:['jade','node'],from:''},',',':');
<!-- endtab -->
<!-- tab result -->
'name:scott,course:jade,course:node,from:'
<!-- endtab -->
{% endtabbed_codeblock %}

##### 反序列化 querystring.parse(string,para1,para2);
`string`是`url`的`query`的字符串
`para1`是连接符
`para2`是`key`和`value`之间的连接符

{% tabbed_codeblock  test.js %}
<!-- tab js -->
querystring.parse('name=scott,course=jade,course=node,from=',',');
<!-- endtab -->
<!-- tab result -->
{
    name: 'scott',
    course: ['jade','node'],
    form: ""
}

<!-- endtab -->
{% endtabbed_codeblock %}
