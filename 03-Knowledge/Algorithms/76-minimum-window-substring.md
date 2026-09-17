---
tags:
  - knowledge
  - algorithm
  - sliding-window
status: learning
updated: 2026-09-17
---

# LeetCode 76 最小覆盖子串

## 题意

在字符串 `s` 中寻找最短连续子串，使其包含字符串 `t` 中全部字符及对应出现次数。

例如：

```text
s = "ADOBECODEBANC"
t = "ABC"
```

答案为：

```text
"BANC"
```

若 `t = "AABC"`，则合法窗口必须至少包含两个 `A`、一个 `B`、一个 `C`。

## 滑动窗口模型

```text
窗口不满足 → 扩 right
窗口满足 → 记录答案并缩 left
缩到不满足 → 回到扩 right
```

维护：

```text
need[c]   = t 中字符 c 需要多少个
window[c] = 当前窗口中 c 有多少个
valid     = 当前已有多少种所需字符达到需求数量
```

当：

```cpp
valid == need.size()
```

说明当前窗口已经覆盖所有需要的字符种类。

## 右侧加入字符

```cpp
char c = s[right];
right++;

if (need.count(c)) {
    window[c]++;
    if (window[c] == need[c]) {
        valid++;
    }
}
```

只有某种字符第一次“刚好达到需求数量”时才 `valid++`；数量继续超出需求不会重复增加。

## 左侧移出字符

窗口满足后：

```cpp
while (valid == need.size()) {
    if (right - left < len) {
        start = left;
        len = right - left;
    }

    char d = s[left];
    left++;

    if (need.count(d)) {
        if (window[d] == need[d]) {
            valid--;
        }
        window[d]--;
    }
}
```

必须先判断 `window[d] == need[d]`，再 `window[d]--`，因为要捕捉“移走后将从满足变为不足”的临界点。

## 窗口边界

采用左闭右开：

```text
[left, right)
```

长度为：

```cpp
right - left
```

记录最短答案通常保存：

```cpp
start = left;
len = right - left;
```

最终：

```cpp
return len == INT_MAX ? "" : s.substr(start, len);
```

## 复杂度

- 构建 `need`：`O(|t|)`；
- `right` 每个字符最多纳入一次；
- `left` 每个字符最多移出一次；
- 平均哈希操作视为 `O(1)`；
- 总时间：`O(|s| + |t|)`；
- 辅助空间取决于字符集合 / 哈希表规模。

## 当前易错点

- `valid` 按“满足需求的字符种类”计数，不按字符总数计；
- 右侧加入后判断 `window[c] == need[c]`；
- 左侧移出前判断 `window[d] == need[d]`；
- 左闭右开窗口长度是 `right - left`，不是 `right - left - 1`。

## 状态

2026-09-17 第一轮完成；已在引导后独立写出核心滑动窗口更新代码。状态保持 `learning`。

复习：D+1 2026-09-18；D+3 2026-09-20；D+7 2026-09-24；D+21 2026-10-08。
