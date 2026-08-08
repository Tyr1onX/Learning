---
tags:
  - roadmap
  - learning
status: active
updated: 2026-08-08
---

# 学习路线

## 总目标

建立一套能够支撑前端 / 全栈 / AI 工具开发面试与实际项目判断的计算机基础。重点不是“手写所有代码”，而是能够：

- 准确描述需求与技术链路；
- 看懂并判断 AI 生成代码是否正确、安全、可维护；
- 理解常见框架和协议背后的原理；
- 对性能、复杂度、安全、工程化做基本判断；
- 面对追问时能从原理继续推，而不是只会背答案。

## Phase A — Web 与网络基础（当前）

### A1. 一次网页访问的主干

URL 结构 → DNS → IP / Port → TCP → TLS → HTTP Request / Response → 浏览器解析与渲染。

### A2. HTTP

Method、Status Code、Header、Content-Type、幂等、HTTP/1.1 / 2 / 3、Keep-Alive、Multiplexing、Head-of-Line Blocking、QUIC。

### A3. 浏览器安全与状态

Cookie、Session、JWT、Access Token / Refresh Token、Authentication / Authorization、XSS、CSRF、SameSite、Same-Origin Policy、CORS、Preflight。

### A4. 性能基础

强缓存、协商缓存、Cache-Control、ETag、304、Content Hash、CDN、TTL、Cache Hit / Miss、回源。

### A5. 浏览器渲染

DOM、CSSOM、Render Tree、Style Calculation、Layout、Paint、Composite、Reflow / Repaint、`transform` / `opacity`。

完成标准：能够从“输入 URL”连续解释到“页面显示”，并能回答常见追问。

---

## Phase B — HTML / CSS / JavaScript 基础

HTML：语义化、表单、资源加载、脚本加载、可访问性基础。

CSS：盒模型、选择器、层叠与优先级、Flex、Grid、定位、响应式、动画与渲染性能。

JavaScript：类型、作用域、闭包、原型链、`this`、DOM 事件、Promise、`async/await`、Event Loop、Fetch、模块化、错误处理。

重点：不仅知道“怎么写”，还要解释“为什么这样运行”。

---

## Phase C — 前端框架与工程化

先理解框架解决什么问题，再进入具体框架：组件化、状态、响应式、Virtual DOM / Diff、生命周期、路由、数据请求、构建工具。

需要建立 Vue / React 至少一种框架的基础使用能力，同时理解框架原理的关键抽象，不要求一开始深挖源码。

工程化：Vite / Bundler、模块依赖、环境变量、Lint、Format、测试、构建产物、静态部署、Source Map。

---

## Phase D — 后端与全栈基础

HTTP API、REST 语义、Controller / Service / Repository、参数校验、统一错误、日志、鉴权、数据库、事务、并发、异步任务、SSE / WebSocket、服务部署。

数据库主线：表 / 主键 / 索引 / SQL / JOIN / 事务 / 隔离级别 / 参数化查询。

系统主线：进程 / 线程 / 内存 / 文件 / 端口 / Linux / Docker。

---

## Phase E — 数据结构与算法

先掌握复杂度，再逐步建立题型模板：数组、字符串、Hash、链表、栈、队列、树、图、DFS、BFS、二分、排序、双指针、滑窗、动态规划。

真实面试专项：

```text
old lines + new lines
→ keep / delete / add
→ LCS / Diff 思想
→ 再理解 Myers Diff
```

目标不是刷题数量，而是能分析复杂度、解释状态定义与转移、写出基础实现。

---

## Phase F — 软件工程 / 安全 / 性能

工程：模块边界、依赖方向、测试分层、日志、错误处理、兼容性、迁移、可维护性、多人协作、Git / PR / CI。

安全：输入不可信原则、XSS、CSRF、SQL 注入、Token 泄露、Secrets、HTTPS、CORS 边界、权限校验。

性能：算法复杂度、网络请求、缓存、数据库查询、渲染性能、测量与 Profile。

---

## Phase G — AI 辅助开发能力

把 AI 当作开发工具而不是知识替代品。形成固定检查框架：

```text
需求是否说清楚？
↓
方案为什么合理？
↓
代码能否运行？
↓
边界情况是什么？
↓
安全性如何？
↓
性能复杂度如何？
↓
测试覆盖了吗？
↓
半年后还能维护吗？
```

最终目标：能够解释 AI 生成实现、发现错误、提出约束、进行验收，并对设计取舍负责。

## 学习方法

每个主题使用同一节奏：**白话直觉 → 准确概念 → 小例子 → 与项目连接 → 面试表达 → 回忆题 → 错误纠正 → 间隔复习**。

不把“刚听懂”直接标记为 `interview-ready`。只有隔一段时间仍能独立回答、并能处理追问，才升级状态。
