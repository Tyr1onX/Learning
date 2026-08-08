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

学习者不是从零开始写代码，但计算机基础存在“项目做过很多、底层概念不够系统”的特点。AI 辅助开发与项目实践能力明显强于传统基础知识的口头解释与算法能力。

目前最有效的教学目标不是快速堆知识点，而是把已经见过、用过的概念形成稳定模型，让学习者能：

- 用自己的话解释；
- 被追问时继续往下推；
- 发现自己措辞里的技术错误；
- 判断 AI 给出的方案是否合理。

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

## 已确认能解释的内容

### Web / Network

能够解释 URL 基本组成、域名到 IP、端口定位服务、DNS 层级解析、TCP 三次握手的目的、TCP 可靠传输的 ACK / 重传等机制、TLS 的安全目标、HTTP 常见方法与状态码。

### Auth / Browser Security

能够区分 401 / 403、Authentication / Authorization；理解 Cookie / Session；理解签名 JWT 的 Payload 通常可读、签名用于防篡改、Token 被整体偷走仍然危险；能够区分 XSS / CSRF、SameSite / Same-Origin、CORS。

### Cache / CDN / HTTP Versions

理解强缓存与协商缓存、ETag / 304、Content Hash；理解 CDN 边缘缓存、Hit / Miss / 回源 / TTL；能够说明 HTTP/2 多路复用与 TCP 队头阻塞，以及 HTTP/3 → QUIC → UDP 的基本关系。

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
```

## 当前明显薄弱项

- Browser Rendering 还没有完成系统学习；
- JavaScript 执行模型、Event Loop、闭包、原型链等尚未系统补齐；
- Vue / React 等框架原理基础薄弱；
- 后端 / 数据库 / 全栈体系需要系统建立；
- 算法现场实现较弱，尤其是 Diff / LCS / 动态规划；
- 工程化、安全、性能有项目经验，但需要从经验提升到可解释的理论框架；
- 面试时容易使用“可能、就是、相应的”等模糊表达，需要训练技术表述的结构化与精确性。

## 教学规则

1. 不因为“刚刚答对一次”就判断完全掌握。
2. 每隔几个主题，安排旧知识混合回忆。
3. 回答中出现局部错误时，保留正确推理，只修错误点，避免整段推倒重讲。
4. 优先让学习者自己推答案，再给标准表达。
5. 新知识尽量挂接到真实项目、浏览器请求链路或真实面试问题。
6. 每完成一个明显主题，更新本仓库状态，而不是把进度只留在聊天记录里。
7. `interview-ready` 的标准：隔一段时间仍能脱离提示完整解释，并能接至少两层追问。

## 新窗口推荐开场

AI 应先检查：

```text
00-Home.md
02-Current/current-focus.md
02-Current/learning-context.md
05-Progress/learning-status.md
```

然后从 `current-focus.md` 的“正在学习”继续，不要默认从第一章重讲。
