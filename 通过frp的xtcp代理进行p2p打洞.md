# 通过frp的xtcp代理进行p2p打洞

frp 提供了一种新的代理类型`xtcp`用于应对在希望传输大量数据且流量不经过服务器的场景

`xtcp`需要在两边都部署 frpc 用于建立直接的连接

**XTCP** 并不能穿透所有类型的 NAT 设备

本文以SSH为例
1. 在需要暴露到外网的机器上部署 frpc，且配置如下
```
[common]
server_addr = x.x.x.x
server_port = 7000
# 当默认的 stun server 不可用时，可以配置一个新的
# nat_hole_stun_server = xxx

[p2p_ssh]
type = xtcp
# 只有 sk 一致的用户才能访问到此服务
sk = abcdefg
local_ip = 127.0.0.1
local_port = 22
```

2. 在想要访问内网服务的机器上也部署 frpc，且配置如下
```
[common]
server_addr = x.x.x.x
server_port = 7000
# 当默认的 stun server 不可用时，可以配置一个新的
# nat_hole_stun_server = xxx

[p2p_ssh_visitor]
type = xtcp
# xtcp 的访问者
role = visitor
# 要访问的 xtcp 代理的名字
server_name = p2p_ssh
sk = abcdefg
# 绑定本地端口用于访问对面机器的 ssh 服务
bind_addr = 127.0.0.1
bind_port = 6000
# 当需要自动保持隧道打开时，设置为 true
# keep_tunnel_open = false
```
开启 frp 连接，在打洞成功后通过IP地址`127.0.0.1`和端口`6000`进行SSH连接，就能访问对面的SSH服务了
