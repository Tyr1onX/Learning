---
tags:
  - web
  - cache
  - cdn
  - http
status: understood
updated: 2026-08-08
---

# HTTP Cache / CDN / HTTP 版本

## 1. 强缓存

服务器可以返回：

```http
Cache-Control: max-age=3600
```

表示在这段新鲜期内，浏览器通常可以直接使用本地缓存，不必先向服务器确认资源有没有变化。

```text
缓存仍新鲜
→ 直接使用
→ 通常不发网络请求
```

因此如果服务器更新了同一个 URL，但客户端旧缓存仍在有效期内，用户可能继续拿到旧资源。

---

## 2. 协商缓存

缓存过期不等于必须重新下载整个文件。浏览器可以拿着版本信息向服务器确认。

### ETag / If-None-Match

首次响应：

```http
ETag: "abc123"
```

之后请求：

```http
If-None-Match: "abc123"
```

如果没变化：

```http
304 Not Modified
```

浏览器继续使用本地缓存。

如果资源变化，服务器返回：

```http
200 OK
ETag: "xyz789"

<new body>
```

### Last-Modified / If-Modified-Since

另一套机制：

```http
Last-Modified: Fri, 08 Aug 2026 01:00:00 GMT
```

之后：

```http
If-Modified-Since: Fri, 08 Aug 2026 01:00:00 GMT
```

基础理解：ETag 更像资源版本标识，Last-Modified 主要依据修改时间。

### 强缓存 vs 协商缓存

```text
强缓存
→ 不问服务器，直接用

协商缓存
→ 问服务器“变了吗？”
→ 没变：304 + 本地缓存
→ 变了：200 + 新资源
```

304 通常没有完整响应 Body，因此能节省带宽，但仍发生了网络往返。

---

## 3. no-cache 与 no-store

这是高频易错点：

```text
Cache-Control: no-store
→ 不要存储响应

Cache-Control: no-cache
→ 可以存
→ 但再次使用之前必须重新验证
```

`no-cache` 不是“没有缓存”。

---

## 4. Content Hash / Cache Busting

如果：

```text
/app.js
Cache-Control: max-age=31536000
```

服务器即使更新 `/app.js`，浏览器还可能继续使用旧版本。

现代前端构建通常把内容 Hash 放进文件名：

```text
app.a8f31c.js
```

内容变化后：

```text
app.f72bd9.js
```

URL 变了，浏览器会认为这是一个新资源，于是重新请求。

因此常见策略：

```text
index.html
→ 不做非常长期的强缓存 / 经常重新验证
→ 用来发现最新资源 URL

带 hash 的 JS / CSS / 图片
→ 可以长期强缓存
→ 内容一变，文件名也变
```

---

## 5. CDN

CDN = Content Delivery Network，内容分发网络。

核心思想：在全球 / 各区域部署边缘节点，把内容缓存到离用户更近的位置。

```text
User
↓
CDN Edge Node
↓ 必要时
Origin Server
```

### Cache Hit

```text
CDN 已有有效缓存
→ 直接返回用户
```

### Cache Miss

```text
CDN 没有有效缓存
→ 去源站拿资源
```

### 回源

CDN 向 Origin Server 获取原始资源的过程。

### TTL

TTL = Time To Live。

在 CDN 场景中可以理解为缓存内容在多长时间内仍可视为有效。DNS 中也有 TTL，但它表示 DNS 记录的缓存时间。

不要把 HTTP 里的 `max-age` 直接叫做某个“TTL Header”；它们概念相似，但具体字段不同。

### Purge / Invalidation

主动让 CDN 中的旧缓存失效。

```text
Origin 已更新
CDN 旧缓存 TTL 还没过期
↓
Purge / Invalidation
↓
旧缓存被清除 / 标记无效
↓
下一次请求回源获取新版
```

区别可先记为：

```text
TTL
→ 等自然过期

Purge / Invalidation
→ 主动让缓存立即失效

Content Hash
→ 换新 URL，绕过旧缓存
```

