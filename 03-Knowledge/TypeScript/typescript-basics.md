---
tags:
  - knowledge
  - typescript
status: learning
updated: 2026-09-17
---

# TypeScript 基础

## 核心直觉

TypeScript 在 JavaScript 上增加静态类型检查，让很多类型错误在运行前暴露。

```ts
let age: number = 20;
age = "twenty"; // 类型错误
```

## 类型推断

当初始值已经明确时，通常无需重复类型：

```ts
let age = 20;      // 推断 number
let name = "Tom"; // 推断 string
```

## 函数参数与返回值

```ts
function add(a: number, b: number) {
  return a + b;
}
```

参数类型显式约束；返回值可由表达式推断为 `number`。

## 对象类型

```ts
type User = {
  name: string;
  age?: number;
};
```

- `name` 默认必填；
- `age?: number` 表示字段可不存在；
- 字段存在时必须是 `number`；
- 在常见严格配置下读取可选字段时需考虑 `undefined`。

## 类型别名

```ts
type User = {
  name: string;
  age?: number;
};
```

`type` 可以为一套类型规则命名，避免重复书写复杂对象结构。

## 联合类型

```ts
let id: number | string;
```

表示 `id` 可以是 `number` 或 `string`，不能随意赋其他类型。

## Narrowing

```ts
function printId(id: number | string) {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  } else {
    console.log(id + 1);
  }
}
```

通过 `typeof` 等运行时判断，TypeScript 能在当前分支把联合类型缩小成更具体的类型。

## 数组类型

```ts
const scores: number[] = [90, 80, 100];
const users: User[] = [{ name: "Tom" }];
```

- `number[]`：数字数组，取单个元素通常得到 `number`；
- `User[]`：User 数组，取单个元素通常得到 `User`。

## 当前易错点

- 可选字段不是“永远有值”；读取时需要考虑 `undefined`；
- 对象类型中的非可选字段缺失会报错；
- `User[]` 是 User 数组，不是单个 User；
- 能推断出来的局部变量不必机械重复类型注解。

## 状态

2026-09-17 完成第一轮，状态保持 `learning`。

复习：D+1 2026-09-18；D+3 2026-09-20；D+7 2026-09-24；D+21 2026-10-08。
