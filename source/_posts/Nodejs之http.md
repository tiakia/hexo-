---
title: Nodejs之http
tags: [nodejs]
date: 2018-04-11 11:06:12
categories: Nodejs
description:
thumbnail:
keywords:
---
{% alert info %}
首先需要引入http模块 `var http = require('http')`
{% endalert %}
创建服务
<!-- more -->
{% tabbed_codeblock  test.js  %}
<!-- tab js -->
http.createServer(function(res,req){
    //  request 事件
})

<!-- endtab -->


{% endtabbed_codeblock %}

或者是:

{% tabbed_codeblock  test.js  %}
<!-- tab js -->
const server = http.createServer();
server.on('request',callback); //监听request事件
<!-- endtab -->
{% endtabbed_codeblock %}

`createserver`的回调函数就是 `server.on('request',callback);`

{% alert info %}
 `listening` 监听服务是否开启了
{% endalert %}



{% tabbed_codeblock  test.js  %}
<!-- tab js -->
server.listening //返回一个 bool 值 表示服务器是否正在监听连接
<!-- endtab -->
{% endtabbed_codeblock %}

{% alert warning %}
`request`事件，回调函数的俩个参数重要的属性
{% endalert %}


{% tabbed_codeblock  test.js  %}
<!-- tab js -->
server.on('request',function(req, res){...})
<!-- endtab -->
{% endtabbed_codeblock %}

### req
- **httpVersion**
- **headers**
- **url**
- **method**

### res
- **res.write(chunk[,encoding])**
    - 返回给前端的数据chunk 编码方式 默认utf8
- **res.writeHead(statusCode, [reasonPhrase状态码对应的文字信息], [headers])**
    -  这个方法只能在当前请求中用一次，并且必须在response.end()之前调用
- **res.setHeader(name, value)**
    - 设置返回头信息,单个的,自定义的
- **res.statusCode**
    -  该属性用来设置返回的状态码
- **res.end([chunk][,encoding)**
    - 当所有正文和头信息发送完成以后调用该方法，告诉服务器数据已经全部发送完了，
这个方法在每次完成信息发送以后必须调用，并且是最后调用



{% tabbed_codeblock  test.js  %}
<!-- tab js -->
server.on('error',function(err){...})
<!-- endtab -->
{% endtabbed_codeblock %}

`error`事件用来监听连接出错的情况


{% tabbed_codeblock  test.js  %}
<!-- tab js -->
server.listen()
<!-- endtab -->
{% endtabbed_codeblock %}

`listen`事件，用来确定连接的端口号和主机名，必须有`listen`事件才能开始连接


{% tabbed_codeblock  test.js  %}
<!-- tab js -->
server.listen(8080, 'localhost');
<!-- endtab -->
{% endtabbed_codeblock %}

#### http处理get/post请求
  - 在`request`事件中回调函数可以通过`req.url`拿到这个`url`
  - 使用`url.parse()`方法解析`url`拿到`url`的对象`urlStr`
  - 根据`urlStr.pathname`来加载相应的页面
  - `get`请求的数据直接写在了`url`的`query`中
  - 直接使用`querystirng`模块来解析`urlStr.query`拿到数据
  - 而`post`请求数据写在了缓存区`buffer`中
  - 在写入数据的过程中触发一个`data`事件
  - 数据写入完成的时候触发一个`end`事件
  - 数据在触发`end`事件的时候发送完成，转成字符串和`get`请求的数据格式一样
  - 使用`querystirng.parse()`解析得到数据的对象表示

{% alert success %}
示例代码
{% endalert %}



{% tabbed_codeblock  test.js  %}
<!-- tab js -->
var http = require('http');
var url = require('url');
var fs = require('fs');
var querystring = require('querystring');

const server = http.createServer();

const htmlDir = __dirname + '/html/';

server.on('request', function(req, res){
    var urlStr = url.parse(req.url);
    switch(urlStr.pathname) {
        case '/':
            sendData(htmlDir + 'index.html', req, res);
            break;
        case '/user':
            sendData(htmlDir + 'user.html', req, res);
            break;
        case 'login':
            sendData(htmlDir + 'login.html', req, res);
            break;
        case 'login/check':
            if(req.method.toUpperCase() === 'POST'){//POST请求
                var str = '';

                req.on('data', function(chunk){
                    str += chunk;
                });

                req.on('end',function(){
                    //str里面写入了所有的通过POST请求的数据，形式如下
                    //userName=miaov&password=123463
                    const post_data = querystring.parse(str,"&");
                    //post_data里就是post请求的数据对象
                });

            }else{//GET请求
                const get_data = queryString.parse(urlStr.query,'&');
                //get_data就是get请求数据的对象
            }
            break;
        default:
            sendData(htmlDir + 'err.html', req, res);
            break;
    }
});

function sendData(fileName, req, res){
    fs.readFile(fileName, function(err, data){
        if(err){
            res.writeHead(404,{
                'content-type' : "text/html;charset=utf8"
            });
            res.write('页面找不到了');
            res.end();
        }else{
            res.writeHead(200,{
                'content-type' : 'text/html;charset=utf8'
            });
            res.write(data);
            res.end();
        }
    }
}

server.on('error', function(err){
    console.log(err);
});

server.listen(8080, 'localhost');


<!-- endtab -->
{% endtabbed_codeblock %}
