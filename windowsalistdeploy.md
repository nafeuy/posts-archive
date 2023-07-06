---
title: 记录一下我在Windows上部署AList的经验
date: 2023-02-10 13:40:06
tags:
---

# 配置  
从AList的[Releases](https://github.com/alist-org/alist/releases)下载Windows端的AList，我的系统是64位的，所以选择<u>alist-windows-amd64.zip</u>  

解压后可以得到一个**alist.exe**  

在**alist.exe**所在目录打开一个命令行窗口，输入`alist.exe server`启动AList服务  

首次运行会输出初始密码，程序默认监听5244端口，现在打开`http://127.0.0.1:5244`就可以看见登陆页面了  

用户名为**admin**，密码即为输出的初始密码  

如果不想在运行时出现黑乎乎的命令行窗口，可以使用`vbs`启动AList服务  

在**alist.exe**所在目录创建一个`.vbs`后缀的脚本文件，用文本编辑器编辑，输入以下内容并保存：  
```
Set ws = CreateObject("WScript.Shell")
ws.run "alist.exe server",vbhide
Set ws = Nothing
WScript.Quit
```  
现在双击这个`vbs`文件就能无窗口启动AList服务了  

如果想实现开机自启，右键这个`vbs`文件，创建快捷方式，再右键这个快捷方式，剪切  

`Win`+`R`打开**运行**，输入`shell:startup`打开**启动**文件夹，粘贴刚才的快捷方式，就能实现开机自启了