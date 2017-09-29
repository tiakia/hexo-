---
title: 7个你可能不认识的css单位
tags: [css]
date: 2017-09-28 10:18:30
categories: css
description: 解密css单位
thumbnail:
keywords:
---
#### 注： [原文链接(https://github.com/simaQ/cssfun/issues/1)](https://github.com/simaQ/cssfun/issues/1)

众所周知CSS技术我们虽然很熟悉，在使用的过程却很容易被困住，这让我们在新问题出现的时候变得很不利。
随着web继续不断地发展，对于新技术新解决方案的要求也会不断增长。因此，作为网页设计师和前端开发人员，我们别无选择，必须熟悉我们手上的工具，做到知己知彼，这样才能百战不殆。

这就意味着有那么些个特别的货，虽然平常都不怎么会用上，但是一旦某个地方需要它们了，他们就真的是特么得合适不过来了呢。

今儿，我就准备向大伙儿介绍一些你们之前可能很少见过CSS家伙们。他们每个都是度量的单位，类似pixel 和 em 这样的，但是很有可能你之前从来就没听过这些家伙们！就让我们一起来交个朋友吧~

#### rem

我们首先介绍下和我们熟悉的很相似的货。em 被定义为相对于当前对象内文本的字体大小。炒个栗子，如果你给body小哥设置了font-size字体大小，那么body小哥的任何子元素的1em就是等于body设置的font-size。
```
<body>
    <div class="test">Test</div>
</body>
```
```
body {
    font-size: 14px;
}
div {
    font-size: 1.2em; // calculated at 14px * 1.2, or 16.8px
}
```
你看，这里div这娃的字体大小是1.2em。解释来说，就是他从body爹爹那里继承的字体大小（这里是14px）的1.2倍，结果就是16.8px。

但是，如果你用em一层一层级联得定义嵌套元素的字体大小又会花生什么事情呢？在下面这一小段代码里我们应用了和上面一样一样的CSS，每一个div都从它上一级父元素继承了字体大小，并且逐渐得增加。
```
<body>
    <div>
        Test <!-- 14 * 1.2 = 16.8px -->
        <div>
            Test <!-- 16.8 * 1.2 = 20.16px -->
            <div>
                Test <!-- 20.16 * 1.2 = 24.192px -->
            </div>
        </div>
    </div>
</body>
```
虽然在某些地方这正是我们想要的，但是通常情况下我们还是希望就依赖单一的相对度量单位就好。这时候嘛，我们就可以使用 rem 了。 ‘r’是“root”的缩写，意思就是1rem等于根元素的字体大小；大部分情况下，根元素就是<html>元素了。
```
html {
    font-size: 14px;
}
div {
    font-size: 1.2rem;
}
```
这样在上面的那三个嵌套的div娃们的字体大小都是 1.2*14px = 16.8px 了。

#### 适用于网格布局

Rems 不仅仅只是在设置字体大小上很方便。再炒个栗子，你可以用基于html根元素字体大小的rem作为整个网格布局或者UI库的大小单位，然后在其他特定的地方用em单位。这样将会给你带来更多的字体大小和伸缩的可控性，
```
.container {
    width: 70rem; // 70 * 14px = 980px
}
```
概念上来说，这个方法的思想就是让你的界面根据你的内容进行缩放。但是，这样做并不是对所有的情况都有意义。

#### vh and vw

响应式web设计离不开百分比。但是，CSS百分比并不是所有的问题的最佳解决方案。CSS的宽度是相对于包含它的最近的父元素的宽度的。但是如果你就想用视口（viewpoint）的宽度或者高度，而不是父元素的，那该肿么办？ 这就是 vh 和 vw 单位为我们提供的。

1vh 等于1/100的视口高度。栗子：浏览器高度900px, 1 vh = 900px/100 = 9 px。同理，如果视口宽度为750， 1vw = 750px/100 = 7.5 px。

可以想象到的，他们有很多很多的用途。比如，我们用很简单的方法只用一行CSS代码就实现同屏幕等高的框。
```
.slide {
    height: 100vh;  /* viewpointHeight/100 = 100vh */
}
```
假设你要来一个和屏幕同宽的标题，你只要设置这个标题的font-size的单位为vw，那标题的字体大小就会自动根据浏览器的宽度进行缩放，以达到字体和viewport大小同步的效果，有木有？！


#### vmin and vmax

vh和 vw 依据于视口的高度和宽度，相对的，vmin 和 vmax则关于视口高度和宽度两者的最小或者最大值。比如，浏览器的宽度设置为1100px，高度设置为700px， 1vmin = 7px， 1vmax = 11px。如果宽度设置为800px,高度设置为1080px, 1vmin就等于8px, 1vmax则未10.8px。
那么问题来了，我们应该在什么场景下使用这两个单位呢？
假设有一个元素，你需要让它始终在屏幕上可见。只要对其高度和宽度使用vmin单位，并赋予其低于100的值就可以做到了。再来个栗子，可以这样定义一个至少有两个边触摸到屏幕的方形：
```
.box {
    height: 100vmin;
    width: 100vmin;
}
```
![](http://ostu98x74.bkt.clouddn.com/css/6f6549ba-6b3a-11e4-8a20-ed18bc2c045c.png)
如果你要让这个方形框框始终铺满整个视口的可见区域（四边始终触摸到屏幕的四边）
```
.box {
    height: 100vmax;
    width: 100vmax;
}
```
![](http://ostu98x74.bkt.clouddn.com/css/73bab7d4-6b3a-11e4-8bbd-263380e2f789.png)
结合使用这些单位可以为我们提供一个新颖有意思的方式来灵活地利用我们视口的大小。

#### ex and ch

ex 和 ch 单位，类似于 em 和 rem, 依赖于当前的字体和字体大小。 但是，不同的是，这两货是基于字体的度量单位，依赖于设定的字体。

ch 单位通常被定义为数字0的宽度。你可以在Eric Meyers的博客里找到关于它的一些有意思的讨论，例如将一个等宽字体的字母"N"的宽度设置为40ch，那么在另一种类型的字体里它却可以包含40个字母。这个单位的传统用途主要是盲文的排版，但是除此之外，肯定还有可以应用他的地方。

ex 定义为当前字体的小写x字母的高度或者 1/2 的 1em。 很多时候，它是字体的中间标志。

![](http://ostu98x74.bkt.clouddn.com/css/890205a2-6b3a-11e4-852d-e239d3bf2475.png)
x-height; the height of the lower case x

这些单位有很多用途，大部分用于版式的微调。比方说，sup 元素（上角文字标），可以通过position:relative;bottom: 1ex;实现 。类似的方法，你可以实现一个下角文字标。浏览器默认的方式是利用
上标和下标特定垂直对齐规则，但是如果你想更细粒度更精确得控制，你可以像下面这样做：
```
sup {
    position: relative;
    bottom: 1ex;
}
sub {
    position: relative;
    bottom: -1ex;
}
```
#### 补充：  
vh与flexbox结合起来做Sticky footer(如果页面内容不够长的时候，页脚块粘贴在视窗底部；如果内容足够长时，页脚块会被内容向下推送。)原文: https://www.w3cplus.com/css3/css-secrets/sticky-footers.html © w3cplus.com
```
<body>
<div class='main'>
    
</div>
<div class='footer'>

</div>
</body>
```
```
body{
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}
.main{
    flex: 1
}
```



