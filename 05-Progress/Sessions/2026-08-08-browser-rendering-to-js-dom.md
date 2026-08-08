---
tags:
  - progress
  - session
  - browser
  - javascript
status: completed
updated: 2026-08-08
---

# 2026-08-08 Browser Rendering → JavaScript / DOM

## 本次学习主线

本次会话从 Browser Rendering Pipeline 继续，完成浏览器渲染主干第一轮，并发现一个新的学习问题：现象通常能理解，但由于尚未系统学习 JavaScript / DOM，一些具体 API 名称和英文专有术语很难主动记住。

因此路线从继续深挖 `requestAnimationFrame` / Event Loop 调整为：

```text
Browser Rendering 第一轮完成
→ JavaScript 最低必要基础
→ DOM / Event
→ Promise / async-await / Event Loop
→ fetch / JSON / API
→ Backend
```

## 已经通过口头回答确认的内容

### HTML 与 DOM

学习者能够说明：HTML 本质上是文本 / 标记源码；DOM 是浏览器解析之后形成、可被 JavaScript 操作的对象结构。

关键纠正：`display:none` 后不是“元素不占内存 / DOM 中不存在”，而是 DOM 节点仍可存在，但不生成正常布局盒、不参与 Layout、不占页面布局空间。

### `display:none` / `visibility:hidden` / `opacity:0`

能够区分：

```text
display:none
→ DOM 可存在
→ 不参与正常 Layout
→ 不占布局空间

visibility:hidden
→ DOM 存在
→ 仍参与 Layout / 占空间
→ 不可见

opacity:0
→ DOM 存在
→ 仍参与 Layout / 占空间
→ 完全透明
→ 默认仍可能被鼠标点击
```

### `transform` / `opacity` / `transition`

已理解：

- `transform` = 变换，可移动 / 缩放 / 旋转；
- `opacity` = 不透明度；
- `transition` = 属性从旧值到新值的平滑过渡；
- `opacity:1 → 0` 可以产生连续淡出，而 `display:none` 更接近离散开关；
- 实际隐藏可先用 `opacity` 做视觉淡出，再让元素真正退出布局。

能够解释为什么频繁修改 `left` / `width` 可能触发 Layout / Paint，而 `transform` / `opacity` 在合适情况下更适合动画。

### 普通 script / async / defer

能够自己回答：普通 JS 之所以可能阻塞 HTML Parser，更核心的原因是 JS 可以改变 DOM / 文档解析结果，而不是简单因为“JS 能重新 Paint”。

`async`：

```text
下载与 HTML Parsing 并行
→ 谁先下载完，谁可能先执行
→ 不保证声明顺序
```

已正确判断：A 写在 B 前面，但 B 下载更快时，B 可能先执行。

`defer`：

```text
下载与 HTML Parsing 并行
→ 执行推迟到文档解析之后
→ 保持声明顺序
```

已正确判断：即使 B 100ms 下载完成、A 1000ms 才完成，B 也需要等 A，按 A → B 执行。

### DOMContentLoaded / load

已正确回答：HTML / DOM 已解析完成、但 50MB 大图片仍在下载时，`DOMContentLoaded` 可以触发，而 `load` 暂时不会。

### CSS 对 Parsing / Rendering 的影响

已理解：CSS 通常不直接阻塞 HTML Parser，因此 DOM 可以继续构建；但关键 CSS 会影响首次正确渲染。

已能够进一步推理间接等待链：

```text
HTML Parser 等普通 JS
JS 需要最终 CSS 信息
JS 等 CSS
↓
CSS 间接拖住后续 HTML Parsing
```

### Reflow / Repaint / Forced Synchronous Layout / Layout Thrashing

已经理解现象：

```js
box.style.width = "500px";
const width = box.offsetWidth;
```

浏览器本可延迟 / 批量计算 Layout，但第二句要求立即得到真实几何值，因此不能随便返回旧值，可能被迫立即执行同步 Layout。

如果反复：

```text
写布局
→ 读布局
→ Layout
→ 再写
→ 再读
→ 再 Layout
```

就会形成 Layout Thrashing。

当前问题不是现象不理解，而是 `offsetWidth`、Forced Synchronous Layout、Layout Thrashing 等 API / 专有名词很难在没有系统 JS / DOM 基础时主动记忆。因此这些术语暂不判为熟练。

## JavaScript / DOM 新起点

开始拆解：

```js
const title = document.querySelector(".title");
```

当前已经建立的理解：

```text
const
→ JavaScript 变量声明关键字；绑定不能被重新赋值

title
→ 自己起的变量名，用来保存右边表达式的结果

document
→ 浏览器提供的 Document 对象，代表当前整个文档，是 DOM 树的重要入口

querySelector(...)
→ document 上的方法，用 CSS Selector 查找第一个匹配的 DOM 元素

".title"
→ 普通 JavaScript 字符串
→ 由 querySelector 按 CSS Selector 语法解释
→ . 表示 class selector
```

### 本次最后纠正的两个点

1. `document` 不是 HTML 中某一个具体 DOM Element；它是代表整个当前文档的 `Document` 对象。
2. `".title"` 本身不是“CSS 解析器”；它只是字符串，是 `querySelector` 按 CSS Selector 规则解释它。

如果没有找到匹配元素，`querySelector` 可以返回 `null`；这一点以后在值 / 类型和空值处理中展开。

## 学习策略变化

学习者有 C++ 基础，因此后续 JavaScript 可利用以下概念做类比：

```text
变量
成员访问 .
函数 / 方法调用
条件 / 循环
对象的直觉
```

但需要明确 JavaScript 的动态类型、对象模型、绑定 / 引用语义并不等同于 C++。

针对术语记忆，后续按三层处理：

```text
先理解现象
→ 再贴正式术语
→ 间隔复习后要求主动说出术语
```

DOM API 第一次出现只要求知道用途，不强求立刻背名字。

## 下一窗口精确入口

从下面这句继续：

```js
const title = document.querySelector(".title");
```

下一步顺序：

```text
const / let
→ JavaScript 的值与基本类型
→ 对象与“对象.属性”
→ 函数 / 方法
→ DOM Element
→ 修改 textContent / style
→ addEventListener / Event
→ Promise / async-await / Event Loop
→ fetch / JSON / API
→ 正式进入 Backend
```

## 自动交接规则

学习者要求：以后只要明确提出准备切换 / 新开聊天窗口，就自动先同步本次学习增量到 GitHub `Tyr1onX/Learning`，不只写当前断点，还要更新对应知识笔记、学习状态和 Session 记录，然后再给简短的新窗口交接词。该规则已经写入 [[02-Current/learning-context]]。