## 检查内核版本
Linux内核4.9版本已经内置BBR，因此首先检查内核版本
```
uname -r
```
检查是否启用了BBR
```
sysctl net.ipv4.tcp_available_congestion_control
sysctl net.core.default_qdisc
```
返回结果中没有BBR，说明没有启用
## 开启BBR
```
echo "net.ipv4.tcp_congestion_control= bbr" >> /etc/sysctl.conf
echo "net.core.default_qdisc = fq" >> /etc/sysctl.conf
sysctl -p
```
检查是否开启成功
```
sysctl net.ipv4.tcp_available_congestion_control
sysctl net.core.default_qdisc
```
返回结果中有BBR，说明已启用
## 检测是否在运行
现在内核中已经开启BBR功能，检测一下是否正在运行
```
lsmod | grep bbr
```
看到`tcp_bbr`说明 BBR 已经成功在运行了
