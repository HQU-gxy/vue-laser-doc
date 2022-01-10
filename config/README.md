# 网关配置

## 准备条件

- [RAK2245 Pi HAT WisLink LPWAN Concentrator](https://docs.rakwireless.com/Product-Categories/WisLink/RAK2245-Pi-HAT/Overview/#product-description)
- [Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) 4B or 3B; maybe Raspberry Pi Zero W is also compatible.
- 16 GB 或以上 SD Card + 读卡器
- Windows/Linux/MacOS 兼容的 PC 机

## 刷入树莓派固件

下载 [balenaEtcher](https://www.balena.io/etcher/), 或者其他可以刷入树莓派固件至SD卡的工具.

从[此处](https://downloads.rakwireless.com/LoRa/RAK2245-Pi-HAT/Firmware/RAK2245_Latest_Firmware.zip)下载所需固件/系统. 请勿刷写树莓派官方的固件/系统,
虽然这是可行的, 但是不建议.

亦可以从 [downloads.rakwireless.com](https://downloads.rakwireless.com/LoRa/RAK2245-Pi-HAT/Firmware/) 此处获取所需的固件和详细资料.

如果你不喜欢预先安装的系统, 也可以从
[RAKWireless/rak_common_for_gateway](https://github.com/RAKWireless/rak_common_for_gateway)获取 RAK 网关的辅助工具, 将其安装至任意已经安装系统的树莓派,
安装过程参照其文档, 在此不再赘述.

刷入过程不赘述, 参考 [balenaEtcher](https://www.balena.io/etcher/).

## 配置 RAK 网关

参照
[RAK2245 Pi HAT Quick Start Guide](https://docs.rakwireless.com/Product-Categories/WisLink/RAK2245-Pi-HAT/Quickstart/#configuring-the-gateway),
这里只做简单说明.

**Before powering the Raspberry Pi 3B+ or 4, you should connect the LoRa and GPS antennas. Not doing so might damage the boards.**

**在给树莓派上电之前, 你应该连接LoRa和GPS天线. 如果不连接, 可能会损坏树莓派.**

### 连接到树莓派

通常有以下几种方式连接树莓派

- [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) (SSH) 处于同一网络环境时
- 显示输出 -- [DisplayPort](https://en.wikipedia.org/wiki/DisplayPort)/[HDMI](https://en.wikipedia.org/wiki/HDMI)
- [RPi Serial Connection](https://elinux.org/RPi_Serial_Connection) 串口控制台

当然, 也可以通过 [USB On-The-Go](https://en.wikipedia.org/wiki/USB_On-The-Go) 加上 [Android Debug Bridge](https://developer.android.com/studio/command-line/adb) 连接树莓派, 但需要额外配置, 在此不赘述.

#### 查找树莓派 IP

在连入同一网络环境 (以太网/Wi-Fi) 下时, 可以使用 [mDNS](https://datatracker.ietf.org/doc/html/rfc6762) 直接访问树莓派, 使用 `主机名.local` 连接即可 (树莓派默认的主机名是`raspberrypi`, 但 RAK 的定制固件的主机名似乎是 `rak-gateway`).

更加直接/暴力的方式是使用 [Nmap](https://nmap.org/) 扫描开放的 22 端口, 当然前提是你的树莓派已经开放了`ssh`端口.

### 初始配置

假设你已经进入了 [Shell 环境](https://en.wikipedia.org/wiki/Unix_shell), 并且配置了网络环境. (如何连接 Wi-Fi 在此不再赘述)

```bash
sudo gateway-config
```

你会进入一个 TUI 环境, 在此可以设置网关的各种参数.

![RAK Config](../fig/setup_rak_gateway.jpg)

选择 `Setup RAK Gateway LoRa Concentrator` => `Server is Chirpstack` => `ChirpStack Channel-plan configuration` => `Server IP` 为默认的 `127.0.0.1`.

如果需要启用 [Adaptive Data Rate (自适应数据传输速率)](https://www.thethingsnetwork.org/docs/lorawan/adaptive-data-rate/) 功能, 可以选择 `Chirpstack ADR Configure` => `Enable ADR`.

此时使用外部浏览器访问 `http://树莓派的IP:8080/` 即可访问 [ChirpStack](https://www.chirpstack.io/) 的网关配置界面.

![ChirpStack Gateway Config](../fig/chirpstack-ui.png)

网关界面的介绍在此不再赘述, 参照 [ChirpStack Application Server](https://www.chirpstack.io/application-server/) 的文档.

## 安装 Java 后端服务器

假设你已经配置好了 [Raspbian 源镜像](https://mirrors.ustc.edu.cn/help/raspbian.html)

项目源码位于 [HQU-gxy/vue-laser-backend](https://github.com/HQU-gxy/vue-laser-backend)

安装 JDK 和 MariaDB/MySQL 数据库.

```bash
sudo apt update
sudo apt install default-jdk mariadb-server
```

切换至 `~` 目录 (`$HOME`)

```bash
cd ~
```

### 数据库配置

用 `wget` 亦可

```bash
curl https://raw.githubusercontent.com/HQU-gxy/vue-laser-backend/master/sql/jiguang.sql -O
```

若出现 `curl: (35) OpenSSL SSL_connect: Connection reset by peer in connection to raw.githubusercontent.com:443` 检查你的代理配置, 或者从源码仓库中的 [sql/jiguang.sql](https://github.com/HQU-gxy/vue-laser-backend/blob/master/sql/jiguang.sql) 下载, 然后使用 SFTP 或者其他方法的上传到树莓派.

### 启动服务器

```bash
curl https://github.com/HQU-gxy/vue-laser-backend/releases/download/v0.0.1/target.zip -LO
```

若下载失败, 检查你的代理配置, 中国大陆网络环境问题不再赘述.
