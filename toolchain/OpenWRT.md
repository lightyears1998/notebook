# OpenWRT

## DNS

- [在 OpenWrt 上配置 unbound 使用 DNS over TLS](https://www.rubyfish.cn/unbound-with-dnsmasq-on-openwrt)

## USB储存设备

- [OpenWRT: Using storage devices](https://openwrt.org/docs/guide-user/storage/usb-drives)
- [在USB设备上安装软件](http://tuntuntun.net/OpenWrt%E6%8C%82%E8%BD%BDUSB%EF%BC%8C%E5%9C%A8U%E7%9B%98%E4%B8%8A%E5%AE%89%E8%A3%85%E8%BD%AF%E4%BB%B6.html)

```sh
vi /etc/profile
source /etc/profie
```

指定Python的安装目录

```sh
opkg install python -d usb
opkg install python-pip -d usb  # 此后，不使用--user选项的Pip安装，也会安装到USB目录
```
