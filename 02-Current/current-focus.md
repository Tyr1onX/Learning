---
tags:
  - current
  - learning
status: active
updated: 2026-09-02
---

# 当前学习焦点

## 当前总目标

面向下一次字节跳动日常实习 / 暑期实习，按“每天一个明确学习主题 + 一道 Hot 100 算法任务”的固定节奏推进全栈能力。当天任务完成后停止继续备战，避免无休止加量。

## 已完成主干

Web / Network / Browser 已完成一轮系统学习并经过无提示混合回忆，主干维持 `understood`。详见 `03-Knowledge/Web/`。

## 当前全栈学习主线

### JavaScript 基础第一轮进度

2026-08-27：变量、基础类型、`undefined` / `null`、`typeof`、`==` / `===`。

2026-08-28：对象 / 数组、属性访问、共享引用直觉、`const` 与对象内部可变性。

2026-08-29：函数定义与调用、形参与实参、`return`、无显式 `return` 时的 `undefined`、局部变量与基础作用域方向。

2026-08-30：词法作用域、块级作用域、shadowing、`return fn` vs `return fn()`、闭包基础。

2026-08-31：`this` 基础：

- 普通函数的 `this` 主要看这一次怎么调用；
- 方法被取出后独立调用会丢失原对象调用关系；
- 普通内部函数不会自动继承外层方法的 `this`；
- 箭头函数没有自己的 `this`，使用外层词法环境中的 `this`。

2026-09-01：`prototype` / 原型基础：

- 对象先查找自身属性，自身没有时沿原型链向上查找；
- `Object.create(proto)` 可理解为创建新对象并把 `proto` 设为其原型；
- 自身同名属性会遮蔽原型同名属性；
- `Dog.prototype` 可作为多个实例共享的方法对象；
- 实例自己的数据属性与 prototype 上的共享方法是两回事；
- 暂不展开 `new` 的完整内部机制。

2026-09-02：DOM / Event 基础：

- `document` 是 JavaScript 访问当前页面 DOM 的入口；
- `document.querySelector("#id")` 返回匹配的 DOM 元素对象；
- `textContent` 可读取 / 修改元素文本；
- `addEventListener("click", handler)` 注册事件处理函数，事件发生时再执行；
- `event` 由浏览器在事件发生时提供，`event.target` 表示实际触发事件的元素；
- 已能在少量提示后独立写出“点击按钮 → 修改文本”的最小交互；
- 当前易错点是 DOM API 大小写、选择器字符串引号，以及从零恢复固定语法。

这些内容仍处于第一轮 + 间隔复习阶段，不提前整体标记为 `understood`。

### 当前下一学习断点

下一个单日主题候选顺序：

```text
Promise / async-await / Event Loop
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

### 已完成第一轮 / 当前状态

- 2026-08-27：LeetCode 49「字母异位词分组」；
- 2026-08-28：LeetCode 128「最长连续序列」；
- 2026-08-29：LeetCode 283「移动零」；
- 2026-08-30：LeetCode 11「盛最多水的容器」；
- 2026-08-31：LeetCode 15「三数之和」；
- 2026-09-01：LeetCode 42「接雨水」；
- 2026-09-02：LeetCode 438「找到字符串中所有字母异位词」滑动窗口实现已完成。

### 当前需要稳定的算法 / C++ 点

- `unordered_map<Key, Value>` 与 `unordered_set` 的语义区别；
- `vector` / `unordered_set` / `unordered_map` 的基础操作；
- 局部基本类型变量不会自动初始化为 0；
- 复杂度分析时区分输入空间、辅助空间、输出空间；
- 49：`unordered_map<string, vector<string>>`，不是 `unordered_set`；
- 128：只有连续序列起点启动内部 `while`，平均时间 `O(n)`；空间 `O(n)`；
- 283：`write` 表示下一个非零元素写入位置；时间 `O(n)`，额外空间 `O(1)`；
- 11：移动较高边只会缩小宽度而短板不变，因此应移动较短边；
- 15：排序 + 固定 `i` + 双指针 + 去重；时间 `O(n^2)`；不计输出时双指针本身 `O(1)`，考虑 `std::sort` 常见递归栈时通常 `O(log n)`；
- 42：`left/right` 是下标，`height[left]/height[right]` 才是高度；每轮依据 `leftMax/rightMax` 较小的一侧结算当前位置；时间 `O(n)`、额外空间 `O(1)`；
- 438：固定长度滑动窗口；右字符进入计数 `+1`，窗口过长时左字符计数 `-1` 后 `left++`；两个 26 长度数组相等时记录 `left`；时间 `O(n)`、额外空间 `O(1)`；复杂度易错点是固定 26 项比较为常数，但外层仍然有长度为 `n` 的遍历。

### 近期复习节点

LeetCode 49：
- D+7：2026-09-03；
- D+21：2026-09-17。

LeetCode 128：
- D+7：2026-09-04；
- D+21：2026-09-18。

LeetCode 283：
- D+7：2026-09-05；
- D+21：2026-09-19。

LeetCode 11：
- D+7：2026-09-06；
- D+21：2026-09-20。

LeetCode 15：
- D+3：2026-09-03；
- D+7：2026-09-07；
- D+21：2026-09-21。

LeetCode 42：
- D+3：2026-09-04；
- D+7：2026-09-08；
- D+21：2026-09-22。

LeetCode 438：
- D+1：2026-09-03；
- D+3：2026-09-05；
- D+7：2026-09-09；
- D+21：2026-09-23。

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

[[05-Progress/Sessions/2026-09-02-bytedance-day-7]]
