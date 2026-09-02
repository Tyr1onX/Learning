---
tags:
  - progress
  - session
  - bytedance
  - javascript
  - dom
  - event
  - algorithm
status: completed
updated: 2026-09-02
---

# 2026-09-02 字节准备 Day 7

## 今日固定任务

1. LeetCode 11 D+3 轻量复习；
2. LeetCode 42 D+1 轻量复习；
3. JavaScript：DOM / Event 基础；
4. LeetCode Hot 100：438. 找到字符串中所有字母异位词。

固定任务完成后停止，不额外加量。

## LeetCode 11 D+3

复习通过：

- 容器面积由 `min(height[left], height[right]) * (right - left)` 决定；
- 当前较矮的一侧是短板；
- 若移动较高的一侧，宽度一定缩小，而短板上限不变，因此不可能得到比当前更优的面积；
- 移动较矮的一侧虽然宽度缩小，但有机会遇到更高的新短板；
- 时间复杂度 `O(n)`，额外空间 `O(1)`。

## LeetCode 42 D+1

复习通过：

- 单点接水量由 `min(leftMax, rightMax) - height[i]` 决定；
- 当 `leftMax <= rightMax` 时，左侧当前位置的限制边界已经由 `leftMax` 决定，因此可以直接结算 `leftMax - height[left]`；
- 即使右侧以后遇到更高柱子，较小边界仍然是 `leftMax`；
- `left/right` 是下标，`height[left]/height[right]` 才是高度；
- 时间复杂度 `O(n)`，额外空间 `O(1)`。

## JavaScript：DOM / Event 基础

完成第一轮基础学习：

- `document` 可理解为 JavaScript 访问当前页面 DOM 的入口；
- `document.querySelector("#id")` 返回匹配的第一个 DOM 元素对象，而不是元素中的文本字符串；
- `textContent` 可用于读取或修改元素文本内容；
- 常见元素属性可直接通过 DOM 对象修改，例如 `img.src`；
- `addEventListener("click", handler)` 会注册事件处理函数，函数在事件发生时再由浏览器调用，而不是注册时立即执行；
- 浏览器会在事件发生时向处理函数提供 `event` 对象；
- `event.target` 表示这次事件实际发生的元素；
- 已理解最小交互链路：找到元素 → 注册事件 → 用户触发 → 修改 DOM。

### 实际练习

能够在提示后独立写出：

```js
const message = document.querySelector("#message");
const change = document.querySelector("#change");

change.addEventListener("click", function () {
    message.textContent = "修改成功";
});
```

### 当前易错点

- 第一轮从零写语法时不熟练，需要先通过填空恢复固定结构；
- `querySelector`、`textContent` 等 API 名称区分大小写；
- CSS 选择器参数必须是字符串，例如 `document.querySelector("#message")`，曾漏写引号；
- 当前只掌握 DOM / Event 最基础交互，不提前扩展事件冒泡、捕获等复杂机制。

## 算法：LeetCode 438 找到字符串中所有字母异位词

### 核心理解

- 字母异位词必须与 `p` 长度相同，因此只需要维护长度固定为 `p.size()` 的窗口；
- 判断异位词本质是比较各字符出现次数，而不是比较字符顺序；
- 使用两个长度为 26 的计数数组：`need` 统计 `p`，`window` 统计当前窗口；
- 右侧新字符进入时对应计数 `+1`；
- 窗口过长时，最左字符计数 `-1`，随后 `left++`；
- 当 `window == need` 时，当前窗口是异位词，记录起点 `left`。

### 实现过程

第一版代码已经建立 `need/window/ans` 和左右边界框架，但有以下问题：

- `right` 从 `p.size() - 1` 开始时没有先把初始窗口加入 `window`；
- 窗口缩小时误删了 `right` 对应字符，应删除 `left` 对应字符；
- `right <= s.size()` 存在越界风险；
- 判断窗口是否匹配的时机需要放在“加入右字符、必要时缩窗”之后。

修正后独立写出：

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> need(26, 0);
        vector<int> window(26, 0);
        vector<int> ans;
        for (int i = 0; i < p.size(); i++) {
            need[p[i] - 'a']++;
        }

        int left = 0;

        for (int right = 0; right < s.size(); right++) {
            window[s[right] - 'a']++;

            if (right - left + 1 > p.size()) {
                window[s[left] - 'a']--;
                left++;
            }

            if (window == need) ans.push_back(left);
        }
        return ans;
    }
};
```

### 复杂度

- 主循环线性扫描 `s`，`left/right` 都只单向移动；
- `window == need` 比较固定 26 个位置，可视为常数开销；
- 时间复杂度 `O(n)`；
- 两个计数数组长度固定为 26，额外空间复杂度 `O(1)`。

复杂度部分首次回答时误以为可能是 `O(1)`，需要继续稳定“固定数组比较是常数，但外层仍有长度为 n 的遍历”这一点。

## 晚间轻复习

仅回顾今天已完成内容，没有新增知识或算法题，也没有提前推进下一主题。

### 脱离细节后的核心回忆框架

- DOM / Event：`document` 找到页面元素；`querySelector("#id")` 得到 DOM 元素对象；`addEventListener` 先注册处理函数，事件发生后浏览器再调用；处理函数可通过 `textContent` 修改页面，`event.target` 指向实际触发事件的元素。
- 11 盛最多水的容器：面积由宽度和短板共同决定，只移动较矮边，因为移动高边只会缩宽度且短板上限不变；`O(n)` / `O(1)`。
- 42 接雨水：当前位置由左右最高边界中的较小者限制；双指针每次结算已确定的一侧；注意指针是下标、高度要写 `height[left/right]`；`O(n)` / `O(1)`。
- 438 字母异位词：固定 `p.size()` 长度的滑动窗口，右进 `+1`、超长时左出 `-1` 并 `left++`，两个 26 长度计数数组相等时记录 `left`；`O(n)` / `O(1)`。

### 继续保留的易错点

- DOM API 名称大小写与 `querySelector("#id")` 中选择器必须写成字符串；
- 438 缩窗时删除的是 `s[left]`，不是刚进入的 `s[right]`；
- 遍历字符串使用 `right < s.size()`，避免 `right == s.size()` 时越界；
- 438 的 26 项数组比较是常数开销，但外层仍扫描长度为 `n` 的字符串，所以时间复杂度是 `O(n)`，不是 `O(1)`。

本次为非交互式轻复习，因此不把“看过回顾”误记为新的无提示回忆通过；上述易错点继续留给后续到期复习验证。

## 复习计划

### LeetCode 438

- D+1：2026-09-03，口述为什么窗口长度固定为 `p.size()`，以及窗口右移时哪两个计数发生变化；
- D+3：2026-09-05，不看答案恢复滑动窗口代码；
- D+7：2026-09-09，独立完成并说明复杂度；
- D+21：2026-09-23，随机抽查。

### DOM / Event

后续间隔复习重点：

- `querySelector("#id")` 的固定语法；
- `addEventListener("click", handler)` 的注册时机；
- `textContent` 修改文本；
- `event.target` 的基础含义；
- 独立从零写出一个“点击按钮 → 修改文本”的最小交互。

## 下一次入口

下一次开始时：

1. 执行当天到期旧题复习；
2. JavaScript 从 DOM / Event 之后继续下一个单日主题：Promise / async-await / Event Loop；
3. 安排当天唯一一道 Hot 100 新题；
4. 固定任务完成后停止。
