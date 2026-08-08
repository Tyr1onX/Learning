---
tags:
  - current
  - ai-context
  - teaching
status: active
updated: 2026-08-08
---

# Learning Context for AI

> 新聊天窗口继续教学时，先读本文件，再读 [[02-Current/current-focus]] 与 [[05-Progress/learning-status]]。

## 当前能力画像

学习者不是从零开始写代码，有一定 C++ 语言基础，因此变量、函数、成员访问、控制流等概念可用 C++ 做直觉类比；但 JavaScript、DOM / Web API 尚未系统学习。项目实践与 AI 辅助开发经验明显强于传统基础知识的系统化口头解释与算法能力。

目前最有效的教学目标不是快速堆知识点，而是把已经见过、用过的概念形成稳定模型，让学习者能：

- 用自己的话解释；
- 被追问时继续往下推；
- 发现自己措辞里的技术错误；
- 判断 AI 给出的方案是否合理；
- 把“理解现象”逐渐升级成“记得准确术语并能面试表达”。

## 已确认的学习方式

当前教学方式效果较好：

```text
先给一个直觉模型
↓
补正式术语
↓
用极小例子解释
↓
问 1～5 个回忆 / 推理题
↓
学习者用自己的话回答
↓
只纠正真正不准确的部分
↓
把正确表达压缩成面试可用版本
```

不要一次性灌大量教材内容。优先“小块推进 + 高频回忆”。

对于 JavaScript / DOM API 与浏览器性能术语，当前采用三层记忆策略：

```text
第一层：先理解现象 / 代码意图
第二层：知道准确术语是什么
第三层：经过间隔复习后，能脱离提示主动说出术语
```

例如 `offsetWidth`、`querySelector` 第一次出现只要求知道用途；Layout Thrashing、Forced Synchronous Layout 先理解现象，再逐渐记住名称，不因为暂时叫不出术语就判定“不理解”。

## 已确认能解释的内容

### Web / Network

能够解释 URL 基本组成、域名到 IP、端口定位服务、DNS 层级解析、TCP 三次握手的目的、TCP 可靠传输的 ACK / 重传等机制、TLS 的安全目标、HTTP 常见方法与状态码。

### Auth / Browser Security

能够区分 401 / 403、Authentication / Authorization；理解 Cookie / Session；理解签名 JWT 的 Payload 通常可读、签名用于防篡改、Token 被整体偷走仍然危险；能够区分 XSS / CSRF、SameSite / Same-Origin、CORS。

### Cache / CDN / HTTP Versions

理解强缓存与协商缓存、ETag / 304、Content Hash；理解 CDN 边缘缓存、Hit / Miss / 回源 / TTL；能够说明 HTTP/2 多路复用与 TCP 队头阻塞，以及 HTTP/3 → QUIC → UDP 的基本关系。

### Browser Rendering 第一轮

已经完成第一轮 Browser Rendering 主干学习并能通过口头推理回答主要问题：

```text
HTML → DOM
CSS → CSSOM
→ Layout
→ Paint
→ Composite
```

已理解：

- HTML 与 DOM 的区别；
- `display:none` / `visibility:hidden` / `opacity:0`；
- `transform` / `opacity` 与动画性能；
- `transition` 的连续过渡直觉；
- 普通 `<script>` 为什么阻塞 HTML Parser；
- `async` / `defer` 的下载与执行顺序；
- `DOMContentLoaded` / `load`；
- CSS 通常不直接阻塞 DOM 构建，但会影响关键渲染，并可能通过普通 JS 形成间接等待；
- Reflow / Repaint；
- 修改布局后立即读取尺寸为什么可能产生 Forced Synchronous Layout；
- 频繁读写布局为什么可能形成 Layout Thrashing。

注意：最后几个专有术语和具体 DOM API 名称仍不稳定，需要后续间隔复习。

## 最近纠正过的错误

这些点容易复发，教学时应主动检查：

```text
错误：JWT 是加密。
纠正：常见 JWT 是签名 Token，Payload 通常可读。

错误：TCP 可靠性主要靠三次握手 / 心跳。
纠正：三次握手负责建连；可靠传输靠序列号、ACK、重传、流控等。

错误：TLS 提升 TCP 的可靠性。
纠正：TLS 解决保密性、完整性、身份认证；TCP 负责可靠有序传输。

错误：CORS 阻止跨域请求。
纠正：更准确地说，它控制浏览器是否把跨源响应暴露给 JS；有些请求仍会真正到达服务器。

错误：CORS 可以防 CSRF。
纠正：CSRF 不一定需要读取响应，CORS 不是主要 CSRF 防线。

错误：no-cache = 不缓存。
纠正：no-cache 可以存，但复用前需要重新验证；no-store 才是不存。

错误：HTTP/2 有 Multiplexing 就彻底没有队头阻塞。
纠正：仍存在 TCP 连接级 Head-of-Line Blocking。

错误：display:none = 元素不占内存 / DOM 中不存在。
纠正：DOM 节点仍可存在；它是不参与正常 Layout、不占页面布局空间。

错误：普通 script 阻塞 HTML Parsing 是因为 JS 会“重新绘制页面”。
纠正：更核心的原因是 JS 可以修改 DOM / 文档解析结果，因此 Parser 不能无条件越过脚本继续。

易混：document 是 HTML 中某一个 DOM 元素。
纠正：`document` 是浏览器提供的 `Document` 对象，代表当前整个文档，是访问 DOM 树的重要入口。

易混：`.title` 字符串本身是 CSS 解析器。
纠正：`.title` 只是 JavaScript 字符串；是 `querySelector()` 按 CSS Selector 语法解释这个字符串。
```

