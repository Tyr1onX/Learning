---
tags:
  - progress
  - session
  - review
  - web
  - browser
  - javascript
status: completed
updated: 2026-08-09
---

# 2026-08-09 Web / Browser 混合回顾

## 回顾目的

在新聊天窗口中对前一阶段 Web / Network / Browser Rendering / JavaScript-DOM 起点做无提示混合回忆，检查哪些知识已经稳定保留、哪些仍存在术语混淆。

## 回顾中表现稳定的内容

- URL 中能够区分 Path、Query、Fragment，并记住 Fragment 通常不发送给服务器；
- IP 与端口：IP 定位主机，Port 定位主机上的具体服务；
- TLS：能够说明保密性、完整性、身份认证，并区分 TLS 的安全职责与 TCP 的可靠传输职责；
- 401 / 403：能够区分未认证与已知身份但无权限；
- Cookie / Session：能够说明 session_id 常放在浏览器 Cookie 中，真实登录状态 / session 映射通常保存在服务端；
- JWT：理解 Payload 默认通常不是加密，签名用于防篡改；完整有效 JWT 被盗后仍可能被冒用；
- XSS / CSRF：能够说明 XSS 是恶意脚本在受信任站点上下文中执行，CSRF 是借用已有登录身份诱导发送请求；
- CORS：能够解释服务器即使返回 200，浏览器仍可能因为缺少允许跨源读取的响应头而不把响应暴露给前端 JS；
- `no-cache` / `no-store`：能够区分“可存但复用前验证”与“不存”；
- `max-age`、ETag / 304、CDN Hit / Miss / Origin 主干稳定；
- HTTP/2：理解多 Stream 仍共享同一 TCP 有序字节流，因此仍有 TCP 层 HOL；
- HTTP/3：理解 QUIC over UDP，可靠性由 QUIC 实现，并知道 QUIC 与 TLS 1.3 高度集成；
- HTML 与 DOM：能够说明 HTML 是标记文本，DOM 是浏览器解析后形成的对象树；
- `display:none` / `visibility:hidden` / `opacity:0`：主干基本稳定；
- Layout / Paint / Composite：能够按顺序解释主要职责；
- 普通 script 阻塞 Parser、`async` / `defer`、`DOMContentLoaded` / `load`：主干稳定；
- `document`：能够准确说明它是代表整个当前文档的 `Document` 对象，不是某个具体 HTML Element；
- `".title"`：能够准确说明它只是字符串，由 `querySelector()` 按 CSS Selector 语法解释；
- `querySelector()` 未匹配到元素时返回 `null`。

## 本次暴露出的仍需复习点

### DNS 术语

回忆时把 `TLD` 误说成 `TLS`。需要继续强化：

```text
Root → TLD → Authoritative
```

其中 TLD = Top-Level Domain；TLS = Transport Layer Security，两者完全不同。

### TCP 可靠传输机制

能够说出 ACK、重传、序列号，但第一次回答时仍把 SYN / 三次握手混入“可靠传输机制”。需要继续分箱：

```text
建连：SYN / SYN+ACK / ACK
可靠传输：Sequence Number + ACK + Retransmission（以及校验、流控、拥塞控制等）
```

### JWT 术语

第一次表述用了“解密”，应继续固定为：常见 JWT Payload 是编码而非默认加密，因此是“解码读取”，不是“解密”。

### Content Hash

理解新 URL 会绕过旧强缓存，但曾表述为“自动清除旧缓存”。需要固定：旧缓存可以仍然存在；关键是内容变化导致文件名 / URL 变化，新 URL 不会命中旧 URL 的缓存。

### Browser Performance 术语

能够解释：

```text
写布局 → 立即读取真实几何值 → 浏览器必须先算最新 Layout
```

但 `Forced Synchronous Layout` 仍不能稳定主动说出。

能够记得“布局抖动”，并能想起 `Layout th...`，但完整术语 `Layout Thrashing` 仍需间隔复习。

另外要继续固定：

```text
transform / opacity
→ CSS 属性

Composite
→ 浏览器渲染阶段
```

不能说“transform 一般只触发 transform”；更准确是 transform 在合适情况下可避免 Layout / Paint，主要由 Composite 处理。

## 当前状态判断

本次回顾不急于把更多主题升级到 `interview-ready`。Web / Browser 主干多数保持 `understood`；DNS/TCP/JWT/Content Hash 中出现的是可纠正的术语或机制边界混淆；Forced Synchronous Layout / Layout Thrashing 继续保持 `learning`。

JavaScript + DOM 仍处于系统学习起点。虽然 `document / querySelector / selector string / null` 已能正确回答，但尚未完成 `const / let`、值与类型、对象、函数等语言基础，因此不提前判为完整掌握。

## 下一步

继续当前主线：

```text
const / let
→ JavaScript 的值与基本类型
→ 对象与属性访问
→ 函数 / 方法
→ DOM Element
→ textContent / style
→ Event / addEventListener
→ Promise / async-await / Event Loop
→ fetch / JSON / API
→ Backend
```
