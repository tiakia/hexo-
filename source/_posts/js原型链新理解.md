---
title: js原型链新理解
tags: [javaScript]
date: 2018-04-10 17:35:08
categories:
description:
thumbnail:
keywords:
---
### 对象都是由函数创建的

```
        // 对象都是由函数创建的
        //var obj = { a: 10, b: 20 };
        //var arr = [5, 'x', true];

        var obj = new Object();
        obj.a = 10;
        obj.b = 20;

        var arr = new Array();
        arr[0] = 5;
        arr[1] = 'x';
        arr[2] = true;
```
<!-- more -->
###  函数也是一种对象
  - 他也是属性的集合，你也可以对函数进行自定义属性。
  ```
    function Fn() { }
    Fn.prototype.name = 'xxx';
    Fn.prototype.getYear = function () {
        return 1988;
    };
  ```
  - <font color=#f50>  每个函数都有一个属性叫做prototype。</font>
  - prototype的属性值是一个对象（属性的集合），默认的只有一个叫做constructor的属性，指向这个函数本身。
  ```
    var fn = new Fn();
    console.log(fn.name); // xxx
    console.log(fn.getYear()); // 1988
  ```

> 代码解释：Fn是一个函数，fn对象是从Fn函数new出来的，这样fn对象就可以调用Fn.prototype中的属性。
> 因为每个对象都有一个隐藏的属性——`__proto__`，这个属性引用了创建这个对象的函数的prototype。即：`fn.__proto__=== Fn.prototype`


- <font color="#f50">每个对象都有一个`__proto__` 属性，指向创建该对象的函数的prototype</font>

  - `Fn.prototype` 也是一个对象（属性的集合）它的`__proto__`指向的是`Object.prototype` (__创建该对象的函数是 function Object()__)

  - `function Fn(){...}`是一个函数，既然函数也是对象，那么function Fn(){...}也有`__proto__`属性，指向的是`Function.protorype`

  - `Function`也是一个函数，函数是一种对象，也有`__proto__`属性。既然是函数，那么它一定是`Function`创建。所以`Function`是被自身创建的。所以它的`__proto__`指向了自身的Prototype。即`function Function().__proto__ === Function.protorype`

  - `Function.protorype`也是一个对象,也是一个普通的被Object创建的对象,所以它的`__proto__`指向的是 `Object.prototype`

  - `Object.protorype.__proto__ === null` (__特殊__)

  - 对象是被函数创建的  引申出 `Object.__proto__ === Function.prototype`
