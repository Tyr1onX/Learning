---
tags:
  - current
  - learning
status: active
updated: 2026-08-30
---

# 当前学习焦点

## 当前总目标

面向下一次字节跳动日常实习 / 暑期实习，按“每天一个明确学习主题 + 一道 Hot 100 算法任务”的固定节奏推进全栈能力。当天任务完成后停止继续备战，避免无休止加量。

## 已完成主干

Web / Network / Browser 已完成一轮系统学习并经过无提示混合回忆，主干维持 `understood`。详见 `03-Knowledge/Web/`。

## 当前全栈学习主线

### JavaScript 基础已完成第一轮

2026-08-27：

- `let` / `const`；
- variable / binding / value；
- JavaScript 动态类型；
- 基础类型、`undefined` / `null`、`typeof`；
- `==` 与 `===`。

2026-08-28：

- 对象 / 数组；
- 属性访问；
- 对象 / 数组共享引用直觉；
- `const` 与对象内部可变性。

2026-08-29：

- 函数定义与调用；
- 形参与实参；
- `return`；
- 无显式 `return` 时的 `undefined`；
- 函数局部变量与基础作用域方向。

2026-08-30：

- 词法作用域基础：变量从当前作用域向外查找；
- `let` / `const` 块级作用域；
- shadowing；
- `return fn` vs `return fn()`；
- 闭包基础直觉：函数返回后仍可访问定义时引用的外层变量；
- 多次调用外层函数可创建彼此独立的闭包状态。

这些内容仍处于第一轮 + 间隔复习阶段，不提前整体标记为 `understood`。闭包表述仍需继续稳定。

### 当前下一学习断点

下一个单日主题候选顺序：

```text
this
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

每天只推进一个明确主题，不一次跨越多个主题。

## 算法主线

### 已完成第一轮

- 2026-08-27：LeetCode 49「字母异位词分组」；
- 2026-08-28：LeetCode 128「最长连续序列」；
- 2026-08-29：LeetCode 283「移动零」；
- 2026-08-30：LeetCode 11「盛最多水的容器」核心双指针与证明已理解；当时无电脑，完整 C++ 实现待补。

### 当前需要稳定的算法 / C++ 点

- `unordered_map<Key, Value>` 与 `unordered_set` 的语义区别；
- `vector` / `unordered_set` / `unordered_map` 的基础操作；
- 局部基本类型变量不会自动初始化为 0；
- 复杂度分析时区分输入空间与额外辅助空间；
- 49：`unordered_map<string, vector<string>>`，不是 `unordered_set`；
- 128：只有连续序列起点启动内部 `while`，平均时间 `O(n)`；
- 283：遇到 0 不处理，遇到非零才交换到 `write`；时间 `O(n)`，额外空间 `O(1)`；
- 11：若移动较高边，则宽度减小且短板仍限制高度，因此不会更优；应移动较短边。

### 近期复习节点

LeetCode 49：
- D+7：2026-09-03；
- D+21：2026-09-17。

LeetCode 128：
- D+3：2026-08-31；
- D+7：2026-09-04；
- D+21：2026-09-18。

LeetCode 283：
- D+3：2026-09-01；
- D+7：2026-09-05；
- D+21：2026-09-19。

LeetCode 11：
- D+1：2026-08-31，口述移动短边的安全性；方便时独立补 C++；
- D+3：2026-09-02；
- D+7：2026-09-06；
- D+21：2026-09-20。

## 每日执行规则

每天开始时固定给出：

```text
今日学习主题
完成标准
今日算法新题
需要复习的旧题（如有）
今日停止线
```

每天固定任务完成后立即结束，不追加第二个知识主题或第二道新算法题。重要知识点也通过间隔回忆复习。

## 最近一次会话

[[05-Progress/Sessions/2026-08-30-bytedance-day-4]]
