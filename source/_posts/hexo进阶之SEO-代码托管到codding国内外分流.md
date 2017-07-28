---
title: hexo进阶之SEO & 代码部署到codding国内外分流
tags: hexo
date: 2017-07-28 11:42:55
categories: hexo
description: 
thumbnail:
---
配置折腾的差不多了，终于可以好好的写博客了，今天给大家分享的是SEO，也叫搜索引擎优化，是指别人在谷歌或百度的时候搜索引擎能把你的文章给显示出来，第二个就是把自己的代码部署到coding上，国内的一个类似github的网站，让国人访问你的博客时候，通过coding，外国友人访问的时候通过github，其实我觉得没必要，可是耐不住想折腾就搞了一下子。
**SEO**
1. 验证自己的网站有没有被百度或谷歌收录很简单，输入`site: tiankai.party`
2. `先来百度吧`
3. [点击提交网址](http://zhanzhang.baidu.com/site/index),进入百度站长平台，点击添加网站，输入自己申请的域名，选择一个自己的领域，然后验证网站
4. `百度`提供了三种验证方式，我选择的是HTML的验证方式*简单粗暴*谷歌之后也是用的这个方法
5. 我用的是[material主题](https://github.com/viosey/hexo-theme-material),我说一下思路，首先你要找到渲染模板文件，只要找到模板，一改动，其他的就跟着改变了，material的模板文件在`thems -> material -> layout -> _partial`这里面就是你博客的模板文件了，你要是自定义也是改动这些文件，找到`head.ejs`,这个就是你博客所有文件的head文件了，打开，把刚才HTML标签验证的那段==meta==标签粘贴到这（基本的代码能看懂吧，别粘错了，找个合适的地方粘贴）
6. 粘贴好后，重新打包编译部署一下

``` stylus
hexo clean
hexo d -g 
```
7. 回到站长平台，点击完成验证
8. 验证成功后，等吧，百度可慢了，过几天站点管理就会出现你的网站信息了。
9. `谷歌`
10. 因为被墙所以谷歌弄的话最好还是翻个墙，速度也快
11. http://www.jianshu.com/p/86557c34b671


