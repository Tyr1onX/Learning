---
tags:
  - progress
  - session
  - bytedance
  - javascript
  - algorithm
status: completed
updated: 2026-08-28
---

# 2026-08-28 字节准备 Day 2

## 今日固定任务

1. LeetCode 49 D+1 轻量复习；
2. JavaScript：对象 / 数组、属性访问、对象引用直觉；
3. LeetCode Hot 100：128. 最长连续序列。

当天任务完成后停止继续准备。

## LeetCode 49 D+1 复习结果

能够脱离代码恢复：

- 排序后的字符串可作为字母异位词公共 key；
- `unordered_map<string, vector<string>>` 用于 `key -> group`；
- `pair.first` 是 key，`pair.second` 是对应分组；
- 时间复杂度 `O(n * k log k)`；
- 空间复杂度 `O(n * k)`。

本次术语口误：曾将“字母异位词”说成“字母移位词”，已纠正。

## JavaScript 学习结果

完成对象 / 数组第一轮基础：

- `user.name` 与 `user["name"]` 都可访问属性；
- `user[key]` 会先求变量 `key` 的值，再把结果当作属性名；
- `user.key` 查找的是真正名为 `key` 的属性；
- 数组用下标访问，如 `arr[0]`；
- 对象 / 数组赋值时不会自动复制出一个新对象；
- `const user2 = user` 后，`user` 与 `user2` 引用同一个对象；
- 修改 `user2.age` 会反映到 `user.age`；
- `const a = { score: 60 }; const b = { score: 60 };` 会创建两个不同对象；
- `const` 限制变量重新赋值 / 重新绑定，不禁止修改对象内部属性；
- 数组与对象具有相同的共享引用直觉。

当前已能通过示例判断共享对象与独立对象，但“引用”概念仍属第一轮理解，后续需要间隔复习。

## 算法：LeetCode 128 最长连续序列

### 核心思路

- 先把所有数字放入 `unordered_set<int>`；
- 对每个 `x`，只有当 `x - 1` 不存在时，才把 `x` 作为连续序列起点；
- 从起点不断检查 `current + 1` 是否存在；
- 统计当前连续长度并更新全局最大值；
- 非起点元素不进入内部 `while`，因此每个连续序列只从起点完整扫描一次。

### C++ 基础补充

本次暴露出 STL 容器操作混淆：

- `vector` 尾插：`push_back()`；
- `unordered_set` 插入：`insert()`；
- `unordered_set` 查询：`count(value)`；
- `unordered_set` 没有下标访问，不用 `groups[i]`；
- 范围 for：`for (int x : groups)`；
- `unordered_map` 主要按 `key -> value` 访问，如 `mp[key]`。

还暴露出局部变量初始化问题：

```cpp
int ans;
```

不会自动得到 `0`，可能是未定义的垃圾值；本题应显式写：

```cpp
int ans = 0;
```

未初始化 `ans` 时，LeetCode 曾返回异常大整数；初始化后通过测试。

### 复杂度

- 平均时间复杂度：`O(n)`；
- 空间复杂度：`O(n)`。

时间复杂度的正确理由不是“代码只遍历一次”，而是：

1. 建集合 `O(n)`；
2. 哈希集合 `count()` 平均 `O(1)`；
3. 只有序列起点会启动内部 `while`；
4. 每个连续序列不会从其中间元素重复向后完整扫描，因此所有内部扫描总量仍为 `O(n)`。

## 复习计划

### LeetCode 128

- D+1：2026-08-29，口述起点判断、为什么内部 while 不导致 `O(n^2)`、复杂度；
- D+3：2026-08-31，不看答案恢复关键实现；
- D+7：2026-09-04，重新独立完成或完整推导；
- D+21：2026-09-18，随机抽查。

### JavaScript 对象 / 数组

晚间与后续间隔复习重点：

- `user.key` vs `user[key]`；
- `const b = a` 是否创建新对象；
- 对象 / 数组共享引用；
- `const` 与对象内部可变性的关系。

## 下一次入口

下一次“今天准备字节”时：

1. 先做 LeetCode 128 的 D+1 轻量复习；
2. JavaScript 继续对象 / 数组之后的函数基础，不重复今天内容；
3. 再安排当天唯一一道 Hot 100 新题；
4. 当天固定任务完成后停止。
