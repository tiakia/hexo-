---
title: hexo+github+域名搭建自己的博客（一）
date: 2017-07-11 21:10:05
tags: 教程
categories: hexo
---
# 如何使用hexo+github快速搭建一个属于自己的博客

### 我是先注册的域名，我们就先从注册域名开始吧

1. 登录[万网](https://wanwang.aliyun.com)
2. 输入一个你喜欢的域名，eg: baidu
    <img src='/img/hexo/search.png'/>
3. 搜索结果会出现一群你输入的域名，区别就是后缀名不一样，com的一般都被注册了  你可以选择一个没有被注册的你喜欢的，把它买下来。（便宜点就行）
    <img src='/img/hexo/searchResult.png'/>
4. 解析域名，进入控制台 - 域名与网站（万网） - 域名 
    <img src='/img/hexo/control.png'/>
5. 开始解析域名
    点击解析 
    <img src='/img/hexo/jiexi.png'/>
6. 这里有几个参数要填写对
    + 记录类型 选择CNAME 因为代码是托管在github上的
    + 主机记录 这个是访问你域名的前缀，一般都填 wwww
    + 解析线路 默认就行
    + 记录值 这个地方填写的是你github的地址，（你的账户名).github.io
    + 点击保存，等十分钟后，解析才会成功
    <img src='/img/hexo/jiexi1.png'/>

### 第二步 配置github

1. 登录[github](https://github.com)，点击 New repository 新建一个项目
    <img src='/img/hexo/repository.png'/>
2. 填写项目名称，默认选择Public,勾选图中 初始化新建一个 README 文件
    <img src="/img/hexo/create.png"/>
3.  进入项目中，新建一个gh-pages分支，图中关键点已经标出
    <img src="/img/hexo/createBranch.png"/>
4. 进入gh-pages分支，创建一个new file，命名为CNAME，文件内容，是你刚刚解析的域名,eg: www.superMan.party
    <img src="/img/hexo/CNAME1.png"/>
    <img src="/img/hexo/CNAME2.png"/>
  **别忘了提交文件哦**
    <img src="/img/hexo/commit.png"/>
5. 最后一步，进入 setting 页面：
    <img src="/img/hexo/setting.png"/>
 **配置如图**
 分支选择对，就是gh-pages,域名填写对 www.superman.party,要和CNAME 文件 一致了
    <img src="/img/hexo/ghPages.png"/>

 **静等十分钟后，在地址栏输入你的域名访问你的网站吧，下一篇教你快速打出绚丽的博客**














