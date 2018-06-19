---
title: Emacs的配置和使用
tags: [emacs]
date: 2018-06-06 17:00
categories: emacs
description:
thumbnail: 
keywords: emacs
---

### 修改的配置

#### 垃圾回收机制修改
 purcell的老是报错 就参考了 spacemacs 的配置
{% tabbed_codeblock init.el %}
      <!-- tab lisp -->
          (setq gc-cons-threshold 100000000)
      <!-- endtab -->
{% endtabbed_codeblock %}
<!--more-->
#### 设置中文环境,日期正常显示

{% tabbed_codeblock init-preload.el %}
    <!-- tab lisp -->
    (set-language-environment 'Chinese-GBK)
    (prefer-coding-system 'utf-8-unix)
    <!-- endtab -->
{% endtabbed_codeblock %}

#### 设置启动时的大小及位置

{% tabbed_codeblock init-preload.el %}
<!-- tab lisp -->
    ;;设置窗口位置为屏库左上角(0,0)
    (set-frame-position (selected-frame) 0 0)

    (set-frame-width (selected-frame) 110)
    (set-frame-height (selected-frame) 33)

<!-- endtab -->
{% endtabbed_codeblock %}

#### ivy 搜索到时候取消显示匹配的数字

{% tabbed_codeblock init-ivy.el %}
<!-- tab lisp -->
   ivy-count-format ""
<!-- endtab -->
{% endtabbed_codeblock %}

#### mode-line 自定义显示

#### 增加\`yasnippet\`模板

#### 增加全局搜索差价 \`ag\`

#### 增加中文输入法 \`pyim\`

#### 增加\`web-mode\`支持jsx/js/css/html&#x2026;

### 改变emacs的透明度

-   类似 mac 下的效果
-   init-alph.el

1.  具体的配置见[My GitHub](https://www.github.com/tiakia/.emacs.d)

### Org-mode 的使用
<p>tap: show/hide展示/隐藏 一级标题下的其他item
{% hl_text green %}* 一级标题 {% endhl_text %}<br/>
{% hl_text green %}** 二级标题{% endhl_text %}</p>

#### 链接

-   [Here's my Blog](http://www.tiankai.party)
##### 插入链接的快捷键
<p> {% hl_text green %}C-c & C-l {% endhl_text %}: add link</p>

<p> {% hl_text green %}C-c & C-o {% endhl_text %}: open the Link</p>

####  标记文本

**bold text**, 	 `*bold text*`
*italic text*, 	`/italic text/`
<u>underlined text</u>, 	`_underline text_`
<del>strikethrough line</del>,		`+strikethrough line+`
`verbatim`     	`=verbatim=`

#### Table use Tab to enter
|Name|Age|Occupation|生成表格然后 使用tab 来输入 会自动对齐自动添加

{% tabbed_codeblock markdown %}
<!-- tab md -->
| Name   | Age | Occupation    |
|--------+-----+---------------|
| Allen  |  15 | Teacher       |
| Clyve  |  34 | Office-worker |
| Barney |  65 | Worker        |
|--------+-----+---------------|

<!-- endtab -->
{% endtabbed_codeblock %}

| Name   | Age | Occupation    |
| ---- | ---- | ---- |
| Allen  |  15 | Teacher       |
| Clyve  |  34 | Office-worker |
| Barney |  65 | Worker        |

#### org导出为其他文件

{% hl_text green %}
C-c & C-e
{% endhl_text %}选择一个模板导出 (例如: h - o 导出为html并打开)

{% hl_text danger %}
标题文件声明
{% endhl_text %}

{% tabbed_codeblock test %}
    <!-- tab md -->
    #+STARTUP: overview
    #+TITLE: org-lesson
    #+OPTIONS: toc:nil
    #+CREATOR: Tiankai

    **** toc:nil 忽略导航,导出为HTML的时候会忽略

    <!-- endtab -->
{% endtabbed_codeblock %}

#### org 输入代码

- {% hl_text red %}
输入< + s & 敲 tab键
{% endhl_text %} 生成代码块,填写 {% hl_text danger %}
mode
{% endhl_text %}
- {% hl_text red %}
C-c $ '
{% endhl_text %} 到相应的 {% hl_text red %}
mode
{% endhl_text %} 编写代码,编写完成后 {% hl_text red %}
C-c & '
{% endhl_text %}返回

{% tabbed_codeblock test %}
<!-- tab org -->
    #+BEGIN_SRC js2
      function add(x, y){
        return x + y
      }
      let sum = add(3,4);
    #+END_SRC
<!-- endtab -->
{% endtabbed_codeblock %}

#### Todo

{% tabbed_codeblock todo.org %}
   <!-- tab org -->
   ** DONE cycle through states
      CLOSED: [2018-06-06 Wed 16:24]
   ** TODO explain todo lists
      DEADLINE: <2018-06-07 Thu>
   ** NEXT 写周报
      DEADLINE: <2018-06-08 Fri>

   <!-- endtab -->
{% endtabbed_codeblock %}

-   {% hl_text red %}
TODO  something
{% endhl_text %} 开启todo模式
-   C-c & C-t 来改变当前事项是完成还是未完成
-   shift & 上/下/左/右 可以调整时间
-   C-c & C-d 调出日历选择日期
-   C-c & a & L 显示所有待做事情

