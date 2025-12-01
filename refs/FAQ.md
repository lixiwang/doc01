# 开发环境常见问题

[TOC]

## 科学上网

使用 Ghelper 进行科学上网，大幅度提高工作效率。
每月需要付出大约一杯咖啡的金钱 `17.59 UKD Per Month`，来获得便利。

> Ghelper 是一个浏览器插件，特别是针对开发者、跨边界工作者和研究者，是一个非常有价值的项目。这类插件可以极大地提高工作效率，促进跨平台协作，以及辅助研究和开发工作。

通过以下步骤实现：

- 前往官网 `https://ghelper.net/` 下载Ghelper插件。
- 下载完成后，打开Chrome浏览器，进入扩展程序管理器。
- 开启开发者模式，然后简单地将解压好的crx文件拖拽到扩展程序管理器中即可完成安装。
- 使用Ghelper插件前，你需要先注册一个账号。

注册并登录后，你就可以直接登录Google账户并访问Chrome商店了。需要注意的是，仅仅访问Google是不需要开通会员的。

然而，如果你希望通过该插件访问Google以外的其他受限制网站，会员功能可解锁访问受限制网站的权限。你可以选择开通会员功能。

安装 V2RayN，设置订阅
命令行运行：
netsh winhttp import proxy source=ie

## git 中文路径文件名问题

### Git中文路径问题

主要表现在以下几个方面：

- **中文文件名显示乱码**：在 Git 命令行界面中，中文文件名可能会显示为乱码。
- **中文路径无法创建**：在 Git 仓库中创建包含中文的文件夹或文件时，可能会遇到无法创建的问题。
- **中文路径无法识别**：在使用 Git 命令操作包含中文的路径时，可能会出现无法识别的情况。

### 解决Git中文路径问题的方法

修改 Git 配置，从而支持中文

- 关闭对路径的quote处理
- 关闭路径大小写不敏感
- 设置提交时使用utf-8编码
- 设置执行git log时将utf-8编码转换成gbk编码，可选

终端执行如下命令：

```sh
git config --global core.quotepath false
git config --global core.ignorecase false
git config --global i18n.commitencoding utf-8
git config --global i18n.logoutputencoding gbk
```

## github.com访问不稳定

### 原因分析

Github访问不稳定的主要原因包括：

- 路由节点不稳定  
 GitHub 服务器均位于海外，需要经过一系列的路由器和网络节点。路由节点不稳定会导致数据包丢失、延迟增加、甚至是连接断开等问题。

- DNS 污染
  通常是出于审查或广告推广的目的，恶意修改 DNS 查询结果，影响正常访问。

### 解决方法1： 修改HOSTS文件

1. 获取GitHub真实IP
通过 `https://www.ipaddress.com/` 获得真实 IP。

```python
github.com
assets-cdn.github.com
github.global.ssl.fastly.net
api.github.com
raw.githubusercontent.com
```

或者，使用命令：

```()
nslookup github.com 8.8.8.8  # 使用 Google DNS 查询
```

1. 修改Hosts文件

```()
# https://www.ipaddress.com/website/github.com/
140.82.112.3 github.com

# https://www.ipaddress.com/website/assets-cdn.github.com/
185.199.108.153 assets-cdn.github.com
185.199.109.153 assets-cdn.github.com
185.199.110.153 assets-cdn.github.com
185.199.111.153 assets-cdn.github.com

# https://www.ipaddress.com/site/fastly.net // github.global.ssl.fastly.net
151.101.1.6 github.global.ssl.fastly.net
151.101.65.6   github.global.ssl.fastly.net
151.101.129.6   github.global.ssl.fastly.net
151.101.193.6   github.global.ssl.fastly.net
```

1. 刷新 DNS 缓存：

- Windows：ipconfig /flushdns
- macOS/Linux：sudo dscacheutil -flushcache 或 sudo systemd-resolve --flush-caches

### 解决方法2：  使用加密 DNS 服务

通过加密 DNS（如 DNS-over-HTTPS 或 DNS-over-TLS）避免解析被劫持。

推荐方案：

- Cloudflare DNS（1.1.1.1）或 Google DNS（8.8.8.8）：
手动设置设备的 DNS 地址。

- DNSCrypt 或 DoH/DoT 工具：
使用 AdGuard DNS、NextDNS 等支持加密的 DNS 服务。
