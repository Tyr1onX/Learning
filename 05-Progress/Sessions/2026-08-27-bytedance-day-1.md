---
tags:
  - progress
  - session
  - bytedance
  - javascript
  - algorithm
status: completed
updated: 2026-08-27
---

# 2026-08-27 字节准备 Day 1

## 今日固定任务

1. JavaScript：变量、值与基本类型；
2. LeetCode Hot 100：49. 字母异位词分组。

当天两项完成后停止继续准备。

## JavaScript 学习结果

完成第一轮：

- `let` / `const`；
- variable / binding / value 的区别；
- `const` 对对象限制的是变量不能重新绑定到另一个对象，不代表对象属性不可修改；
- JavaScript 动态类型的核心：值有类型，变量不被固定为某一种类型；
- `number` / `string` / `boolean`；
- `undefined` / `null`；
- `typeof`；
- `typeof null === "object"` 是历史兼容问题，不能据此把 `null` 当作普通对象；
- `==` 会发生隐式类型转换，日常默认优先 `===`。

### 本次需要继续固定的准确表达

- 不说“重新复制”，应说“重新赋值”；
- `let x;` 中 `x` 已经声明，只是当前值为 `undefined`；
- 对象中的 `age` 是属性，不是一个因为 `user` 指向它而存在的独立变量；
- 动态类型不要表述成“变量自己不断改变类型”，更准确是变量可以先后绑定不同类型的值。

### 当前判断

今天能够在连续提问后独立解释主干，但属于刚完成第一轮，暂不升级为 `understood`，后续需要间隔回忆。

## 算法：LeetCode 49 字母异位词分组

### 独立形成的核心思路

对每个字符串复制出一个 `key`，对 `key` 的字符排序；字母异位词排序后会得到相同字符串，因此可用排序结果作为哈希表键：

```text
sorted string -> vector<original strings>
```

C++ 结构：

```cpp
unordered_map<string, vector<string>> groups;
```

最终把每个 `pair.second` 收集到 `vector<vector<string>>` 返回。

### 本次暴露的 C++ 实现点

- `std::sort` 是原地排序，不返回排序后的字符串；正确写法是复制后 `sort(key.begin(), key.end())`；
- 中间哈希表不能直接作为函数返回值，因为函数要求 `vector<vector<string>>`；
- 最终答案类型应写 `vector<vector<string>>`，曾误写成 `vector<string, vector<string>>`；
- `pair.first` 是 key，`pair.second` 是该 key 对应的一组字符串。

### 复杂度

设字符串数量为 `n`，平均长度为 `k`：

- 时间复杂度：`O(n * k log k)`；
- 空间复杂度：`O(n * k)`。

学习者能够自行推出：每个长度为 `k` 的字符串排序为 `O(k log k)`，对 `n` 个字符串处理得到 `O(n * k log k)`。

## 晚间复习结果

2026-08-27 晚间进行了脱离笔记回忆，整体保留良好：

- 能准确区分 `let` 与 `const` 的重新赋值规则；
- 能解释 `const` 对象允许修改属性，但不能把变量重新赋给另一个对象；
- 能区分 `undefined` 与 `null`；
- 能说明 `===` 同时要求类型和值匹配，而 `==` 会发生隐式类型转换；
- 能解释动态类型的核心，但口述时把 JavaScript 误说成 TypeScript，需要继续固定术语；
- 能解释字母异位词排序后得到同一 key，并正确复述完整分组流程；
- 能独立恢复时间复杂度 `O(n * k log k)` 与空间复杂度 `O(n * k)`；
- `vector<vector<string>>` 已理解为“外层 vector 的元素类型是 `vector<string>`”；
- `unordered_map<string, vector<string>>` 的两个模板参数仍需固定：第一个是 Key 类型 `string`，第二个是 Value 类型 `vector<string>`，不是“数据类型 + 管理方法”。

### 晚间复习后重点

下一次优先抽查：

1. JavaScript ≠ TypeScript；当前学习的是 JavaScript 动态类型；
2. `unordered_map<Key, Value>`：`string` 是 Key 类型，`vector<string>` 是 Value 类型；
3. `vector<vector<string>>`：外层每个元素都是一个 `vector<string>`。

## 复习计划

LeetCode 49 进入复习池：

- D+1：2026-08-28，口述核心思路、数据结构和复杂度；
- D+3：2026-08-30，不看答案恢复关键实现；
- D+7：2026-09-03，重新独立完成或完整推导；
- D+21：2026-09-17，随机抽查。

## 下一次入口

下一次“今天准备字节”时：

1. 先做 LeetCode 49 的 D+1 轻量复习，不把它算作新题；
2. JavaScript 从“对象 / 数组的基本模型与属性访问”继续，不重复今天内容；
3. 再安排当天唯一一道 Hot 100 新题；
4. 当天固定任务完成后停止。
