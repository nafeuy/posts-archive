# H3C NX30 Pro刷Openwrt

1. 路由器需要连网，通过 telnet 连接路由器，地址`192.168.124.1`，端口号`99`，用户名 **H3C**，密码是路由器后台登录密码，然后运行以下命令开启**SSH**
```
curl -o /tmp/dropbear.ipk https://downloads.openwrt.org/releases/packages-19.07/aarch64_cortex-a53/base/dropbear_2019.78-2_aarch64_cortex-a53.ipk
opkg install /tmp/dropbear.ipk
/etc/init.d/dropbear enable
/etc/init.d/dropbear start
```
2. 运行以下命令，备份原厂固件到tmp目录下，大小大概是60多MB
```
dd if=/dev/mtd5 of=/tmp/backup.img
```
3. 用 scp 将 uboot.bin 传到路由器的`/tmp`目录，scp 端口号`22`，用户名和密码依旧是第一步

4. 运行以下命令刷入 uboot，此 uboot 可以引导原厂固件
```
mtd write /tmp/uboot.bin FIP
```
5. 拔掉路由器电源，按住路由器背后的 reset 按钮不放再插入电源，10s 后松开 reset，电脑有线连接路由器任意 lan 口，并设置电脑固定ip`192.168.1.2`，子网掩码`255.255.255.0`，网关`192.168.1.1`，浏览器地址栏输入`192.168.1.1`即可进入 uboot 刷机界面

6. 刷机界面选择固件，然后点击 upload，等待上传完成后点击 update，路由器会自动刷入并重启，记得改回电脑ip为自动获取

7. 浏览器访问默认ip`192.168.6.1`，用户名 root，密码为 password
