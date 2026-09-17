---
tags:
  - progress
  - learning
status: active
updated: 2026-09-17
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
| Web | CORS / Preflight | understood | 能解释 200 仍 CORS error、JSON preflight | 间隔复习 |
| Performance | Strong / Conditional Cache | understood | max-age、ETag、304 主干清楚 | 补 Vary 前先复习 |
| Performance | no-cache / no-store | understood | 已纠正反直觉含义 | 高频抽问 |
| Performance | Content Hash | understood | 能解释新 URL 绕过旧缓存 | 与构建工具连接 |
| Performance | CDN / TTL / Hit / Miss / Origin | understood | 主干能自己推导 | 部署实践时再连 |
| HTTP | HTTP/1.1 Keep-Alive | understood | 能解释连接复用目的 | 与连接池联系 |
| HTTP | HTTP/2 Multiplexing / HOL | understood | 已理解 TCP 层队头阻塞 | 间隔复述 |
| HTTP | HTTP/3 / QUIC / UDP | understood | 能解释 QUIC 提供可靠性与 TLS 1.3 | 后续补 RTT / 0-RTT |
| HTTP | QUIC Connection Migration | understood | 能用四元组 vs Connection ID 解释 | 后续复习 |
| Browser | DOM / CSSOM / Render pipeline | understood | 主干能独立解释 | 混合回忆 |
| Browser | display / visibility / opacity | understood | 能区分布局与可见性 | 后续混合问 |
| CSS | transform / opacity / transition | understood | 理解常用于动画的原因 | 结合实际代码 |
| Browser | script / defer / async | understood | 能判断下载 / 执行顺序 | 间隔混合题 |
| Browser | DOMContentLoaded / load | understood | 能区分两事件 | 与 defer/module 联系 |
| Browser | CSS render blocking / JS indirect wait | understood | 能解释 Parsing / Rendering 区别 | 后续关键渲染路径 |
| Performance | Reflow / Repaint | learning | 现象理解，术语仍需稳定 | 间隔复习 |
| Performance | Forced Synchronous Layout | learning | 能解释写后立刻读几何值 | DOM API 中复习 |
| Performance | Layout Thrashing | learning | 现象理解，术语不稳定 | 间隔复习 |
| JavaScript | const / let / value / binding | learning | 第一轮完成；D+7 已通过 | D+21 2026-09-17 待补 |
| JavaScript | Object / Array / reference | learning | D+7 已通过 | D+21 2026-09-18 |
| JavaScript | Function / return / local variables | learning | 2026-09-17 逾期补复习；`NaN` / 缺失参数经补充后理解 | D+21 2026-09-19 |
| JavaScript | Scope / Closure | learning | 第一轮完成，D+7 逾期 | 尽快补复习 |
| JavaScript | this | learning | 第一轮完成，D+7 逾期 | 尽快补复习 |
| JavaScript | Prototype | learning | 第一轮完成，D+7 逾期 | 尽快补复习 |
| JavaScript / DOM | document / querySelector / Element / Event | learning | 第一轮完成，固定语法仍需稳定 | D+7 逾期 |
| JavaScript | Promise / Event Loop / async-await | learning | 第一轮完成；`await` 前后顺序需稳定 | D+21 2026-09-27 |
| Web / JavaScript | fetch / JSON / API | learning | 第一轮完成；Response / JSON / 路由术语需复习 | D+21 2026-09-30 |
| TypeScript | 基础类型 / 对象 / 联合类型 / narrowing / 数组 | learning | 2026-09-17 第一轮完成；可选字段与 `User[]` 初次有混淆 | D+1 2026-09-18 |
| Python | 基础语法 / 控制流 / 列表 / 函数 / 字典 | learning | 2026-09-09 第一轮，之后未记录复习完成 | 待恢复 |
| Python | 集合 set | learning | 已看示例，尚未记录独立去重题完成 | 待恢复 |
| Python | 类型注解 / 模块 / 异常处理 | not-started | 仅入门介绍 | 基础复习后 |
| CSS | Box / Flex / Grid / Position | not-started | 有项目经验但未系统审计 | Phase B |
| Framework | React concepts | not-started | TypeScript 第一轮已完成，下一主线 | **当前下一主题** |
| Backend | Server / Route / Request / Response | not-started | 已由 fetch/API 建立入口 | React 后 / API 链路继续 |
| Backend | REST / service layering / validation | not-started | 有零散概念 | 后端基础之后 |
| Database | SQL / index / transaction | not-started | 有基础使用经验但需系统补 | 后端 API 后 |
| OS/Linux | process / thread / memory / IO | not-started | 有零散接触 | Phase D/F |
| Algorithm | Complexity | review-needed | 能判断常见复杂度，理由表达仍需精确 | 持续穿插 |
| Algorithm | Hash / Prefix Sum | learning | 560 于 2026-09-17 逾期复习恢复；`count[0]` 语义仍需稳定 | D+21 2026-09-27 |
| Algorithm | Sliding Window / Monotonic Queue | learning | 239 于 2026-09-17 恢复；队头/队尾职责经手推后理顺 | D+21 2026-09-30 |
| Algorithm | Sliding Window / Minimum Window | learning | 76 第一轮完成；已能写出核心 need/window/valid 更新 | D+1 2026-09-18 |
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

复习时明显遗忘可回退状态；状态只反映当前真实能力。

## 最近一次更新

2026-09-17：完成 TypeScript 基础第一轮与 LeetCode 76「最小覆盖子串」。

- TypeScript：理解静态类型检查、类型推断、对象类型、可选字段、`type`、联合类型、narrowing、`T[]`；可选字段和数组元素类型初次有混淆，状态保持 `learning`。
- 76：从朴素枚举进入滑动窗口，理解 `need / window / valid`、右扩左缩、临界 `valid++/--`、左闭右开窗口，并在引导后独立写出核心循环；状态保持 `learning`。
- 49 D+21 通过；560 逾期复习恢复；239 D+7 逾期一天补复习恢复。
- 函数定义 / 调用逾期补复习；`NaN` 和缺失参数行为需继续间隔抽查。
