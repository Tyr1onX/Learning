---
tags:
  - web
  - browser
  - rendering
status: understood
updated: 2026-08-08
---

# Browser Rendering Pipeline

> 已完成第一轮系统讲解与口头推理。主干已经能够理解和解释；Reflow / Repaint、Forced Synchronous Layout、Layout Thrashing 等术语仍需后续间隔复习，不把“刚理解现象”误记成术语已熟练。

## 主干

```text
HTML
↓ parse
DOM

CSS
↓ parse
CSSOM

DOM + CSSOM
↓
Render Tree / Rendering Structure
↓
Layout
↓
Paint
↓
Composite
↓
Screen
```

## 1. HTML 与 DOM

HTML 是输入给浏览器的标记文本；DOM（Document Object Model）是浏览器解析 HTML 后在内存中形成的对象树。

示例 HTML：

```html
<div class="card">
  <h1>Hello</h1>
  <p>World</p>
</div>
```

可以粗略理解成：

```text
Document
└─ div.card
   ├─ h1
   │  └─ Hello
   └─ p
      └─ World
```

JavaScript 操作的是 DOM 对象，不是直接修改服务器上的原始 HTML 文件。

已能用自己的话说明：HTML 本质上是文本 / 标记源码，DOM 是浏览器处理后可供 JavaScript 操作的对象结构。

---

## 2. CSSOM

CSS 也是文本，浏览器解析后形成可用于样式计算的数据结构，基础学习中通常称 CSSOM（CSS Object Model）。

```text
DOM   → 页面有哪些节点 / 结构
CSSOM → 样式规则
```

浏览器结合节点与样式信息继续构建渲染所需结构。

---

## 3. `display:none` / `visibility:hidden` / `opacity:0`

三者都可能让用户“看不见元素”，但机制不同。

| 属性 | DOM 中存在 | 参与 Layout / 占空间 | 视觉可见 | 默认鼠标可点击 |
|---|---|---|---|---|
| `display: none` | 是 | 否 | 否 | 否 |
| `visibility: hidden` | 是 | 是 | 否 | 通常否 |
| `opacity: 0` | 是 | 是 | 否 | 是 |

重要纠正：`display:none` 不是“不占内存”。DOM 节点仍可存在于内存中，只是不生成正常布局盒、不参与正常 Layout、不占页面布局空间。

可以用直觉记忆：

```text
display:none
→ 人直接退出队伍，位置也没了

visibility:hidden
→ 人隐身，但队伍位置还留着

opacity:0
→ 人还站在那里，也可能还能被碰到，只是完全透明
```

`opacity:0` 默认仍可能接收鼠标事件；若不希望接收，可结合 `pointer-events:none` 等方式。

---

## 4. `transform` / `opacity` / `transition`

### `transform`

`transform` 可理解为“变换”，常见操作：

```css
transform: translateX(100px); /* 移动 */
transform: scale(1.2);        /* 缩放 */
transform: rotate(30deg);     /* 旋转 */
```

`transform` 视觉上移动元素时，通常不会像修改正常布局属性那样改变其在文档流中的原始布局位置。

### `opacity`

`opacity` = 不透明度：

```text
1   → 完全不透明
0.5 → 半透明
0   → 完全透明
```

### `transition`

`transition` = 过渡：当某个可插值 CSS 属性从旧值变成新值时，让浏览器在指定时间内计算中间状态。

```css
.card {
  transition: opacity 0.3s, transform 0.3s;
}
```

`opacity` 可以形成：

```text
1 → 0.8 → 0.6 → 0.4 → 0.2 → 0
```

因此适合淡入 / 淡出。

传统意义上的 `display:none` 更接近离散开关，不像 `opacity` 一样自然地表达连续的透明度变化。实际开发中常见思路是：先用 `opacity` 做视觉淡出，再在动画结束后真正退出布局。

---

## 5. Layout / Reflow

Layout 负责计算几何信息：

```text
width / height
x / y
父子 / 兄弟元素位置
文字换行
```

修改 `width`、某些定位几何属性等，可能让布局失效，需要重新进行 Layout。传统前端语境常把重新布局称为 Reflow / 重排。

例如持续修改 `left` / `width` 做动画，可能不断引发布局与后续绘制成本；而 `transform` / `opacity` 在合适情况下更容易走较轻的合成路径。

---

## 6. Paint / Repaint

Paint 负责把已确定几何位置和尺寸的内容绘制出来，例如：

```text
背景
边框
文字
阴影
图片
颜色
```

例如只改变背景颜色，几何信息通常不用重新 Layout，但需要重新 Paint。

重新绘制常称 Repaint / 重绘。

---

## 7. Composite

现代浏览器会把部分内容放入不同 Layer，最后在 Composite 阶段组合成最终画面。

粗略性能直觉：

```text
Layout + Paint + Composite
→ 通常成本更高

Paint + Composite
→ 中间

主要 Composite
→ 通常更轻
```

`transform`、`opacity` 在合适情况下往往可以避免 Layout，甚至主要由合成阶段处理，因此常用于高频动画。

不要绝对化：真实流水线由浏览器图层、属性、硬件与优化策略决定。

---

## 8. 普通 `<script>` 为什么可能阻塞 HTML Parser

普通脚本：

```html
<script src="app.js"></script>
```

浏览器解析 HTML 遇到经典普通脚本时，通常需要暂停后续 HTML 解析，先下载 / 执行脚本。

根本原因不是“JavaScript 会 Paint”，而是 JavaScript 可以改变当前 DOM / 文档解析结果，例如：

