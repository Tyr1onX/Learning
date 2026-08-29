---
tags:
  - current
  - learning
status: active
updated: 2026-08-29
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

2026-08-27 第一轮：

- `let` / `const`；
- variable / binding / value；
- JavaScript 动态类型；
- `number` / `string` / `boolean`；
- `undefined` / `null`；
- `typeof`；
- `typeof null === "object"`；
- `==` 与 `===`。

2026-08-28 第一轮：

- 对象 / 数组；
- `user.name` / `user["name"]` / `user[key]`；
- 对象 / 数组共享引用直觉；
- `const` 阻止重新绑定，但不阻止修改对象内部属性。

2026-08-29 第一轮：

- 函数定义与调用；
- 形参与实参；
- `return` 与返回值；
- 无显式 `return` 时返回 `undefined`；
- `return` 会立即结束当前函数；
- 局部变量与外层变量的基础作用域方向。

这些内容仍属于第一轮学习，不提前标记为 `understood`，后续通过间隔回忆确认。

### 当前下一学习断点

下一次从函数基础之后继续，单日只推进一个明确主题。候选顺序：

```text
作用域深化 / 闭包基础
→ this
→ prototype
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

不要一次跨越多个主题，也不要提前跳到 React。

## 算法主线

使用 LeetCode Hot 100 作为主要题池，由题型和当前能力安排顺序，不机械按网页顺序。

### 已完成

- 2026-08-27：LeetCode 49「字母异位词分组」；
- 2026-08-28：LeetCode 128「最长连续序列」；
- 2026-08-29：LeetCode 283「移动零」。

### 当前需要稳定的算法 / C++ 点

- `unordered_map<Key, Value>` 与 `vector<vector<T>>` 的模板结构；
- `vector` 用 `push_back()`，`unordered_set` 用 `insert()`；
- `unordered_set` 没有下标访问，范围 for 用 `for (int x : set)`；
- 局部基本类型变量不会自动初始化为 0；
- 128：只有连续序列起点才启动内部 `while`，因此平均时间 `O(n)`；
- 283：`write` 表示下一个非零元素写入位置；时间 `O(n)`，额外空间 `O(1)`；
- 复杂度分析时，输入本身占用的空间不算算法额外空间。

### 近期复习节点

LeetCode 49：

- D+3：2026-08-30；
- D+7：2026-09-03；
- D+21：2026-09-17。

LeetCode 128：

- D+3：2026-08-31；
- D+7：2026-09-04；
- D+21：2026-09-18。

LeetCode 283：

- D+1：2026-08-30；
- D+3：2026-09-01；
- D+7：2026-09-05；
- D+21：2026-09-19。

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

每天完成固定任务后立即结束字节准备，不追加第二个知识主题或第二道新算法题。重要知识点也要通过后续间隔回忆复习，不只复习算法。

## 最近一次会话

[[05-Progress/Sessions/2026-08-29-bytedance-day-3]]
