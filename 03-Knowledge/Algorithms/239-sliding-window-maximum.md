---
tags:
  - knowledge
  - algorithm
  - hot-100
  - deque
  - sliding-window
status: learning
updated: 2026-09-09
---

# LeetCode 239 滑动窗口最大值

## 题意

给定整数数组 `nums` 和窗口大小 `k`。窗口从数组最左边开始，每次向右移动一格，返回每个长度为 `k` 的连续窗口中的最大值。

例子：

```text
nums = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3
输出：[3, 3, 5, 5, 6, 7]
```

## 暴力法

每个窗口都重新扫描 `k` 个元素找最大值。

```text
窗口数量：n - k + 1
每个窗口扫描：k
时间复杂度：O(nk)
辅助空间：O(1)（不计答案）
```

## 单调队列直觉

维护一个“未来有机会成为最大值”的候选队列。

核心规则：

```text
队列从头到尾，对应值保持递减
队头永远是当前窗口最大值
新元素进来时，从队尾弹出所有比它小的旧元素
```

如果新来的元素比队尾旧元素更大，而且位置更靠右，那么这些更小的旧元素未来不可能成为最大值，可以删除。

## 为什么存下标

队列通常存下标，不直接存值。

原因：

```text
1. 用下标判断元素是否已经滑出窗口
2. 用 nums[index] 访问对应值，继续比较大小
```

窗口右边界为 `i`，窗口左边界为：

```text
i - k + 1
```

队头过期条件：

```cpp
dq.front() < i - k + 1
```

比较队尾值：

```cpp
nums[dq.back()] < nums[i]
```

注意：`dq.back()` 是下标，不是值。

## C++ deque 操作

```cpp
deque<int> dq;

dq.push_back(i);   // 队尾加入下标 i
dq.pop_front();    // 删除队头
dq.pop_back();     // 删除队尾
dq.front();        // 取队头下标
dq.back();         // 取队尾下标
dq.empty();        // 判断是否为空
```

## 核心代码

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> ans;

    for (int i = 0; i < nums.size(); i++) {
        while (!dq.empty() && dq.front() < i - k + 1) {
            dq.pop_front();
        }

        while (!dq.empty() && nums[dq.back()] < nums[i]) {
            dq.pop_back();
        }

        dq.push_back(i);

        if (i >= k - 1) {
            ans.push_back(nums[dq.front()]);
        }
    }

    return ans;
}
```

## 复杂度

时间复杂度：`O(n)`。

关键理由不是只看外层一轮 `for`，而是每个下标最多入队一次、出队一次，因此总队列操作次数是线性的。

辅助空间复杂度：`O(k)`（不计输出数组）。宽松上界可写 `O(n)`，但面试中优先说 `O(k)`。

## 当前掌握状态

2026-09-09 第一轮学习完成，状态保持 `learning`。

已通过：

- 暴力法和 `O(nk)`；
- 单调队列保留未来可能成为最大值的候选；
- 新来的更大元素会让队尾更小元素失效；
- 队列存下标是为了同时判断过期和访问值；
- 窗口形成条件是 `i >= k - 1`；
- 辅助空间更准确为 `O(k)`。

待复习：

- 窗口范围是 `[i-k+1, i]`，不是单个下标 `i`；
- `dq.front() == i-k+1` 仍在窗口内，只有 `< i-k+1` 才过期；
- 比较队尾时必须写 `nums[dq.back()] < nums[i]`；
- 入队时必须写 `dq.push_back(i)`，不是 `dq.push_back(nums[i])`；
- 复杂度理由要说“每个下标最多入队一次、出队一次”。