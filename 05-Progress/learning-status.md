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
| Browser | DOM / CSSOM / Render pipeline | learning | 已准备主干，尚未完成回忆测试 | **当前继续** |
| Browser | script / defer / async | not-started | 尚未系统学 | Rendering 后 |
| JavaScript | Scope / Closure / Prototype / this | not-started | 尚未系统补 | Phase B |
| JavaScript | Promise / Event Loop / async-await | not-started | 尚未系统补 | Phase B |
| CSS | Box / Flex / Grid / Position | not-started | 有项目使用经验但未系统审计 | Phase B |
| Framework | Vue / React concepts | not-started | 框架概念基础薄弱 | Phase C |
| Backend | REST / service layering / validation | not-started | 有零散概念 | Phase D |
| Database | SQL / index / transaction | not-started | 有基础使用经验但需系统补 | Phase D |
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

2026-08-08：完成 URL / DNS / TCP / TLS / HTTP、CORS / Auth / Security、Cache / CDN、HTTP/1.1 / 2 / 3 的一轮学习与口头回忆。下一主题为 Browser Rendering Pipeline。
