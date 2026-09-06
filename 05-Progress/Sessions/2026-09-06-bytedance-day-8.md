---
tags:
  - progress
  - session
  - bytedance
  - javascript
  - algorithm
status: completed
updated: 2026-09-06
---

# 2026-09-06 字节准备 Day 8

## 今日固定任务

1. 补做逾期 / 到期算法轻量复习：49、15、128、283、11、42、438；
2. 旧基础知识轻量复习：变量 / 基础类型中的 `const` 与对象内部可变性；
3. JavaScript：Promise / async-await / Event Loop 基础；
4. LeetCode Hot 100：560. 和为 K 的子数组。

固定任务完成后停止，不额外加量。

## 旧算法复习结果

### LeetCode 49 D+7（逾期补复习）

通过：字母异位词排序后得到相同标准化 key，因此可用 `unordered_map<string, vector<string>>` 分组。

### LeetCode 15 D+3（逾期补复习）

通过：排序后固定 `i`，`sum < 0` 时 `left++`，`sum > 0` 时 `right--`；时间 `O(n^2)`。

### LeetCode 128 D+7（逾期补复习）

通过：只有 `x - 1` 不存在时 `x` 才是连续序列起点；非起点不启动内部 `while`，平均时间 `O(n)`、空间 `O(n)`。

### LeetCode 283 D+7（逾期补复习）

通过：`write` 表示下一个非零元素写入位置；从左到右依次处理保证非零元素相对顺序不变；时间 `O(n)`、额外空间 `O(1)`。

### LeetCode 11 D+7

通过：面积由短板决定；移动较高边只会缩小宽度而短板不变，因此不可能得到更优结果，应移动较短边。

### LeetCode 42 D+3（逾期补复习）

通过：当前位置接水量由 `min(leftMax, rightMax)` 决定；当 `leftMax <= rightMax` 时左侧上限已确定，可直接结算 `leftMax - height[left]`。

### LeetCode 438 D+3（逾期补复习）

通过：异位词要求长度相同，所以窗口固定为 `p.size()`；右字符进入计数 `+1`，左字符退出计数 `-1`。

## 旧基础知识复习

### 变量 / 基础类型：`const` 与对象内部可变性

通过：`const` 限制变量绑定不能重新指向新值，但当前指向的对象内部属性仍可修改；`user.name = ...` 可以，`user = {...}` 不允许。

本轮确认早间与晚间流程必须都包含基础知识间隔复习，且晚间必须通过交互式无提示回忆后才能回写。

## JavaScript：Promise / async-await / Event Loop

完成第一轮基础：

- 当前同步代码先执行；
- `Promise.then` 与 `await` 后续属于微任务；
- 当前同步代码结束后先清空微任务，再处理 `setTimeout` 等后续任务；
- `async` 函数一定返回 Promise；
- 调用 `async` 函数时会先同步执行到第一个 `await`；
- `await` 不会阻塞整个 JavaScript，只暂停当前 async 函数后续执行；
- `await` 后面的代码之后以微任务继续。

### 实际表现

简单顺序题 `A / Promise.then(B) / C` 正确判断为 `A C B`。

综合题第一次把：

```text
同步：A B F
微任务：C E
任务：D
```

顺序判断错，随后能理解并确认正确结果为 `A B F C E D`。

当前易错点：

- 必须区分 `await` 之前仍同步执行、`await` 之后才进入后续微任务；
- 需要继续稳定“同步 → 微任务 → 任务”的执行顺序。

## 算法：LeetCode 560 和为 K 的子数组

### 题意理解

给定整数数组 `nums` 和整数 `k`，统计和恰好等于 `k` 的连续子数组数量。

### 核心模型

通过具体“切一刀”建模后理解：

```text
当前前缀和 = 之前某个前缀和 + 当前连续子数组和
```

因此若当前前缀和为 `sum`，要找和为 `k` 的子数组，就查找以前出现过多少次：

```text
sum - k
```

哈希表含义：

```text
key   = 前缀和
value = 这个前缀和以前出现的次数
```

若 `sum - k` 出现过多次，就对应多个不同切点，因此当前会新增相同数量的合法子数组。

`count[0] = 1` 表示遍历前“空前缀”的和为 0 出现过一次，使从数组开头到当前位置本身就是合法子数组的情况不会漏掉。

### 实现过程

第一次代码把哈希表方向写成了“下标 -> 前缀和”，并误用 `count()` 作为出现次数；经纠正后写出正确核心：

```cpp
unordered_map<int, int> count;
count[0] = 1;

int sum = 0;
int ans = 0;

for (int i = 0; i < nums.size(); i++) {
    sum += nums[i];
    ans += count[sum - k];
    count[sum]++;
}
```

当前需要稳定：

- `unordered_map` 中 key / value 的业务含义先明确再写代码；
- `count(key)` 主要判断 key 是否存在，不是取业务上的“出现次数”；
- 本题必须先更新当前 `sum`，再查询 `sum - k`，最后记录 `count[sum]++`；
- 有负数时窗口和不具备单调性，不能简单用“和太大就移动 left”的滑动窗口。

### 复杂度

- 平均时间复杂度：`O(n)`；
- 额外空间复杂度：`O(n)`。

## 后续复习节点

### Promise / async-await / Event Loop

- D+1：2026-09-07，重点无提示判断 `await` 前后与 Promise / setTimeout 的执行顺序；
- D+3：2026-09-09；
- D+7：2026-09-13；
- D+21：2026-09-27。

### LeetCode 560

- D+1：2026-09-07，口述题意、前缀和“切一刀”模型、`count[0] = 1`；
- D+3：2026-09-09，不看答案恢复代码；
- D+7：2026-09-13；
- D+21：2026-09-27。

## 下一次入口

1. 先执行当天到期的算法与旧基础知识复习；
2. 新知识主题进入 `fetch / JSON / API`；
3. 安排当天唯一一道 Hot 100 新题；
4. 固定任务完成后停止。
