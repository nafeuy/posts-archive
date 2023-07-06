---
title: 为Git设置代理
date: 2023-02-27 12:42:19
tags:
---

> 以**Clash**为例  

# HTTP/HTTPS协议  
使用 HTTP / HTTPS 传输协议连接到 Git 仓库的 URL 实例如下：  
```
http://github.com/example/example.git
https://github.com/example/example.git
```
 
+ 全局代理  
```
git config --global http.proxy http://127.0.0.1:7890
```
+ 只代理Github  
```
git config --global http.https://github.com.proxy http://127.0.0.1:7890
```
+ 撤销代理  
```
git config --global --unset http.proxy
git config --global --unset http.https://github.com.proxy
```


# SSH协议  
使用 SSH 传输协议连接到 Git 仓库的 URL 实例如下：
```
git@github.com:example/example.git
ssh://git@github.com/example/example.git
```

以下内容仅限**Windows**端Git  
+ 编辑`C:\Users\example\.ssh\config`，输入以下内容：  
```
Host github.com
    User git
    ProxyCommand connect -H 127.0.0.1:7890 %h %p
```
> 解释：
> + Host 后面 接的 github.com 是指定要走代理的仓库域名。
> + 在 ProxyCommand 中，Windows 用户用的是 connect 。
> + -H 选项的意思是 HTTP 代理。
> + 在调用 ProxyCommand 时，％h 和 ％p 将会被自动替换为目标主机名和 SSH 命令指定的端口（ %h 和 %p 不要修改，保留原样即可）。  

+ 撤销代理：删除添加的内容  