### CDN 与 DNS

用了 CDN 后，域名解析 / CDN 调度系统可能把用户导向合适的 CDN 基础设施或边缘节点，而不一定把所有用户直接指到源站 IP。

实际 CDN 调度还可能结合 Anycast、路由、网络质量、负载等信息。基础面试说“DNS / CDN 调度将用户导向合适边缘节点”即可。

---

## 6. HTTP/1.1

### Keep-Alive / Persistent Connection

核心：多个 HTTP 请求可以复用同一条 TCP 连接，避免每个资源都重新做 TCP 握手。

```text
TCP 建连
↓
GET HTML
↓
GET CSS
↓
GET JS
↓
继续复用连接
```

浏览器为了提高并发，在 HTTP/1.1 时代通常还会对同一 Origin 建立多条 TCP 连接。

---

## 7. HTTP/2

HTTP/2 的关键能力之一：Multiplexing，多路复用。

一条 TCP 连接中可以存在多个逻辑 Stream：

```text
TCP Connection
├─ Stream A → HTML
├─ Stream B → CSS
├─ Stream C → JS
└─ Stream D → Image
```

HTTP/2 把数据拆成 Frame，并允许不同 Stream 的 Frame 交错传输。

因此多个 HTTP 请求能在一条连接上并发推进，不必让一个大资源完整结束后才处理后面的资源。

### 为什么 HTTP/2 仍有队头阻塞？

因为底层仍然是 TCP：

```text
HTTP/2
↓
TLS
↓
TCP
```

TCP 对上层提供一条可靠、有序的连接级字节流。

如果中间一段 TCP 数据丢失：

```text
1～1000      ✓
1001～1500   丢失
1501～2000   ✓
```

后面的字节虽然已经到达，也要等待缺口恢复后才能以连续有序字节流交给上层。

多个 HTTP/2 Stream 共用同一条 TCP，因此一个 TCP 丢包可能让多个 Stream 一起受到影响。

这就是 TCP 层 Head-of-Line Blocking。

---

## 8. HTTP/3 / QUIC

层次：

```text
HTTP/3
↓
QUIC
↓
UDP
↓
IP
```

UDP 自身：

```text
不保证送达
不保证顺序
不自动重传
```

HTTP/3 仍然能可靠传输，是因为 QUIC 自己实现了：

```text
丢包检测与重传
流量控制
拥塞控制
多个 Stream
可靠传输
TLS 1.3 安全机制
```

QUIC 的不同 Stream 在可靠 / 有序处理上可以相对独立，因此一个 Stream 丢数据时，不需要因为 TCP 的连接级顺序约束把其他 Stream 一起卡住。

### Connection Migration

传统 TCP 连接与四元组紧密关联：

```text
源 IP + 源端口 + 目标 IP + 目标端口
```

手机从 Wi-Fi 切换到 5G 时，源 IP / 端口可能变化，原 TCP 连接通常需要重新建立。

QUIC 使用 Connection ID 标识逻辑连接，不完全依赖原始四元组，因此更有机会在网络路径改变后继续连接，这叫 Connection Migration。

### 为什么不能说“HTTP/3 快是因为 UDP 比 TCP 快”？

UDP 只是提供了更简单、灵活的底层接口。真正的收益来自 QUIC 在 UDP 之上重新设计了可靠传输、多 Stream、连接建立、丢包恢复、连接迁移等能力。

---

## 面试速记

```text
HTTP/1.1
→ Keep-Alive
→ 复用 TCP
→ 常开多条 TCP 提升并发

HTTP/2
→ 一条 TCP + 多 Stream
→ Multiplexing
→ 仍有 TCP Head-of-Line Blocking

HTTP/3
→ QUIC over UDP
→ QUIC 自己提供可靠传输
→ TLS 1.3
→ Stream 相对独立
→ Connection Migration
```
