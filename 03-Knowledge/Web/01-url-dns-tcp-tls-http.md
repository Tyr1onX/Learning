---
tags:
  - web
  - network
  - http
status: understood
updated: 2026-08-08
---

# URL → DNS → TCP → TLS → HTTP

## 1. URL

示例：

```text
https://example.com:443/blog/article?id=123#comments
```

可以拆成：

```text
scheme   https
host     example.com
port     443
path     /blog/article
query    ?id=123
fragment #comments
```

HTTPS 默认端口通常是 443，HTTP 默认端口通常是 80。Fragment 通常只由浏览器本地处理，不随普通 HTTP 请求发送给服务器。

### 域名、IP、端口

```text
域名 / DNS → 找到机器或网络入口
IP          → 网络中的地址
Port        → 找到该机器上的具体服务
```

一台机器可以同时运行多个服务，例如 22 / SSH、80 / HTTP、443 / HTTPS、3306 / MySQL。

TCP 连接常用四元组区分：

```text
源 IP + 源端口 + 目标 IP + 目标端口
```

客户端的源端口通常是临时端口。

---

## 2. DNS

DNS 的核心目标：

```text
example.com
↓
找到对应 IP / 网络入口
```

简化解析流程：

```text
浏览器 / OS 等本地缓存
↓ 未命中
递归 DNS Resolver
↓ Resolver 缓存未命中
Root DNS
↓ 告诉你 .com 去哪里问
TLD (.com)
↓ 告诉你 example.com 权威 DNS 去哪里问
Authoritative DNS
↓
A / AAAA 等最终记录
```

注意：Root 通常不会直接返回目标网站最终 IP，而是给出下一层委派信息。

### 常见记录

```text
A     → IPv4
AAAA  → IPv6
CNAME → 别名
```

### TTL

TTL = Time To Live。DNS 解析结果可以被缓存一段时间，因此 DNS 记录更新后并不一定全网立即生效。

### Recursive 与 Iterative

用户通常把“帮我拿到最终结果”的任务交给递归 Resolver；Resolver 再去和 Root、TLD、Authoritative 等逐步查询。

---

## 3. 同一个 IP 为什么能放多个网站？

HTTP 层可以使用：

```http
Host: www.example.com
```

服务器据此做虚拟主机 / 路由。

HTTPS 还有一个先后顺序问题：HTTP 请求发送前 TLS 已经要建立安全连接并选择证书，因此 TLS ClientHello 里会带 SNI（Server Name Indication），让服务器知道客户端想访问哪个主机名。

```text
SNI  → TLS 层，帮助选择证书 / 站点
Host → HTTP 层，帮助 HTTP 路由
```

---

## 4. TCP

TCP 提供的是：

> 可靠、有序的字节流传输。

### 三次握手

```text
Client                Server
  | ---- SYN ---------> |
  | <--- SYN + ACK ---- |
  | ---- ACK ---------> |
```

核心作用：建立连接、确认双方通信能力、同步初始序列号等。

为什么不是简单两次？服务器需要知道客户端确实收到了自己的响应，否则服务端无法确认双向链路已经建立。

### 可靠性不是靠三次握手

后续可靠传输的重要机制包括：

```text
Sequence Number → 数据编号 / 有序
ACK             → 确认收到
Retransmission  → 丢失重传
Checksum        → 错误检测
Flow Control    → 不压垮接收方
Congestion Control → 不压垮网络
```

Keepalive / 应用层 heartbeat 不是 TCP 可靠传输的核心来源。

---

## 5. TLS / HTTPS

TLS 主要解决：

```text
Confidentiality → 保密性
Integrity       → 完整性
Authentication  → 身份认证
```

不是“提升 TCP 可靠性”。

简化层次：

```text
HTTP
↓
TLS
↓
TCP
↓
IP
```

HTTP/3 是例外，后续见 [[03-Knowledge/Web/03-cache-cdn-http-versions]]。

### 证书与 CA

服务器把证书提供给浏览器。浏览器验证证书链、域名、有效期等，以判断当前服务器身份是否可信。

私钥必须由服务器保护；公钥 / 证书可以公开。

现代 TLS 中常使用 ECDHE 等方式协商临时会话密钥，长期私钥更多承担签名 / 身份认证功能。后续大量数据使用对称加密提高效率。

---

## 6. HTTP Request / Response

典型流程：

```text
连接建立
↓
GET /index.html
↓
服务器返回 Response
↓
Status + Headers + Body
```

浏览器拿到 HTML 后，会解析其中引用的 CSS、JS、图片、字体等资源，并继续发起请求。

### 常见 Method

```text
GET    获取资源
POST   创建 / 处理
PUT    对明确资源做完整替换语义
PATCH  部分更新
DELETE 删除
```

### 幂等

同一个 PUT 多次执行后，资源最终状态通常相同，因此通常认为幂等。

POST 多次执行可能创建多个资源，因此通常不幂等。

DELETE 虽然第一次可能返回 200、第二次返回 404，但最终资源状态都为“不存在”，因此状态效果上仍可视为幂等。

### 常见状态码

```text
200 OK
201 Created
204 No Content
301 Permanent Redirect
302 Temporary Redirect
400 Bad Request
401 Unauthorized / Authentication 未通过
403 Forbidden / 已识别但没有 Authorization
404 Not Found
500 Internal Server Error
502 Bad Gateway
```

Authentication：你是谁？

Authorization：你能做什么？

---

## 7. 当前面试版主干

```text
解析 URL
↓
DNS 将域名解析到合适的网络入口 / IP
↓
建立 TCP（HTTP/1.1 / 2 常见情况）
↓
HTTPS 则进行 TLS 握手和证书验证
↓
发送 HTTP 请求
↓
服务器返回 HTML
↓
浏览器继续请求 CSS / JS / 图片等资源
↓
解析并进入浏览器渲染流程
```

渲染后半段见：[[03-Knowledge/Web/04-browser-rendering]]。

## 容易说错

```text
错误：TLS 提升 TCP 可靠性
正确：TCP 负责可靠有序传输；TLS 负责安全

错误：TCP 可靠性主要靠三次握手
正确：握手负责建连；ACK / 重传 / 序列号等负责可靠传输

错误：Root DNS 直接给最终网站 IP
正确：Root 通常给下一层委派信息
```
