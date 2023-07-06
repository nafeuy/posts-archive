---
title: 通过手机流量的公网ipv6，利用Termux和frp实现内网穿透
date: 2023-02-20 09:43:08
tags:
---

现在手机流量基本都是公网ipv6地址了，是否可以用Termux配合frp实现内网穿透呢  

> Termux 0.118.0  
> frp 0.47.0  

+ **ipv4无法访问纯ipv6，本文通过ipv6架设的内网穿透并无太大作用，大部分设备的ipv6本身就是公网地址**  

# 准备  

打开[6.ipw.cn](http://6.ipw.cn),显示的便是你访问外网的ipv6地址  
<img src="https://s2.loli.net/2023/02/20/xHP7dCqG4rOoLBk.jpg" height="800px" width="360px" >  

进入手机的**状态信息**，找到**IP地址**，确认ipv6地址是否与网页显示的一致，如果一致，则说明你的是公网ipv6地址  
<img src="https://s2.loli.net/2023/02/20/Y3lyKuxAwbFNigP.jpg" height="800px" width="360px" > <img src="https://s2.loli.net/2023/02/20/j9QgZUw4iEaPYIM.jpg" height="800px" width="360px" >  

# 配置  

使用`wget`在frp的[releases](https://github.com/fatedier/frp/releases)下载正确版本的frp，因为是在Termux上部署，所以选择<u>frp_0.47.0_linux_arm64.tar.gz</u>  

解压后进入frp的文件夹，ls可以看到以下文件  
<img src="https://s2.loli.net/2023/02/20/GSRcY7eTW8qmozh.jpg" height="800px" width="360px" >  

使用`./frps -c ./frps.ini`命令启动服务；默认监听端口为`7000`  
<img src="https://s2.loli.net/2023/02/20/bVPS8EIJwTY4p2f.jpg" height="800px" width="360px" >  

若有需要，可以使用vim编辑服务端配置文件`frps.ini`(没有vim请使用`pkg install vim`命令安装)，关于frp服务端配置请自行了解  

# 客户端配置  

编辑客户端的`frpc.ini`文件，在`server_addr`处填写你的ipv6地址；未修改服务端配置文件的情况下，`server_port`处填写服务端默认的`7000`，关于客户端详细配置请自行了解  
![p](https://s2.loli.net/2023/02/20/ildYuentw6skhNy.png)  

我将AList进行了内网穿透，效果如下  
![p](https://s2.loli.net/2023/02/20/QXjYP3sKDLvHoJr.png)  
![p](https://s2.loli.net/2023/02/20/fj9pLrksMYeNQxJ.jpg)