```js
document.write(...)
element.remove()
element.textContent = ...
```

因此经典流程可粗略理解为：

```text
HTML Parser
↓
遇到普通 script
↓
暂停 HTML Parsing
↓
下载并执行 JS
↓
JS 可能修改 DOM
↓
执行结束
↓
继续解析 HTML
```

---

## 9. `async` 与 `defer`

二者共同点：外部脚本下载都可以与 HTML 解析并行，不需要 Parser 原地等待下载结束。

### `async`

```html
<script src="A.js" async></script>
<script src="B.js" async></script>
```

谁先下载完，谁就可能先尽快执行；多个 `async` 脚本不保证 HTML 声明顺序。

例如 B 下载更快，则 B 可能先执行。

适合相互独立的脚本，如某些统计 / 独立第三方脚本。

### `defer`

```html
<script src="A.js" defer></script>
<script src="B.js" defer></script>
```

下载可并行，但经典 `defer` 脚本会等待文档解析，并保持文档中的执行顺序。

即使 B 100ms 下载完、A 1000ms 才下载完，而 HTML 300ms 已解析完成，B 仍需等 A，然后按 A → B 执行。

粗略记忆：

```text
async
→ 下载不阻塞，谁先好谁可能先上

defer
→ 下载先并行做，执行推迟并保持声明顺序
```

---

## 10. `DOMContentLoaded` 与 `load`

`DOMContentLoaded`：DOM 已经完成解析 / 准备好；不要求图片、视频等所有资源都下载完。

`load`：页面依赖资源完成加载流程之后才触发得更晚。

例如 HTML 已解析完，但 50MB 图片仍在下载：

```text
DOMContentLoaded
→ 可以已经触发

load
→ 暂时不会触发
```

`defer` 脚本会在 `DOMContentLoaded` 之前执行完成，因此 `DOMContentLoaded` 会等待 defer 脚本。

---

## 11. CSS 与 HTML Parsing / Rendering

外部 CSS 通常不会像经典普通 JavaScript 那样直接阻塞 HTML Parser，因此 DOM 可以继续构建；但关键样式表会影响首次正确渲染。

```text
HTML Parser
→ 可以继续构建 DOM

CSS
→ 下载 / 解析为 CSSOM
→ 影响样式计算和首次渲染
```

如果浏览器在关键 CSS 尚未准备时就按默认样式绘制，之后再切换成最终样式，可能产生无样式内容闪烁（FOUC，Flash of Unstyled Content）。

因此面试表达应避免简单说“CSS 完全不阻塞”。更准确：

> CSS 通常不直接阻塞 DOM 构建，但会阻塞 / 影响关键渲染；并且当前面脚本需要依赖最终样式时，还可能形成间接等待。

例如：

```html
<link rel="stylesheet" href="style.css">
<script src="app.js"></script>
```

如果脚本要读取：

```js
getComputedStyle(element)
```

那么脚本可能需要等待前面的样式表；而 HTML Parser 又在等待这个普通脚本执行完，因此形成：

```text
HTML Parser → 等 JS
JS → 等 CSS
```

CSS 由此间接拖住后续 HTML Parsing。

---

## 12. Forced Synchronous Layout 与 Layout Thrashing

浏览器通常有机会批量处理样式 / 布局修改，而不是每写一行 JS 就立刻渲染一次。

例如：

```js
box.style.width = "100px";
box.style.width = "200px";
box.style.width = "300px";
```

浏览器可能把中间修改合并处理。

但是：

```js
box.style.width = "500px";
const width = box.offsetWidth;
```

第二行要求立刻得到元素的真实布局宽度。浏览器不能返回旧值或随便猜，因此可能必须先把前面的布局变化计算完成，再同步返回准确结果。

这称为 **Forced Synchronous Layout（强制同步布局）**。

如果频繁交替：

```text
写布局属性
↓
读几何属性
↓
被迫 Layout
↓
再写
↓
再读
↓
再 Layout
```

就可能产生 **Layout Thrashing（布局抖动 / 反复折腾布局）**。

当前学习状态：现象已经理解，但 `offsetWidth`、Forced Synchronous Layout、Layout Thrashing 等 API / 术语尚不要求死记；以后在 JavaScript / DOM 基础和性能模块中再次出现并巩固。

---

## 13. 与 JavaScript / DOM 基础的衔接

由于尚未系统学习 JavaScript，浏览器性能例子中出现的 DOM API 会产生额外记忆负担。例如：

```js
const box = document.querySelector(".box");
const width = box.offsetWidth;
```

当前策略调整为：先理解浏览器现象，再补最低必要的 JavaScript + DOM 语言基础；API 名称第一次出现只要求知道用途，不强求立即背诵。

下一学习点见：[[02-Current/current-focus]]。

## 第一轮完成标准

当前已能在提示较少的情况下推理：

```text
HTTP 返回 HTML
→ DOM / CSSOM
→ Layout
→ Paint
→ Composite
→ Screen
```

并能解释：

- HTML 与 DOM 的区别；
- `display:none` / `visibility:hidden` / `opacity:0`；
- 为什么动画常用 `transform` / `opacity`；
- 普通 script 为什么阻塞 HTML Parser；
- `async` / `defer` 的核心差异；
- `DOMContentLoaded` / `load`；
- CSS 对 Parsing 与 Rendering 的不同影响；
- 修改布局后立即读取尺寸为什么可能强制同步 Layout；
- 频繁读写为什么可能造成 Layout Thrashing。

后续需要做间隔复习，尤其是专有术语与具体 DOM API 名称。