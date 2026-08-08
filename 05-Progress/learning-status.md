---
tags:
  - progress
  - learning
status: active
updated: 2026-08-08
---

# Learning Status

> 状态不是成绩，而是“现在能不能在没有提示的情况下解释清楚”。

| 领域 | 主题 | 状态 | 当前判断 | 下一次检查 |
|---|---|---|---|---|
| Web | URL / Domain / IP / Port | understood | 主干能独立解释 | 混合回忆 |
| Web | DNS hierarchy / TTL / records | understood | Root/TLD/Auth、TTL 能解释 | 追问 CNAME / CDN |
| Network | TCP handshake | understood | 能解释为什么三次 | 与关闭连接一起复习 |
| Network | TCP reliable transport | understood | 已纠正“握手/心跳=可靠性” | 再问 ACK/重传/序列号 |
| Security | TLS / certificate / CA | understood | 能区分 TCP 与 TLS 职责 | 后续补 TLS handshake 细节 |
| HTTP | Method / idempotency | understood | POST/PUT/DELETE 能解释 | REST API 中再强化 |
| HTTP | Status Code / 401 / 403 | understood | Authentication / Authorization 已纠正 | 混合回忆 |
| Auth | Cookie / Session | understood | 客户端 ID / 服务端状态模型清楚 | 后端实现时复习 |
| Auth | JWT / Access / Refresh Token | understood | 已纠正 JWT≠加密 | 间隔复习 Token 被盗场景 |
| Security | XSS / CSRF | understood | 能解释攻击目标差异 | 后续补 CSP / CSRF token |
| Web | Same-Origin / SameSite | understood | 能区分 Origin 与 Site | 与 Cookie/CORS 混合问 |
| Web | CORS / Preflight | understood | 能解释 200 仍 CORS error、JSON preflight | 需间隔复习 safelist |
| Performance | Strong / Conditional Cache | understood | max-age、ETag、304 主干清楚 | 补 Vary 等更深内容前先复习 |
| Performance | no-cache / no-store | understood | 已纠正反直觉含义 | 高频抽问 |
| Performance | Content Hash | understood | 能解释为什么新 URL 绕过旧缓存 | 与构建工具连接 |
| Performance | CDN / TTL / Hit / Miss / Origin | understood | 主干能自己推导 | 后续补 CDN 与部署实践 |
| HTTP | HTTP/1.1 Keep-Alive | understood | 能解释连接复用目的 | 与连接池/浏览器并发联系 |
| HTTP | HTTP/2 Multiplexing / HOL | understood | 已理解 TCP 层队头阻塞 | 间隔复述 |
| HTTP | HTTP/3 / QUIC / UDP | understood | 能解释 QUIC 提供可靠性与 TLS 1.3 | 后续补 RTT / 0-RTT |
| HTTP | QUIC Connection Migration | understood | 能用四元组 vs Connection ID 解释 | 后续复习 |
| Browser | DOM / CSSOM / Render pipeline | understood | 已能解释 HTML≠DOM、Layout→Paint→Composite 主干 | 隔一段时间无提示复述 |
| Browser | display / visibility / opacity | understood | 能区分是否占布局空间、是否默认可点击 | 与动画 / accessibility 再联系 |
| CSS | transform / opacity / transition | understood | 已理解变换、不透明度、连续过渡及为何常用于动画 | 后续结合实际动画代码 |
| Browser | script / defer / async | understood | 能根据下载完成顺序判断 async；能说明 defer 保持声明顺序 | 间隔混合题 |
| Browser | DOMContentLoaded / load | understood | 能判断 DOM 完成但大图片未完成时两事件差异 | 与 defer / module 再联系 |
| Browser | CSS render blocking / JS indirect wait | understood | 能解释 DOM 可继续构建、关键渲染需等样式，以及 HTML→JS→CSS 等待链 | 后续结合 Critical Rendering Path |
| Performance | Reflow / Repaint | learning | 现象基本理解，正式术语仍需稳定 | JS / DOM 后再抽问 |
| Performance | Forced Synchronous Layout | learning | 能解释“写布局后立刻读真实几何值必须先算 Layout” | 结合实际 DOM API 复习 |
| Performance | Layout Thrashing | learning | 已理解频繁读写导致反复 Layout，但术语不易主动想起 | 间隔复习术语 + 代码模式 |
| JavaScript | const / let / value / binding | learning | 已开始从 `const title = ...` 建立 JS 语言基础 | **当前继续** |
| JavaScript / DOM | document / querySelector / Element | learning | 已理解大意；需巩固 Document≠具体 Element、selector 字符串由方法解释 | **当前继续** |
| JavaScript | Scope / Closure / Prototype / this | not-started | 尚未系统补 | JS 基础后 |
| JavaScript | Promise / Event Loop / async-await | not-started | 尚未系统补 | DOM / Event 后 |
| CSS | Box / Flex / Grid / Position | not-started | 有项目使用经验但未系统审计 | Phase B |
| Framework | Vue / React concepts | not-started | 框架概念基础薄弱 | fetch/API/完整交互后逐步进入 |
| Backend | Server / Route / Request / Response | not-started | 计划由 `fetch()` 自然切入 | JS 异步 / API 后 |
| Backend | REST / service layering / validation | not-started | 有零散概念 | 后端基础之后 |
| Database | SQL / index / transaction | not-started | 有基础使用经验但需系统补 | 后端 API 后 |
| OS/Linux | process / thread / memory / IO | not-started | 有零散接触 | Phase D/F |
| Algorithm | Complexity | review-needed | 知道概念但需系统化 | Phase E 前置 |
| Algorithm | DFS / BFS | review-needed | 见过常见写法，需真正理解 | Phase E |
| Algorithm | DP / LCS / Diff | not-started | 真实面试暴露为明显短板 | **重点专项** |
| Engineering | Git / PR / CI / testing | review-needed | 项目经验较多，理论表达需整理 | Phase F |
| Engineering | Maintainability / architecture | review-needed | 有实际迭代经验，需形成判断框架 | Phase F |
| AI Coding | Requirement / review / validation | understood | 当前相对优势 | 与每个基础模块融合 |

## 状态升级规则

```text
not-started
↓ 系统学习
learning
↓ 能独立解释主干
understood
↓ 隔一段时间仍能答 + 处理追问
interview-ready
```

如果复习时明显遗忘，可以从 `understood` 回退为 `review-needed`，这不是失败，而是让记录反映真实状态。

## 最近一次更新

2026-08-08：Browser Rendering 完成第一轮学习并通过连续口头推理：HTML / DOM / CSSOM、`display:none` / `visibility:hidden` / `opacity:0`、`transform` / `opacity` / `transition`、普通 script、`async` / `defer`、`DOMContentLoaded` / `load`、CSS 对 Parsing / Rendering 的不同影响、Reflow / Repaint、Forced Synchronous Layout、Layout Thrashing。浏览器主干升级为 `understood`，但性能专有术语仍保留为 `learning`。

当前已转入 JavaScript + DOM 最低必要基础，从：

```js
const title = document.querySelector(".title");
```

继续学习 `const` / `let`、值与类型、对象、函数、`document`、DOM Element、方法与 CSS Selector；之后再进入 DOM Event、Promise / async-await / Event Loop，并由 `fetch()` 正式引入后端。