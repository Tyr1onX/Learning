---
tags:
  - web
  - cors
  - security
  - auth
status: understood
updated: 2026-08-08
---

# CORS / Cookie / Session / JWT / XSS / CSRF

## 1. Same-Origin Policy 与 CORS

Origin 由三部分决定：

```text
scheme + host + port
```

路径不同不影响 Origin；协议、主机名、端口任何一个不同，就属于不同 Origin。

示例：

```text
https://www.example.com
https://api.example.com
```

主机名不同，因此跨 Origin。

### Same-Origin Policy

浏览器默认限制一个 Origin 下的 JavaScript 随意读取另一个 Origin 的响应数据。

### CORS

CORS = Cross-Origin Resource Sharing。

服务器可以通过响应头声明允许哪些 Origin 的前端 JS 读取响应，例如：

```http
Access-Control-Allow-Origin: https://frontend.com
```

因此：

```text
HTTP 200
≠
前端 JS 一定能读取响应
```

服务器可能已经成功处理请求并返回 200，但如果 CORS 响应头缺失或不匹配，浏览器仍可能拒绝把响应暴露给调用方 JS。

> CORS 是浏览器安全机制的一部分，不是 Authentication，也不是防火墙。

---

## 2. Preflight / OPTIONS

对于不满足 CORS safelist 条件的跨源请求，浏览器通常先发 OPTIONS 预检。

例如：

```http
PUT /users/123
Content-Type: application/json
Authorization: Bearer xxx
```

这里 PUT、`application/json`、`Authorization` 都可能使请求需要预检。

基础阶段记住：

```text
常见 safelisted method：GET / HEAD / POST
常见 safelisted Content-Type：
  text/plain
  multipart/form-data
  application/x-www-form-urlencoded
```

预检大致是：

```text
浏览器
↓ OPTIONS
服务器：允许这个 Origin / Method / Header 吗？
↓ 允许
浏览器发送真正请求
```

真正响应仍要满足 CORS 条件。

---

## 3. Credentialed CORS

跨 Origin `fetch` 如果要携带 Cookie，前端常需要：

```js
fetch(url, {
  credentials: "include"
})
```

服务器还需要类似：

```http
Access-Control-Allow-Origin: https://frontend.com
Access-Control-Allow-Credentials: true
```

带 Credentials 时不能简单使用：

```http
Access-Control-Allow-Origin: *
```

同时 Cookie 自身的 SameSite / Secure 等规则也必须允许发送。

---

## 4. Same-Origin ≠ Same-Site

```text
CORS / Same-Origin
→ 看 Origin：scheme + host + port

SameSite Cookie
→ 看 Site 概念
```

`www.example.com` 与 `api.example.com` 是不同 Origin，但在常见情况下仍可能属于 Same-Site。

---

## 5. Cookie 与 Session

HTTP 本身是无状态协议，因此 Web 应用需要额外机制维持登录等状态。

### Cookie

服务器可以：

```http
Set-Cookie: session_id=abc123
```

浏览器保存后，满足条件的后续请求会自动携带：

```http
Cookie: session_id=abc123
```

Cookie 更准确地说是 HTTP 中保存 / 携带状态信息的一套机制，不是“服务器缓存”。

### Session

常见 Session 模型：

```text
Browser Cookie
session_id = abc123

Server Session Store
abc123 → user_id=9527, role=student
```

浏览器只需要持有 session_id，具体登录状态可以保存在服务端。

---

## 6. Cookie 安全属性

```text
HttpOnly
→ JavaScript 不能通过 document.cookie 直接读取
→ 降低 XSS 直接偷 Cookie 的风险

Secure
→ Cookie 只通过 HTTPS 发送

SameSite
→ 控制跨站请求时 Cookie 是否发送
→ 有助于降低 CSRF 风险
```

SameSite 常见模式：Strict / Lax / None。None 通常需要配合 Secure。

---

## 7. JWT

常见 JWT 结构：

```text
Header.Payload.Signature
```

最重要的纠正：

> 常见签名 JWT 不是“加密 Token”。Payload 通常可以被解码看到。

例如：

```json
{
  "user_id": 9527,
  "role": "student"
}
```

攻击者可以看到 Payload，但如果直接改成：

```json
{
  "role": "admin"
}
```

原 Signature 与新内容不匹配，服务器验签失败。

所以：

```text
JWT 防篡改 ✓
JWT 默认隐藏 Payload ✗
JWT 防止合法 Token 被盗 ✗
```

如果攻击者直接偷走完整有效 JWT，不做修改，服务器可能仍把持有者当成原用户，因为常见 Access Token 是 Bearer Token。

### Access Token / Refresh Token

```text
Access Token
→ 生命周期较短
→ 调用业务 API

Refresh Token
→ 生命周期更长、更敏感
→ 用于换取新的 Access Token
```

短 Access Token 可以缩短被盗后的有效攻击窗口。

---

## 8. Authentication / Authorization

```text
Authentication
→ 你是谁？
→ 身份认证

Authorization
→ 你能做什么？
→ 权限授权
```

常见状态码理解：

```text
401 → 没有有效身份凭证 / Authentication 未通过
403 → 已识别身份，但没有操作权限 / Authorization 不允许
```

---

## 9. XSS

XSS = Cross-Site Scripting。

核心：攻击者让恶意 JavaScript 在可信网站的上下文里执行。

常见类型：Stored XSS、Reflected XSS、DOM-based XSS。

DOM XSS 典型危险做法：

```js
output.innerHTML = userControlledInput;
```

如果只是展示文本，更安全的思路是：

```js
output.textContent = userControlledInput;
```

原则：用户输入从 URL、表单等进来以后，即使存进 `const`，也仍然是不可信数据。安全处理取决于它最终进入什么上下文 / sink。

HttpOnly 能降低 JS 直接读取 Cookie 的风险，但 XSS 仍可能在当前网站上下文发起请求，浏览器会自动携带合法 Cookie，因此 HttpOnly 并不能“解决 XSS”。

---

## 10. CSRF

CSRF = Cross-Site Request Forgery。

核心：攻击者借用用户已经登录的身份，让浏览器替攻击者执行请求。

```text
用户已登录 bank.com
↓
打开 evil.com
↓
evil.com 诱导浏览器向 bank.com 发操作请求
↓
浏览器可能自动携带 Cookie
↓
服务器误以为是用户本人操作
```

关键点：

> CSRF 不一定需要读取响应，只要请求真的执行成功就够了。

因此 CORS 不是主要 CSRF 防线。

常见防护：SameSite、CSRF Token、Origin / Referer 检查、敏感操作重新认证。

---

## 面试速记

```text
XSS：坏人的代码跑进了我的网站。
CSRF：坏人借我的登录身份去办事。

CORS：控制跨 Origin JS 是否能读取响应。
SameSite：控制跨 Site 时 Cookie 是否发送。

200 OK：HTTP 层成功。
CORS pass：浏览器愿意把跨源响应交给 JS。
```
