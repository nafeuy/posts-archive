# Debian12替换为USTC源  

```
echo "# 默认注释了源码仓库，如有需要可自行取消注释
deb http://mirrors.ustc.edu.cn/debian bookworm main contrib non-free non-free-firmware
# deb-src http://mirrors.ustc.edu.cn/debian bookworm main contrib non-free non-free-firmware
deb http://mirrors.ustc.edu.cn/debian bookworm-updates main contrib non-free non-free-firmware
# deb-src http://mirrors.ustc.edu.cn/debian bookworm-updates main contrib non-free non-free-firmware

# backports 软件源，请按需启用
deb http://mirrors.ustc.edu.cn/debian bookworm-backports main contrib non-free non-free-firmware
# deb-src http://mirrors.ustc.edu.cn/debian bookworm-backports main contrib non-free non-free-firmware

deb http://mirrors.ustc.edu.cn/debian-security/ bookworm-security main contrib non-free non-free-firmware
# deb-src http://mirrors.ustc.edu.cn/debian-security/ bookworm-security main contrib non-free non-free-firmware" | tee /etc/apt/sources.list
```