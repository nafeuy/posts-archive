# Wireguard搭建虚拟个人网络（以腾讯云轻量应用服务器为例）

## 手动安装Wireguard

### 安装Wireguard（以ubuntu20.04为例）
```
#root权限
sudo -i

#安装wireguard软件
apt install wireguard resolvconf -y

#开启IP转发
echo 'net.ipv4.ip_forward = 1' | tee -a /etc/sysctl.conf
echo 'net.ipv6.conf.all.forwarding = 1' | tee -a /etc/sysctl.conf
sysctl -p /etc/sysctl.conf
```

### 进入配置存储路径，调整目录权限
```
chmod 0777 /etc/wireguard
cd /etc/wireguard

#调整目录默认权限
umask 077
```

### 生成服务器秘钥
```
#生成私钥
wg genkey > server.key

#通过私钥生成公钥
wg pubkey < server.key > server.key.pub

# 你也可以一次性完成
wg genkey | tee server.key | wg pubkey > server.key.pub
```

### 生成客户端(client1)秘钥
```
#生成私钥
wg genkey > client1.key

#通过私钥生成公钥
wg pubkey < client1.key > client1.key.pub
```

### 创建服务器配置文件
```
echo "
[Interface]
PrivateKey = $(cat server.key) #获取服务端私钥
Address = 10.0.0.1 #本机虚拟局域网IP
ListenPort = 50820
DNS = 119.29.29.29

PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -A FORWARD -o wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -D FORWARD -o wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
#注意eth0需要为本机网卡名称

[Peer]
PublicKey = $(cat client1.key.pub) #获取客户端公钥
AllowedIPs = 10.0.0.2/32 #指定客户端IP" > wg0.conf
```

### 增加客户端client2
```
#生成私钥
wg genkey > client2.key

#通过私钥生成公钥
wg pubkey < client2.key > client2.key.pub

#将peer公钥加入wg0.conf配置
echo "
[Peer]
PublicKey =  $(cat client2.key.pub) #获取client2公钥
AllowedIPs = 10.0.0.3/32 #指定给客户端client2的IP" >> wg0.conf
```

### (可选)设置服务器开机自启动Wireguard
```
systemctl enable wg-quick@wg0
```

### 启动wireguard
```
#启动wg0
wg-quick up wg0
#关闭wg0
wg-quick down wg0
```

### 创建客户端配置（以client1为例）
```
echo "
[Interface]
PrivateKey = $(cat client1.key) #获取客户端私钥
Address = 10.0.0.2 #前文指定的客户端IP
DNS = 119.29.29.29

[Peer]
PublicKey = $(cat server.key.pub) #获取服务端公钥
AllowedIPs = 10.0.0.0/24 #允许的服务器IP，/24允许整个网段
Endpoint = 公网IP:50820 #服务器公网IP+端口
PersistentKeepalive = 25 #连接保活间隔，单位为秒" > client1.conf
```



## Docker安装Wireguard
### 通过容器安装wg-easy
```
docker run -d \
  --name=wg-easy \
  -e WG_HOST=123.123.123.123 (🚨这里输入服务器的公网IP) \
  -e PASSWORD=passwd123 (🚨这里输入你的密码) \
  -e WG_DEFAULT_ADDRESS=10.0.8.x （🚨默认IP地址）\
  -e WG_DEFAULT_DNS=114.114.114.114 （🚨默认DNS）\
  -e WG_ALLOWED_IPS=10.0.8.0/24 （🚨允许连接的IP段）\
  -e WG_PERSISTENT_KEEPALIVE=25 （🚨重连间隔）\
  -v ~/.wg-easy:/etc/wireguard \
  -p 51820:51820/udp \
  -p 51821:51821/tcp \
  --cap-add=NET_ADMIN \
  --cap-add=SYS_MODULE \
  --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
  --sysctl="net.ipv4.ip_forward=1" \
  --restart unless-stopped \
  weejewel/wg-easy
```

### 更新容器命令
```
docker stop wg-easy
docker rm wg-easy
docker pull weejewel/wg-easy
```
