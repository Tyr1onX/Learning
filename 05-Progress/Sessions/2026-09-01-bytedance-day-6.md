---
tags:
  - progress
  - session
  - bytedance
  - javascript
  - algorithm
status: completed
updated: 2026-09-01
---

# 2026-09-01 字节准备 Day 6

## 今日固定任务

1. LeetCode 283 D+3 轻量复习；
2. LeetCode 15 D+1 轻量复习；
3. JavaScript：prototype / 原型基础；
4. LeetCode Hot 100：42. 接雨水。

固定任务完成后停止，不额外加量。

## LeetCode 283 D+3

复习通过：

- `write` 表示下一个非零元素应该放的位置；
- 遇到 0 直接跳过；
- 遇到非零与 `nums[write]` 交换后 `write++`；
- 从左到右依次处理，所以非零元素相对顺序保持；
- 时间 `O(n)`，额外空间 `O(1)`。

口误：曾把 `write` 说成 `right`，理解本身正确。

## LeetCode 15 D+1

复习通过：

- 先排序，为固定 `i` 后的左右双指针提供单调移动依据；
- `left = i + 1`，`right = n - 1`；
- `sum < 0` 时 `left++`，`sum > 0` 时 `right--`；
- `sum == 0` 时记录答案、左右移动并跳过重复值；
- `i` 也需要跳过重复值；
- 去重目标是避免重复输出相同三元组，不是禁止三元组里出现相同数值；
- 时间复杂度 `O(n^2)`；
- 双指针自身辅助空间 `O(1)`，考虑 C++ `std::sort` 常见递归栈时整体辅助空间通常记 `O(log n)`；输出空间另记 `O(k)`。

## JavaScript：prototype / 原型基础

完成第一轮：

- 对象访问属性时先找自身；
- 自身没有时沿原型向上查找；
- 原型也没有时继续沿原型链查找，最终到 `null`；
- `Object.create(animal)` 可理解为创建新对象并让 `animal` 成为其原型；
- 对象自己的同名属性会遮蔽原型上的同名属性；
- `Dog.prototype` 可先理解为多个 `Dog` 实例共享的公共原型对象；
- 实例自己的数据属性与 `prototype` 上的共享方法可以分开存放；
- `d1.sayName === d2.sayName` 可为 `true`，因为二者沿原型找到同一个共享函数。

当前只掌握原型 / 原型链基础，不继续展开 `new` 的完整内部机制。

## 算法：LeetCode 42 接雨水

### 核心理解

某个位置能接的水：

```text
min(leftMax, rightMax) - height[i]
```

其中：

- `left/right` 是当前处理位置的下标；
- `height[left]/height[right]` 是当前柱子高度；
- `leftMax/rightMax` 是两侧目前见过的最高柱子；
- 双指针每轮直接结算 `left` 或 `right` 当前指向的位置，不需要第三个中间指针。

双指针规则：

- 若 `leftMax <= rightMax`，当前左侧位置水量已经确定，累加 `leftMax - height[left]` 后 `left++`；
- 否则处理右侧，累加 `rightMax - height[right]` 后 `right--`。

### 实现结果

独立写出整体结构，但第一次把下标误用于更新最大高度：

```cpp
leftMax = max(left, leftMax);
rightMax = max(right, rightMax);
```

修正为：

```cpp
leftMax = max(height[left], leftMax);
rightMax = max(height[right], rightMax);
```

同时将循环边界从 `left <= right` 调整为更清晰的 `left < right`。修正后通过。

### 复杂度

- 时间复杂度：`O(n)`，`left/right` 只从两端单向向中间移动；
- 额外空间复杂度：`O(1)`，只使用常数个变量。

## 复习计划

### LeetCode 42

- D+1：2026-09-02，口述为什么某侧 `Max` 较小时可以结算该侧当前位置；区分下标与高度；
- D+3：2026-09-04，不看答案恢复双指针代码；
- D+7：2026-09-08，重新独立完成或完整推导；
- D+21：2026-09-22，随机抽查。

### prototype

后续间隔复习重点：

- 自身属性 vs 原型属性；
- `Object.create` 的基础含义；
- 原型链查找顺序；
- 实例属性与 `prototype` 共享方法的区别。

## 晚间轻量复习

2026-09-01 已执行轻量回忆，不新增知识或算法题。

脱离笔记应能口述的最小集合：

- `prototype`：属性查找先自身、再沿原型链；自身同名属性遮蔽原型属性；`Object.create(proto)` 建立原型关系；实例数据与 prototype 共享方法分开理解。
- LeetCode 283：`write` 是下一个非零元素写入位置；时间 `O(n)`、额外空间 `O(1)`。
- LeetCode 15：排序后固定 `i`，其余区间双指针，根据 sum 正负移动并去重；时间 `O(n^2)`。
- LeetCode 42：`left/right` 是下标，更新最大高度必须使用 `height[left/right]`；依据较小一侧的 Max 结算当前位置；时间 `O(n)`、额外空间 `O(1)`。

继续保留的易错点：

- 不把 LeetCode 283 的 `write` 口误成 `right`；
- LeetCode 42 严格区分“下标”和“柱子高度”，不能写成 `max(left, leftMax)`；
- LeetCode 42 的 D+1 重点仍是解释为什么较小 Max 一侧可以立即结算，而不是只背代码。

今晚到此停止，不推进下一主题。

## 下一次入口

下一次开始时：

1. 执行当天到期旧题复习；
2. JavaScript 从 prototype 之后继续下一个单日主题；
3. 安排当天唯一一道 Hot 100 新题；
4. 固定任务完成后停止。
