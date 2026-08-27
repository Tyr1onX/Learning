---
tags:
  - current
  - learning
status: active
updated: 2026-08-27
---

# 当前学习焦点

## 当前总目标

面向下一次字节跳动日常实习 / 暑期实习，按“每天一个明确学习主题 + 一道 Hot 100 算法任务”的固定节奏推进全栈能力。当天任务完成后停止继续备战，避免无休止加量。

## 已完成主干

Web / Network / Browser 已完成一轮系统学习并经过无提示混合回忆，主干维持 `understood`：

- URL、Domain、IP、Port；
- DNS hierarchy / TTL / records；
- TCP handshake 与可靠传输；
- TLS / certificate / CA；
- HTTP methods / status / idempotency；
- Cookie / Session / JWT / Access Token / Refresh Token；
- XSS / CSRF / SameSite / Same-Origin / CORS / Preflight；
- Strong / Conditional Cache、ETag、Content Hash、CDN；
- HTTP/1.1 / 2 / 3、QUIC；
- DOM / CSSOM / Layout / Paint / Composite；
- script / async / defer；
- DOMContentLoaded / load；
- Reflow / Repaint；
- Forced Synchronous Layout / Layout Thrashing 的现象已理解，术语仍需间隔复习。

详见：

- [[03-Knowledge/Web/01-url-dns-tcp-tls-http]]
- [[03-Knowledge/Web/02-cors-auth-security]]
- [[03-Knowledge/Web/03-cache-cdn-http-versions]]
- [[03-Knowledge/Web/04-browser-rendering]]

## 当前全栈学习主线

### JavaScript 基础

2026-08-27 已完成第一轮：

- `let` / `const`；
- variable / binding / value；
- `const` 与对象属性修改；
- JavaScript 动态类型：值有类型，变量不被固定为某一种类型；
- `number` / `string` / `boolean`；
- `undefined` / `null`；
- `typeof`；
- `typeof null === "object"` 的历史兼容问题；
- `==` 与 `===`，默认优先严格相等。

当前这些内容刚完成第一轮，不提前标记为 `understood`；后续通过间隔回忆确认。

### 下一学习断点

下一次从：

```text
对象 / 数组的基本模型
→ 属性访问
→ 对象与引用直觉
→ 函数
→ 作用域 / 闭包 / this / prototype
→ DOM / Event
→ Promise / async-await / Event Loop
→ fetch / JSON / API
→ TypeScript
→ React
→ Node.js Backend
→ SQL / Database
→ Auth / Full-stack interaction
→ Linux / Docker / Deployment / CI
```

不重复从 Web / Network 开始，也不提前跳到 React。

## 算法主线

使用 LeetCode Hot 100 作为主要题池，由题型和当前能力安排顺序，不机械按网页顺序。

### 已完成

2026-08-27：LeetCode 49「字母异位词分组」第一轮完成。

核心：

```text
每个字符串复制为 key
→ 对 key 排序
→ 排序结果作为 unordered_map 的键
→ key 相同的原字符串进入同一 vector
→ 收集所有 pair.second 形成最终答案
```

复杂度：

- 时间：`O(n * k log k)`；
- 空间：`O(n * k)`。

本次暴露的实现点：

- `std::sort` 原地排序，不返回排序结果；
- `unordered_map<string, vector<string>>` 是中间分组结构，不能直接返回为 `vector<vector<string>>`；
- 最终通过遍历哈希表收集 `pair.second`；
- C++ 嵌套 `vector` 类型仍需通过实践继续稳定。

### LeetCode 49 复习节点

- D+1：2026-08-28，口述思路 / 数据结构 / 复杂度；
- D+3：2026-08-30，不看答案恢复关键实现；
- D+7：2026-09-03，重新独立完成或完整推导；
- D+21：2026-09-17，随机抽查。

## 每日执行规则

详见：[[01-Roadmap/bytedance-fullstack-daily-plan]]。

每天开始时固定给出：

```text
今日学习主题
完成标准
今日算法新题
需要复习的旧题（如有）
今日停止线
```

每天完成固定任务后立即结束字节准备，不追加第二个知识主题或第二道新算法题。

## 最近一次会话

[[05-Progress/Sessions/2026-08-27-bytedance-day-1]]
