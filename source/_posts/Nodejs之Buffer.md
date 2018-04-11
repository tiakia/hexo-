---
title: Nodejs之Buffer
tags: [nodejs]
date: 2018-04-11 11:04:07
categories: Nodejs
description:
thumbnail:
keywords:
---
#### Buffer类
用于操作二进制数据的
它的声明和赋值和java中的数组操作差不多

#### 创建Buffer
```
1. var buf = new Buffer(size);//创建并为buffer分配空间，长度固定不能更改
2. var buf = new Buffer(array);//声明并赋值
3. var buf = new Buffer(string[,encoding]);//把字符转换为二进制、编码方式
//默认为utf-8编码  支持 "ascli" "utf8" "utf16le" "ucs2" "base64" "hex"
```
<!-- more -->
#### 写入缓冲区
```
buf.write(string[,offset[,length]][,encoding]);
```
参数
```
string - 写入缓冲区的字符串
offset - 缓冲区开始写入的索引值，默认为0
length - 写入的字节数， 默认为 buffer.length
encoding - 使用的编码，默认为 'utf8'
```

**返回值**
返回实际写入的大小。如果 buffer 空间不足， 则只会写入部分字符串。
#### 从缓冲区读取数据
```
buf.toString([encoding[,start[,end]]]);
```
参数
```
encoding - 使用的编码。 默认为 utf-8
start - 指定开始读取的索引位置，默认为0
end - 结束位置，默认为缓冲区末尾
```
**返回值**
解码缓冲区数据并使用指定的编码返回字符串。
#### 将 Buffer 转换为 JSON 对象
```
buf.toJSON();
```
#### 缓冲区合并
```
Buffer.concat(list[,totalLength]);
```
参数
```
list - 用于合并的 Buffer 对象数组列表
totalLength - 指定合并后Buffer对象的总长度
```
**返回值**
返回一个多个成员合并的新 Buffer 对象
```
var buf1 = new Buffer('Hello');
var buf2 = new Buffer('World');
var buf3 = Buffer.concat([buf1,buf2]);
console.log(buf3.toString());// Hello World
```
#### 缓冲区比较
```
buf.compare(otherBuffer);
```
参数
```
otherBuffer - 与 buf 对象比较的另外一个 Buffer 对象
```
返回值
```
返回一个数字，表示 buf 在 otherBuffer 之前，之后或相同
```
例子：
```
var buf1 = new Buffer('ABC');
var buf2 = new Buffer('ABCD');
var result = buf1.compare(buf2);
if(result<0){
    console.log(buf1 + " 在 " + buf2 + " 之前");
}else if(result === 0){
    console.log(buf1 + " 与 " + buf2 + " 相同");
}eles{
    console.log(buf1 + " 在 " + buf2 + " 之后");
}
```
运行结果：
```
ABC 在 ABCD 之前
```

#### 缓冲区裁剪
```
buf.slice([start[,end]]);
```
含头不含尾规则

**返回值**
返回一个新的缓冲区，它和旧缓冲区**指向同一块内存**，但是从索引 start 到 end 的位置剪切。

#### 缓冲区拷贝
```
buf.copy(targetBuffer[, targetStart[, sourceStart[, sourceEnd]]])
```
参数
```
buf: 源buffer
targetBuffer: 要拷贝的buffer
targetStart: 在待拷贝buffer的第几个位置开始放置
sourceStart: 源buffer的第几个开始进行拷贝 含头不含尾

```
**从 buf 中拷贝到 targetBuffer 中**


例子：
```
var buffer1 = new Buffer('ABC');
// 拷贝一个缓冲区
var buffer2 = new Buffer(3);
buffer1.copy(buffer2);
console.log("buffer2 content: " + buffer2.toString());
```
输出结果
```
buffer2 content: ABC
```


##### 比较 slice 和 copy
slice 选取的buf和原来引用的是相同的地址
copy 方法 和原来的引用的地址不同

**字节长度和字符串长度不一样，一个汉字的字符串长度为1 (utf8编码)，字节长度为3.**

#### 其他
```
Buffer.isBuffer() //判断是否是buffer对象
Buffer.byteLength(str);//获得str的字节长度
```
