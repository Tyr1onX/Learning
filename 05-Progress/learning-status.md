---
tags:
  - progress
  - learning
status: active
updated: 2026-09-09
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
| JavaScript | const / let / value / binding | learning | 已完成第一轮，变量 / 基础类型 D+7 已补复习通过 | D+21：2026-09-17 |
| JavaScript | Object / Array / reference | learning | 已完成第一轮，对象 / 数组 D+7 于 2026-09-09 补复习通过 | D+21：2026-09-18 |
| JavaScript | Function / return / local variables | learning | 已完成第一轮，D+7 逾期待补 | 尽快补复习 |
| JavaScript | Scope / Closure | learning | 已完成第一轮，D+7 待补 | 尽快补复习 |
| JavaScript | this | learning | 已完成第一轮，D+7 待补 | 尽快补复习 |
| JavaScript | Prototype | learning | 已完成第一轮，D+7 待补 | 尽快补复习 |
| JavaScript / DOM | document / querySelector / Element / Event | learning | DOM / Event 已完成第一轮；需巩固 API 大小写、选择器字符串和 `event.target` | D+7 待补 |
| JavaScript | Promise / Event Loop / async-await | learning | 已完成第一轮；需巩固 `await` 前同步执行、`await` 后微任务 | D+1/D+3 待补，D+7：2026-09-13 |
| Web / JavaScript | fetch / JSON / API | learning | 2026-09-09 完成第一轮；`res` vs `data`、`res.ok`、JSON 结构、路由匹配需复习 | D+1：2026-09-10 |
| CSS | Box / Flex / Grid / Position | not-started | 有项目使用经验但未系统审计 | Phase B |
| Framework | Vue / React concepts | not-started | 框架概念基础薄弱 | TypeScript 后进入 |
| Backend | Server / Route / Request / Response | not-started | 已由 `fetch()` 建立入口，尚未正式系统学后端 | API 后正式进入 |
| Backend | REST / service layering / validation | not-started | 有零散概念 | 后端基础之后 |
| Database | SQL / index / transaction | not-started | 有基础使用经验但需系统补 | 后端 API 后 |
| OS/Linux | process / thread / memory / IO | not-started | 有零散接触 | Phase D/F |
| Algorithm | Complexity | review-needed | 能说常见复杂度，但理由表达需更精确，如 239 要说“每个下标最多入队/出队一次” | 持续穿插 |
| Algorithm | Hash / Prefix Sum | learning | 560 已完成第一轮；D+3 补问后恢复，但循环顺序初次记反 | 晚间 / D+7 复查 |
| Algorithm | Sliding Window / Monotonic Queue | learning | 239 已完成第一轮；deque 存下标、窗口边界、过期判断和入队下标需巩固 | D+1：2026-09-10 |
| Algorithm | DFS / BFS | review-needed | 见过常见写法，需真正理解 | Phase E |
| Algorithm | DP / LCS / Diff | not-started | 真实面试暴露为明显短板 | 重点专项 |
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

2026-09-09：完成 `fetch / JSON / API` 第一轮与 LeetCode 239「滑动窗口最大值」。

- `fetch / JSON / API`：能理解浏览器 JS 通过 `fetch` 向后端 API 请求数据，后端匹配路由并返回 JSON；当前需继续巩固 `Response` / `res.json()`、`res.ok`、JSON 对象 / 数组结构和路由匹配术语。
- 239：能理解单调队列保留未来可能成为最大值的候选；当前需继续巩固 `deque` 存下标、窗口边界 `[i-k+1, i]`、过期条件、队尾比较、入队下标和 `O(n)` 复杂度理由。
- 旧复习：对象 / 数组、438、15 通过；42 补问后通过；560 补问后恢复，但循环顺序需要晚间再抽。