# 如何在 GitHub 正确地使用 Curl 下载文件？  

下载与原始文件同名的文件的常用语法非常简单：

```
curl -O URL_of_the_file
```

这在大多数情况下都有效，但是，有时从 GitHub 或 SourceForge 下载文件时，它不会获取正确的文件  

## **使用 curl 正确下载存档文件**  

这里的问题是 URL 重定向到实际的存档文件，为此，需要使用其他选项  

```
curl -JLO URL_of_the_file
```

选项可以按任何顺序排列  

这是基于 curl 命令手册页的选项的快速说明：  
J：此选项告诉 -O, --remote-name 选项使用服务器指定的 Content-Disposition 文件名，而不是从 URL 中提取文件名  
L：如果服务器报告请求的页面已移动到不同的位置（用 Location: 标头和 3XX 响应代码指示），此选项将使 curl 在新位置重做请求  
O：使用此选项，无需指定下载的输出文件名  
