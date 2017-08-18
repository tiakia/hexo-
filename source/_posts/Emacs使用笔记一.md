---
title: Emacs使用笔记一
tags: [Emacs]
date: 2017-08-04 22:57:27
categories: Emacs
description:
thumbnail:
keywords: Emacs
---
同事一直在耳旁推荐使用这个编辑器，引用编程界的几句话，来说一下这款编辑器的地位，世界上有三种编辑器，一种是Emacs,一种是Vim,还有一种是其他；Emacs被称作是神用的编辑器，Vim被称作是神一样的编辑器，足以说明Emacs的地位，作为程序猿理想的编辑器，应该是有长远性的，可定制性的，逐渐形成一个符合自己习惯的编辑器，我先用了Vim，老实说有点不习惯它的来回切换模式的做法，只是尝试了一下就放弃了，那会也许是想着这款神用的编辑器，果不其然，只是一会就觉得一个字，爽，比起vim来Emacs用的真是爽爆了，Emacs提倡的所见即所得，不想Vim那样需要来回切换编辑模式，Emacs是输入什么就是什么。

1. 下载[Emacs](https://www.gnu.org/software/emacs/)，选择对应的版本下载安装，我选择的是`emacs-25.1-x86_64-w64-mingw32.zip`，下载完成后解压到一个盘，记得新建一个文件`emacs`，然后解压到这里，要不就会解压到根目录，然后找到bin目录，配置到环境变量中，比如说我的解压到了D盘一个Pragram文件下的emacs文件中，那我配置到环境变量的路径就是`D:\Pragram\emacs\bin`这样就可以在命令行中运行emacs了，`Win + R` 输入`cmd`,然后输入`emacs`，打开emacs的ui边界，输入`emacs -nw` 直接在命令行打开emacs
2. 先来了解一下基本概念，在windows中，Emacs的 C 表示的Ctrl键，M 表示的Alt键，一般的命令都是与这俩个命令分不开的，这里建议将Ctrl键与大写锁定键CapsLock换掉，否则的话对小拇指的压力太大了， 建议先看教程，因为写的太好了，绝对是入门的好东西，而且还是中文，打开教程的快捷键`C-h t`,然后就进入教程了。
3. 快捷键：
退出 : C-x C-c
保存 : C-x C-s
上一行 : C-p
下一行 : C-n
左(后)移动一个字符 : C-b
右(前)移动一个字符 : C-f
左移动一个字符串 : M-b
右移动一个字符串 : M-f
下一页 : C-v
上一页 : M-v
这一行的行首 : C-a 光标就在这一行
这一行的行位 : C-e 光标就在这一行
行的行首 : M-a 光标会向上走
行的行尾 : M-e 光标会向下走
撤销 : C-/
删除一行 : C-k 光标要在行首
CTRL+d相当于键盘上的DELETE键，
先标记 C+shift+2(Ctrl+@) 然后就通过上下左右键选择好复制的区域，然后：
`C-w` 剪切
`M-w` 复制
`C-y` 粘贴
搜索 `C-s` 输入搜索的关键词，然后通过`C-r`键和`C-s`控制搜索的前后
全选 : `C-x h`
格式化对齐: `C-M-\`
打开新窗口 : `M-x make-frame`
打开文件 : `C-x C-f` 然后输入文件名字，如果有直接打开，如果没有创建，然后关闭的时候会提醒你是否保存，或者自己保存`C-x C-s`。
主题改变 `M-x customize-themes`

打开新的窗口 `M-x make-frame`

显示行号 `M-x linum-mode`

到文件末尾 `M->`
到文件开头 `M-<`
推荐世界级大神[Purcell](https://github.com/purcell/emacs.d)的配置，windows下ui界面有点卡
今天用到的快捷键大概就这些，字体选择的我直接`Options - Set Default Font`,然后选择的。大概就这么多，以后继续写，晚安。