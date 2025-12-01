# 声明
Added for test.
## 系统性

思想之火花如同茫茫宇宙之星辰，散落着，毫无可用价值。

## github.com访问不稳定

### 原因

- 路由节点不稳定
  
  GitHub 服务器均位于海外，需要经过一系列的路由器和网络节点。路由节点不稳定会导致数据包丢失、延迟增加、甚至是连接断开等问题。

- DNS 污染
  通常是出于审查或广告推广的目的，恶意修改 DNS 查询结果，影响正常访问。

### 解决方法1： 修改HOSTS文件

(1) 获取GitHub真实IP

通过https://www.ipaddress.com/

```()
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

(2) 修改Hosts文件

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

(3) 刷新 DNS 缓存：

- Windows：ipconfig /flushdns
- macOS/Linux：sudo dscacheutil -flushcache 或 sudo systemd-resolve --flush-caches

### 解决方法2：  使用加密 DNS 服务

通过加密 DNS（如 DNS-over-HTTPS 或 DNS-over-TLS）避免解析被劫持。
推荐方案：
Cloudflare DNS（1.1.1.1）或 Google DNS（8.8.8.8）：
手动设置设备的 DNS 地址。

DNSCrypt 或 DoH/DoT 工具：
使用 AdGuard DNS、NextDNS 等支持加密的 DNS 服务。
