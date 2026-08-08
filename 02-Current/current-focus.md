---
tags:
  - current
  - learning
status: active
updated: 2026-08-08
---

# 当前学习焦点

## 当前主线

正在补齐 Web / 网络 / 浏览器基础，来源是 2026-08-07 的一次真实前端 / 全栈方向面试暴露出的基础缺口。

### 已经连续学过

- URL 结构、域名、IP、端口；
- DNS 递归解析、Root / TLD / Authoritative、TTL、A / AAAA / CNAME；
- SNI 与 HTTP `Host` 的层次区别；
- TCP 三次握手、序列号、ACK、重传、可靠有序字节流；
- TLS 的保密性、完整性、身份认证、证书、CA、非对称 + 对称加密；
- HTTP Methods、状态码、幂等；
- Cookie / Session / JWT / Access Token / Refresh Token；
- XSS / CSRF / SameSite / Same-Origin / CORS / Preflight；
- HTTP 强缓存 / 协商缓存、ETag / 304、`no-cache` / `no-store`；
- Content Hash、CDN、TTL、Cache Hit / Miss、回源、Purge / Invalidation；
- HTTP/1.1 Keep-Alive、HTTP/2 Multiplexing、TCP Head-of-Line Blocking；
- HTTP/3、QUIC over UDP、TLS 1.3、Connection ID / Connection Migration。

详见：

- [[03-Knowledge/Web/01-url-dns-tcp-tls-http]]
- [[03-Knowledge/Web/02-cors-auth-security]]
- [[03-Knowledge/Web/03-cache-cdn-http-versions]]

## 正在学习

### Browser Rendering Pipeline

下一段从这里继续：

```text
HTML → DOM
CSS → CSSOM
DOM + CSSOM
→ Render Tree / render structure
→ Layout
→ Paint
→ Composite
```

重点追问：

- HTML 与 DOM 有什么区别？
- `display: none` 为什么 DOM 中仍可能存在，但不参与正常布局？
- Layout / Reflow 与 Paint / Repaint 有什么区别？
- 为什么动画常推荐 `transform` / `opacity`？
- JavaScript 修改 DOM / Style 后浏览器可能做哪些工作？
- 脚本加载为什么可能影响 HTML 解析？`defer` / `async` 怎么区别？

对应笔记：[[03-Knowledge/Web/04-browser-rendering]]

## 当前不要跳过的薄弱点

1. 刚学会的内容容易在术语上说散，需要继续做口头回忆题。
2. JWT 必须牢记“常见签名 JWT ≠ 加密”；Payload 通常可读，签名负责防篡改。
3. TCP 的可靠传输不能归因于“三次握手 / 心跳”，核心是序列号、ACK、重传、流控、拥塞控制等。
4. CORS 不是认证，也不是 CSRF 防护；`200 OK` 与“JS 能否跨源读取响应”是两层判断。
5. HTTP/2 的多路复用没有消灭 TCP 层队头阻塞。
6. Diff / 动态规划仍是明显薄弱项，后续必须专项补。

## 下一步顺序

```text
Browser Rendering
→ script / defer / async
→ JavaScript 执行模型与 Event Loop
→ HTML / CSS / JS 系统基础
→ Framework 核心概念
→ Backend / Full Stack
→ Data Structures & Algorithms
→ Engineering / Security / Performance
```
