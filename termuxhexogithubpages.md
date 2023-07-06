---
title: 利用Termux + Hexo + Github搭建博客
date: 2023-02-10 12:15:54
tags:
---

> 我使用的Termux版本为0.118.0  
> 手机已root（用以访问`/data`目录）  
> Github仓库已开启Pages功能  
> **首先将Termux更换为清华源，这一步不过多赘述**  

## 需要安装的组件  

1. 输入`pkg install openssh`以安装SSH  
2. 输入`pkg install git`以安装Git  
3. 输入`pkg install nodejs-lts`以安装Node.Js  
4. 输入`npm install hexo-cli -g`以安装Hexo  
    * 更换npm国内镜像`npm config set registry https://registry.npmmirror.com`  

**至此所有准备工作就完成了**  

## 开始配置  

### 配置用户名和邮箱  

```
git config --global user.name "github用户名"
git config --global user.email "github注册邮箱"
```

### 生成SSH密钥  

```
ssh-keygen -t rsa -C "github注册邮箱"
```

> 生成密钥这一步输入命令后需要回车三次  

然后你可以在`/data/data/com.termux/files/home/.ssh/`目录下找到`id_rsa`和`id_rsa.pub`两个文件  

我们需要将`id_rsa.pub`文件里的所有内容复制下来，注意是所有内容，包括空格和换行，建议直接长按全选，避免遗漏  

### 打开Github的[密钥](https://github.com/settings/keys)设置  

点击`New SSH key`，填写`Title`和`Key`，`Title`可以随便填写，将刚才复制的`id_rsa.pub`的内容粘贴到`Key`处，然后点击`Add SSH key`保存  

### 开始我们的博客  

使用`hexo init`命令生成一个博客目录，为方便建议直接取名为`blog`，即`hexo init "blog"`  

**进入该博客目录**  

输入`npm install hexo-deployer-git --save`以安装Git部署  

完成后，在博客目录的`_config.yml`文件的最后面deploy部分输入以下内容  

```
deploy:
  type: git
  repo: 
  branch: main
```
* `repo`处填写仓库的**SSH链接**  

* `type`和`repo`和`branch`的冒号后都有一个空格  

![p1](https://s2.loli.net/2023/02/09/wzx5TMpFcAyjEHN.png)  

### 博客常用命令  

使用`hexo new "文章标题"`命令以创建一篇文章，文章保存在博客目录下`/source/_post`文件夹中，为md后缀  

使用`hexo g`命令以生成静态网页  

使用`hexo s`命令以开启本地服务器，开启本地服务器后可以访问`http://localhost:4000`查看网页（`Ctrl`+`C`关闭本地服务器）  

使用`hexo d`命令以部署到远程仓库  

使用`hexo clean`命令以清除缓存  

当我们写完文章后，使用`hexo clean && hexo d`命令可以一键完成部署  

### 访问你的Pages页面就能看到你的博客了  