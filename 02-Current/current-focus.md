---
tags:
  - current
  - learning
status: active
updated: 2026-08-08
---

# 当前学习焦点

## 当前主线

正在沿着“Web 请求完整链路”补齐 Web / 浏览器 / 前端 / 后端基础。学习方式以理解现象为主，再补准确术语；不要把只见过一次的 API 名称当作已经掌握。

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
- HTTP/3、QUIC over UDP、TLS 1.3、Connection ID / Connection Migration；
- 浏览器渲染第一轮：HTML → DOM、CSS → CSSOM、Layout、Paint、Composite；
- `display:none` / `visibility:hidden` / `opacity:0` 的区别；
- `transform` / `opacity` 与动画性能的基本原因；
- 普通 `script`、`async`、`defer`；
- `DOMContentLoaded` 与 `load`；
- CSS 通常不直接阻塞 HTML Parser，但会影响关键渲染，并可能通过脚本形成间接等待；
- Reflow / Repaint、Forced Synchronous Layout、Layout Thrashing 的现象已经理解，但术语和具体 DOM API 仍不熟。

详见：

- [[03-Knowledge/Web/01-url-dns-tcp-tls-http]]
- [[03-Knowledge/Web/02-cors-auth-security]]
- [[03-Knowledge/Web/03-cache-cdn-http-versions]]
- [[03-Knowledge/Web/04-browser-rendering]]

## 正在学习

### JavaScript + DOM 最低必要基础

因为尚未系统学习 JavaScript，当前先暂停继续深入 `requestAnimationFrame` / Event Loop，补齐之后浏览器学习所需的语言与 DOM 基础。

当前精确断点：

```js
const title = document.querySelector(".title");
```

已经能够大体解释：

- `const`：声明一个不能被重新赋值 / 重新绑定的变量；对于对象，不能把变量重新指向另一个对象，但对象内部内容仍可能修改；
- `title`：自己起的变量名，用来保存右侧表达式的结果；
- `document`：浏览器提供的、代表当前文档的 DOM `Document` 对象，是 Web API，不是 JavaScript 语言关键字；
- `querySelector(...)`：`document` 对象上的一个方法，用 CSS selector 查找匹配的 DOM 元素；
- `".title"`：JavaScript 字符串，其内容会被 `querySelector` 按 CSS Selector 语法解释；这里 `.` 表示 class selector，即寻找 `class="title"` 的元素。

下一窗口需要先纠正/巩固的两个点：

1. `document` 不是“HTML 里某一个 DOM 元素”，而是代表整个当前文档的 `Document` 对象，是 DOM 树的重要入口。
2. `".title"` 本身只是字符串；不是字符串自己成为“解析器”。是 `querySelector` 接收这个字符串，并按 CSS Selector 语法解析它。

用户有 C++ 语言基础，可多用 C++ 的变量、成员访问、成员函数做类比，但要明确 JavaScript 的动态类型、对象模型和引用语义并不等同于 C++。

## 接下来的路线

总体不是“先学完整前端，再学后端”，而是沿一次完整 Web 请求螺旋推进：

```text
Web / Network 基础
→ Browser Rendering
→ JavaScript 最低必要基础
→ DOM / Event
→ Promise / async-await / Event Loop
→ fetch / JSON / API
→ 后端第一次正式进入：Server / Port / Route / Request / Response
→ 数据库与 SQL
→ 完整前后端交互：登录 / Cookie / Session / JWT / CORS / 权限
→ 前端框架核心概念（Vue / React）
→ 后端工程化
→ 算法 / 工程 / 安全 / 性能持续穿插
```

后端的自然切入点是 `fetch()`：浏览器既然发出 `/api/...` 请求，就开始追问是谁监听端口、路由如何匹配、后端如何返回 JSON、数据库何时参与、404/500 在哪里产生。

## 学习方式提醒

- JavaScript / DOM API（如 `offsetWidth`、`querySelector`）第一次遇到只要求知道用途，不强求立即背名字；
- 浏览器核心概念（Layout / Paint / Composite）要求真正理解；
- 专有术语（Layout Thrashing、Forced Synchronous Layout）先理解现象，再贴术语标签；
- 每个重要概念后继续做口头回忆题，把“能理解”逐渐升级为“能准确表达”。
