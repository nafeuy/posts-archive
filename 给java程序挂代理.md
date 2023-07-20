# 给java程序挂代理

+ 命令行挂Socks5代理

启动Socks5代理命令如下
```
java -DsocksProxyHost=127.0.0.1 -DsocksProxyPort=7890 -jar xxxxx.jar
```
其中socksProxyHost是Socks5代理的IP地址，socksProxyPort是Socks5代理的端口号。socksProxyVersion版本号是5或者是4，默认是5版本，也就是Socks5代理，这里也可以指定
* * * * *
+ 命令行挂HTTP代理

如果想对一个Java程序设置HTTP代理，按如下所示设置
```
java -Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=7890 -Dhttps.proxyHost=127.0.0.1 -Dhttps.proxyPort=7890 -Dhttp.nonProxyHosts="*.example.com|localhost" -jar xxxxx.jar
```
如果想使用代理访问HTTP的URL，则必须使用`http.proxyHost` `http.proxyPort`，如果想用代理访问HTTPS的URL，则必须使用`https.proxyHost` `https.proxyPort`， 如果想同时抓HTTP、HTTPS的URL访问的话，以上4项必须设置，缺一不可

`http.proxyHost`是HTTP代理的IP地址，`http.proxyPort`是HTTP代理的端口，`https.proxyHost`是HTTPS代理的IP地址，`https.proxyPort`是HTTPS代理的端口

`http.nonProxyHosts`（此选项对于http/https型URL均适用），用于指定哪些IP地址可以直连网络，不走HTTP/HTTPS代理，`*`是IP地址的通配符，按照`|`分割每个IP段，前后加上双引号包裹起来
* * * * *
+ 如果使用系统代理
```
java -Djava.net.useSystemProxies=true -jar xxxxx.jar
```
那么 xxxxx.jar 程序将会走系统代理
