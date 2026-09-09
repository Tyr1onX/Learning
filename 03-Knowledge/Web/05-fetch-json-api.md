---
tags:
  - knowledge
  - web
  - javascript
  - fetch
  - api
status: learning
updated: 2026-09-09
---

# fetch / JSON / API

## 核心直觉

前端页面通常不是直接拿数据库。常见链路是：

```text
浏览器 JavaScript
↓ fetch 发 HTTP 请求
后端 API
↓ 路由匹配与处理函数
查询 / 处理数据
↓
返回 JSON
↓
前端解析 JSON 并更新页面
```

例如：

```js
fetch("/api/flights")
```

直觉含义：浏览器里的 JavaScript 向后端 `/api/flights` 这个地址发送 HTTP 请求，希望拿到 flights 相关数据。

## API 与页面地址

API 与普通页面地址的核心区别不是有没有查询参数，也不是普通页面地址是否连接后端。

更准确的区分是用途：

```text
页面地址：通常给人看页面，例如 /home、/profile
API 地址：通常给程序请求数据或提交数据，例如 /api/flights
```

`/api/flights` 不一定带查询参数，也仍然可以是 API。

## JSON

JSON 是一种轻量数据交换格式，能表示：

```text
字符串、数字、布尔值、null、对象、数组
```

例子：

```json
{
  "code": 0,
  "message": "ok",
  "data": {
    "flights": [
      { "from": "CKG", "to": "NKG" }
    ]
  }
}
```

结构识别：

```text
最外层：对象
data：对象
flights：数组
flights 数组里的每一项：对象
```

前后端常用 JSON，是因为它文本化、通用，浏览器和后端语言都容易解析和生成。

## fetch 两步

常见写法：

```js
const res = await fetch("/api/flights");
const data = await res.json();
```

两步含义：

```text
fetch 先拿到 HTTP Response 对象 res
res.json() 再把响应体里的 JSON 文本解析成 JavaScript 对象 data
```

`res` 不是业务数据对象。它通常包含：

```text
status
headers
body
```

真正的业务数据在响应体中，需要 `res.json()` 解析后才能通过 `data.flights` 这类方式访问。

错误直觉：

```js
const data = await fetch("/api/flights");
console.log(data.flights);
```

问题：这里的 `data` 实际是 `Response`，不是解析后的业务对象，因此通常拿不到 `data.flights`。

## 状态码与 res.ok

```js
const res = await fetch("/api/flights");

if (!res.ok) {
  throw new Error("请求失败");
}

const data = await res.json();
```

`res.ok` 判断 HTTP 状态码是否在 200～299 范围内。请求 API 时不能只管 `res.json()`，因为后端可能返回：

```text
404：接口不存在
401：没登录
403：没权限
500：服务器内部错误
```

即使失败响应也可能有 JSON 响应体，但不代表业务成功。

面试表达：

```text
fetch 拿到的是 HTTP 响应对象，先通过状态码判断请求是否成功；成功后再解析 JSON，避免把错误响应当成正常业务数据处理。
```

## API 背后的后端流程

前端：

```js
fetch("/api/flights")
```

后端大致流程：

```text
收到请求
→ 根据路径和方法匹配路由，例如 GET /api/flights
→ 执行对应处理函数
→ 可能查询数据库 / 读取文件 / 调用其他服务
→ 把结果组装成 JSON
→ 返回给前端
```

路由匹配决定了这次请求应该交给哪个处理函数。处理函数再决定查什么数据、怎么处理、最后返回什么 JSON。

## 当前掌握状态

2026-09-09 第一轮学习完成，状态保持 `learning`。

已通过：

- 能说出 `fetch("/api/flights")` 是浏览器 JS 向后端 API 请求 flights 数据；
- 能经纠正后区分 API 地址和页面地址；
- 能说明 JSON 通用、方便前后端解析和生成；
- 能说明后端需要根据路径和方法匹配路由，再执行处理函数返回 JSON。

待复习：

- JSON 结构识别：对象 / 数组 / 字段；
- `res` 与 `data` 的区别；
- `res.ok` 与 HTTP 状态码；
- API 路由匹配的准确表达。