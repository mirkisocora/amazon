
# Python 爬虫代理 IP 设置方法汇总

爬虫过程中，遇到强反爬网站时，设置随机 User-Agent 和代理 IP 是两个非常有效的解决方案。本文将详细介绍如何在 Python 的 Requests 和 Scrapy 中设置代理 IP，并分析不同代理的特点与应用场景。

---

## Proxy-Seller：高效的代理解决方案

**覆盖全球197个国家，提供超过2000万个住宅 IP**，Proxy-Seller 是当前最稳定且匿名性极高的住宅代理服务。

### 功能亮点：
- **支持 HTTP 和 HTTPS 协议**，提供旋转和静态代理选择。
- **精确到城市和 ISP 级别**，满足爬取特定区域数据的需求。
- 高达 **99.99% 的稳定性**，特别适合需要长期稳定使用的项目。

立即使用优惠码 **WQMKYZ_888908** 获取额外优惠！点击了解详情：  
☞ [https://bit.ly/proxy-seller-coupon](https://bit.ly/proxy-seller-coupon)

---

## 代理 IP 的概念及作用

代理服务器是用户与目标网站之间的中介，通过代理可以隐藏用户的真实 IP 地址，从而实现以下功能：

- **保护隐私**：隐藏真实 IP，防止数据被跟踪。
- **绕过地理限制**：访问被封锁的内容和区域。
- **提高爬虫效率**：避免因频繁访问被封禁。

---

## Requests 中代理 IP 的设置

### 基础代理设置

在 Requests 中，设置代理非常简单，只需在 `proxies` 参数中指定代理地址即可：

```python
proxies = {
    'http': 'socks5://127.0.0.1:1080',
    'https': 'socks5://127.0.0.1:1080'
}

response = requests.get('http://icanhazip.com', proxies=proxies)
print(response.text)
```

- **HTTP 代理**：仅支持 HTTP 网站。
- **HTTPS 代理**：仅支持 HTTPS 网站。

### 注意事项
- 请求类型需与代理协议匹配，否则代理将失效。
- 可通过随机选择代理池中的 IP 来提高匿名性。

---

## Scrapy 中代理 IP 的设置

在 Scrapy 中，可以通过以下两种方式设置代理。

### 方法一：自定义中间件

在 `middlewares.py` 中自定义代理中间件：

```python
class ProxyMiddleware:
    def process_request(self, request, spider):
        request.meta['proxy'] = 'https://127.0.0.1:8112'
```

并在 `settings.py` 中启用该中间件：

```python
DOWNLOADER_MIDDLEWARES = {
    'your_project.middlewares.ProxyMiddleware': 543,
}
```

### 方法二：使用付费代理

以 Proxy-Seller 为例，配置中间件代码如下：

```python
proxyServer = "http://http-dyn.abuyun.com:9020"
proxyUser = "你的代理账号"
proxyPass = "你的代理密码"

proxyAuth = "Basic " + base64.urlsafe_b64encode(bytes(f"{proxyUser}:{proxyPass}", "ascii")).decode("utf8")

class AbuyunProxyMiddleware:
    def process_request(self, request, spider):
        request.meta["proxy"] = proxyServer
        request.headers["Proxy-Authorization"] = proxyAuth
```

并设置限速以适应代理提供的速率：

```python
DOWNLOAD_DELAY = 0.2
AUTOTHROTTLE_ENABLED = True
```

---

## 代理类型及特点

### 1. HTTP 和 HTTPS 代理
- **HTTP 代理**：支持一般的 HTTP 流量。
- **HTTPS 代理**：适用于加密传输。

### 2. 旋转代理
- 随机更换 IP 地址，有效规避反爬措施。

### 3. 移动代理
- 模拟移动设备流量，适用于移动广告和 App 爬取。

---

## 使用付费代理的优势

相比免费代理，付费代理更加稳定和安全。例如，Proxy-Seller 提供的旋转代理可实现高效爬取，每次请求使用不同 IP，有效避免封禁。

```python
# Proxy-Seller 示例
proxyServer = "http://http-dyn.proxyseller.com:8080"
proxyUser = "user"
proxyPass = "password"

proxies = {
    'http': f"http://{proxyUser}:{proxyPass}@{proxyServer}",
    'https': f"http://{proxyUser}:{proxyPass}@{proxyServer}",
}

response = requests.get('http://icanhazip.com', proxies=proxies)
print(response.text)
```

---

## 推荐代理服务

- **Proxy-Seller**：支持多种类型代理，价格实惠，适合多场景使用。  
  [点击了解更多](https://bit.ly/proxy-seller-coupon)

- **阿布云**：动态 IP 性价比高，适合短期爬虫任务。

- **Scrapy-Proxies**：开源代理库，适合尝试多代理设置。

---

## 结论

在爬虫项目中，合理设置代理 IP 是规避反爬、提高爬取效率的关键。对于预算有限的新手，建议尝试稳定的付费代理，如 **Proxy-Seller**，它能有效提升项目的成功率。

立即使用 Proxy-Seller，享受稳定高速的代理体验！  
☞ [https://bit.ly/proxy-seller-coupon](https://bit.ly/proxy-seller-coupon)