## 当前明显薄弱项

- JavaScript 语言基础尚未系统补齐，目前从 `const title = document.querySelector(".title")` 开始补变量、值、对象、函数、DOM / Web API；
- Browser Rendering 主干已完成第一轮，但 Reflow / Repaint、Forced Synchronous Layout、Layout Thrashing 等术语仍需间隔复习；
- JavaScript 执行模型、Event Loop、闭包、原型链等尚未系统补齐；
- Vue / React 等框架原理基础薄弱；
- 后端 / 数据库 / 全栈体系需要系统建立；
- 算法现场实现较弱，尤其是 Diff / LCS / 动态规划；
- 工程化、安全、性能有项目经验，但需要从经验提升到可解释的理论框架；
- 面试时容易使用“可能、就是、相应的”等模糊表达，需要训练技术表述的结构化与精确性。

## 总体学习路线

不是“完整学完前端以后才进入后端”，而是沿完整 Web 请求链路螺旋推进：

```text
Web / Network 基础
→ Browser Rendering
→ JavaScript 最低必要基础
→ DOM / Event
→ Promise / async-await / Event Loop
→ fetch / JSON / API
→ Backend：Server / Port / Route / Request / Response
→ Database / SQL
→ 完整前后端交互：登录 / Cookie / Session / JWT / CORS / 权限
→ Frontend Framework：Vue / React 核心概念
→ Backend Engineering
→ Algorithm / Engineering / Security / Performance 持续穿插
```

后端的第一次正式切入点是 `fetch()`：浏览器发出 `/api/...` 请求后，自然追问谁监听端口、Route 如何匹配、后端如何返回 JSON、数据库何时参与、404 / 500 在哪里产生。

## 教学规则

1. 不因为“刚刚答对一次”就判断完全掌握。
2. 每隔几个主题，安排旧知识混合回忆。
3. 回答中出现局部错误时，保留正确推理，只修错误点，避免整段推倒重讲。
4. 优先让学习者自己推答案，再给标准表达。
5. 新知识尽量挂接到真实项目、浏览器请求链路或真实面试问题。
6. 每完成一个明显主题，更新本仓库状态，而不是把进度只留在聊天记录里。
7. `interview-ready` 的标准：隔一段时间仍能脱离提示完整解释，并能接至少两层追问。
8. JavaScript / DOM 学习可利用 C++ 做类比，但必须明确 JavaScript 的动态类型、对象模型、引用 / 绑定语义与 C++ 并不等同。

## 学习记录持久化规则

不能把“用户主动提出换窗口”当成唯一同步时机，因为聊天上下文存在容量上限；如果真的在下一次可交互之前触顶，就没有机会再执行 GitHub 写入。因此采用“增量检查点 + 换窗收尾”双保险。

### A. 增量检查点同步（默认自动进行）

在仍可正常交流时，只要出现明显学习增量，就应在合适的回复回合顺手持久化，不必等用户提出换窗口。典型检查点包括：

```text
- 一个明显主题完成一轮讲解 + 回忆验证；
- 连续形成了一组新的、值得长期保存的知识点；
- 一个重要误区被发现并纠正；
- 学习路线 / 教学策略发生调整；
- 当前断点发生明显跨主题变化；
- 会话已经较长，距离上次同步已有较多新增内容。
```

每次检查点不要求重写所有文件，只更新真正有增量的文件，优先保证：

```text
对应 03-Knowledge/... 知识笔记
+ 05-Progress/Sessions/... 滚动会话记录
```

必要时同时更新：

```text
02-Current/current-focus.md
05-Progress/learning-status.md
02-Current/learning-context.md
```

目标是让“最坏情况下丢失的内容”只剩最近很短的一小段，而不是整个窗口。

### B. 窗口切换收尾同步

只要学习者明确表示“要换新窗口 / 开新窗口 / 这个窗口太卡了准备切窗口”等意思，在给出交接词之前，AI 必须先自动把自上次检查点以来的剩余学习增量写入 `Tyr1onX/Learning`，不需要学习者额外提醒。

至少检查并按实际需要更新：

```text
1. 02-Current/current-focus.md
   → 当前精确断点、下一步、尚未解决的问题

2. 对应的 03-Knowledge/... 主题笔记
   → 本窗口真正学过的新知识、例子、纠正过的误区

3. 05-Progress/learning-status.md
   → 各主题状态是否从 not-started / learning / understood 等发生变化

4. 05-Progress/Sessions/... 会话记录
   → 本次学习覆盖内容、关键回答、仍不稳定的术语、下一窗口入口

5. 02-Current/learning-context.md（仅在学习策略 / 能力画像 / 固定规则变化时）
   → 例如发现新的学习习惯、术语记忆问题、路线调整
```

### C. 同步原则

- 记录“学了什么”，不只记录“学到哪里”；
- 记录用户已经能自己推理出的内容，也记录刚纠正的误区；
- 不把只听过一次的概念直接升级为 `understood`；
- 如果现象理解了但术语不稳定，要明确写成“现象理解 / 术语待复习”；
- 不依赖“准确知道还剩多少上下文”来决定何时保存；应通过自然学习检查点主动降低风险；
- 换窗时 GitHub 收尾同步完成后再给新窗口简短交接词。

## 新窗口推荐开场

AI 应先检查：

```text
00-Home.md
02-Current/current-focus.md
02-Current/learning-context.md
05-Progress/learning-status.md
最近一条 05-Progress/Sessions/... 会话记录
```

然后从 `current-focus.md` 的“正在学习”继续，不要默认从第一章重讲。