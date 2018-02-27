---
title: 使用谷歌云免费搭建vpn使用一年
tags: [vpn]
date: 2018-01-17 18:14:07
categories: 
description: 
thumbnail:
keywords: vpn,谷歌云
---
谷歌云现在有活动，新注册的可以免费使用一年，之前同事使用这个搭建了一个梯子，可以访问国外的网站，我今天自己搭建了一下，遇到不少坑，在这里记录一下  
有俩个先决条件
- 信用卡
- 可以翻墙访问谷歌  

信用卡这个是谷歌必须要求的，在注册的时候就需要绑定，绑定成功会扣到1美元，过几天会退回来，就是验证一下信用卡是否可用。  
翻墙这个问题可以使用蓝灯，也可以使用一个谷歌的扩展程序`谷歌访问助手`这个我在后面会给出链接，这个访问助手智能访问谷歌搜索和谷歌邮箱，其他的油管之类的就不行了。话不多说，紧接着开始教程。
<!--more-->
#### 注册
- 首先注册一个谷歌账号
- 登录[谷歌云](https://cloud.google.com/)
- 点击免费试用  
![图片1](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%911.png)
- 然后就是同意谷歌服务条款
- 绑定信用卡号，填写个人信息,账号类型为 个人
- 进入页面后，点击左上角的面包屑导航
- 点击 Compute Engine - VM实例 - 创建
   - 名称随意
   - 地区选择 推荐 asia-east1-c 亚洲东部
   - 机器类型选择最低的 微型
   - 启动磁盘选择 Debian GUN/Linux 8 的操作系统
   - 点击勾选 http 和 https
   - 点击 管理、磁盘、网络、SSH秘钥的 网络的tab选项卡，点击网络接口，外部 ip 选择新建一个静态ip名称随意，内部 ip 临时(自动) 一个地区静态ip只能创建一个
![图片2](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%912.png)
![图片3](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%913.png)
![图片4](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%914.png)
![图片5](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%915.png)
- 点击创建  
![图片6](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%916.png)
- 创建成功后，再点击 左上角 的面包屑导航
- 点击网络 VPC网络 - 防火墙规则 - 创建防火墙规则 - 名字随意起（其他没有提及的默认） - 流量方向 入站 - 目标标记 http-server - ip地址范围 0.0.0.0/0 - 协议和端口 全部允许 - 点击保存 
![图片7](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%917.png)
![图片8](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%918.png)
- 同样的方法再新建一个，只是 目标标记 改为 https-server
- 顺带看一眼 外部ip 是不是 静态的
![图片9](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%919.png)
##  安装bbr加速
- 然后返回 VM实例 - 点击 在浏览器打开ssh - 然后 输入以下命令 
```
1. sudo -i  

2. wget -N --no-check-certificate https://raw.githubusercontent.com/FunctionClub/YankeeBBR/master/bbr.sh && bash bbr.sh install

3. 如果出现蓝屏 选择 NO

4. 需要重启 输入 y，关闭 重新打开一个ssh

5. sudo -i

bash bbr.sh start
```
## 安装shadowsocksR 
### 推荐俩个脚本 这是第一个
```
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh && chmod +x shadowsocksR.sh

./shadowsocksR.sh 2>&1 | tee shadowsocksR.log
```

完成后会要求输入 密码 - 端口号 然后剩下的回车就好  这里我输入的密码是 123456 端口是 455  
![图片12](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%9112.png)  
完成后会出现如下图  
![图片13](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%9113.png)  
### 推荐第二个脚本 这俩个脚本 任选一个安装即可
```
wget -N --no-check-certificate https://softs.fun/Bash/ssrmu.sh && chmod +x ssrmu.sh && bash ssrmu.sh
```
然后按照提示操作    
- 安装脚本 
- 设置 用户名 密码 端口号 
- 加密方式 协议 和 混淆 推荐按下图的选择
![图片14](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%9114.png)   
最后完成后如下图  
![图片11](http://ostu98x74.bkt.clouddn.com/googlecloud%E8%B0%B7%E6%AD%8C%E4%BA%9111.png)   
- 取得这个二维码的链接，粘贴到浏览器
- 打开客户端软件，在文末的分享链接里有
- `ShadowsocksR-dotnet4.0.exe` 我的是 win7 系统 ，点击这个.exe 后缀的文件
- 在任务栏中右键 二维码扫描 然后 就会自动 配置好 服务器的 端口号 ip 这些 
- 然后 把其他的 服务器信息删了 只保留你自己的 服务器信息
- 系统代理模式 选择 全局模式
- 代理规则 选择 绕过局域网 和 大陆
- 然后 就可以 访问 被墙的网站了 
- 注意 要把 谷歌访问助手屏蔽掉
#### 客户端 windows 安装的软件
[客户端软件和谷歌访问助手](https://pan.baidu.com/s/1raoibBA)  
密码： vytf