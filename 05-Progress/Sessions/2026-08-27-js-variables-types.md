---
tags:
  - progress
  - session
  - javascript
  - bytedance
status: completed
updated: 2026-08-27
---

# 2026-08-27 JavaScript：变量、值与基本类型

## 今日完成内容

围绕 JavaScript 变量、值与基本类型完成一轮学习与口头回忆。

已覆盖：

- `let` 与 `const`；
- 变量 / binding 与值的关系；
- 重新赋值；
- `const` 对对象的含义：变量不能重新绑定，但对象内部属性可以修改；
- JavaScript 动态类型的核心直觉：值有类型，变量不被固定为某一种类型；
- `number` / `string` / `boolean`；
- `undefined` 与 `null`；
- `typeof`；
- `typeof null === "object"` 的历史兼容陷阱；
- `==` 与 `===`，以及默认优先使用严格相等。

## 已能自己解释

- `let x = 10; x = 20;` 为什么合法；
- `const x = 10; x = 20;` 为什么不合法；
- `const user = { age: 20 }; user.age = 21;` 为什么合法；
- `100` 与 `"100"` 类型不同；
- JavaScript 是动态类型语言不等于“没有类型”；
- `let x;` 时 x 已经声明，但当前值为 `undefined`；
- `null` 通常用于程序主动表达“这里现在为空”；
- `===` 同时要求类型和值匹配，而 `==` 会发生隐式类型转换。

## 本次纠正过的表述

- “重新复制”应为“重新赋值”；
- `user` 并不是指向 `age` 变量，`age` 是对象属性；
- 不应说 `undefined` 表示“变量没有定义”，`let x;` 中 x 已经声明；
- JavaScript 的 `boolean` 不是 `bool`；
- 更准确地说：值有类型，变量可以先后绑定不同类型的值。

## 当前判断

今天这一小主题已完成第一轮理解和口头验证，可标记为 `learning`，后续通过间隔复习再决定是否升级为 `understood`。

## 下一步

今日学习主题到此停止，不继续学习对象 / 函数 / DOM。

接下来完成当天唯一算法任务：LeetCode 49「字母异位词分组」。
