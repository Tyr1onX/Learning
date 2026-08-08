---
tags:
  - web
  - browser
  - rendering
status: learning
updated: 2026-08-08
---

# Browser Rendering Pipeline

> 当前正在学习。本文件先记录主干和待验证问题，完成一轮讲解与回忆后再升级状态。

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

JavaScript 操作 DOM，并不是直接改服务器上的 HTML 文件。

待确认：能否用自己的话解释“HTML ≠ DOM”。

---

## 2. CSSOM

CSS 也是文本，浏览器解析后需要形成可用于样式计算的数据结构，基础学习中通常称 CSSOM（CSS Object Model）。

可以先理解：

```text
DOM   → 页面有哪些节点 / 结构
CSSOM → 样式规则
```

浏览器结合节点和样式信息继续构建渲染所需结构。

---

## 3. Render Tree / Rendering Structure

不是 DOM 中所有节点都一定以可见盒子的形式进入正常渲染。

例如：

```css
.hidden {
  display: none;
}
```

节点仍可以存在 DOM 中，但不参与正常 Layout，也不会被正常绘制。

对比：

```text
display: none
→ 不显示
→ 不参与正常布局
→ 不占空间

visibility: hidden
→ 不显示
→ 通常仍参与布局
→ 仍占空间
```

待确认：能否解释“DOM 中存在 ≠ 一定被渲染”。

---

## 4. Layout / Reflow

Layout 负责计算几何信息：

```text
width / height
x / y
子元素位置
文字换行
```

修改可能影响几何关系的属性，例如 `width`，可能导致重新 Layout，并连带影响父子 / 兄弟元素。

传统前端语境常把重新布局称为 Reflow / 重排。

---

## 5. Paint / Repaint

Paint 负责把已经确定位置和尺寸的元素绘制出来，例如：

```text
背景
边框
文字
阴影
图片
颜色
```

只改变背景颜色时，几何信息通常不需要重新 Layout，但需要重新绘制相关内容。

---

## 6. Composite

现代浏览器会把部分内容分到不同 Layer 中，最后由合成阶段组合成最终画面。

`transform`、`opacity` 在合适情况下往往可以主要由合成阶段处理，因此更适合作为高频动画属性。

对比直觉：

```text
修改 width / left
→ 可能触发布局计算
→ Paint
→ Composite

修改 transform / opacity
→ 很多情况下可避免 Layout
→ 甚至主要由 Composite 完成
```

不要绝对化：真实浏览器会根据图层、属性和优化策略决定具体流水线。

---

## 当前待回答

1. HTML 和 DOM 是同一个东西吗？为什么？
2. `display: none` 后节点还在 DOM 中吗？会参与 Layout 吗？
3. 为什么移动动画通常更推荐 `transform: translateX()` 而不是持续修改 `left` / `width`？
4. JavaScript 修改 DOM / Style 后，哪些操作会触发 Style / Layout / Paint / Composite？
5. `<script>` 为什么可能阻塞 HTML Parsing？
6. `defer` 与 `async` 的加载和执行顺序有什么区别？

## 完成标准

能够从：

```text
HTTP 返回 HTML
```

连续解释到：

```text
DOM / CSSOM → Layout → Paint → Composite → Screen
```

并能用性能角度解释一次 DOM / Style 修改可能引发的后续成本。
