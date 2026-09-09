---
tags:
  - python
  - basics
status: learning
updated: 2026-09-09
---

# Python 基础语法

## 当前范围

2026-09-09 完成第一轮基础练习。已有 C++ 基础，优先通过小题熟悉 Python 写法；尚未经过间隔复习，不标记为完全掌握。

### 变量、输入与类型

```python
name = "一团"
age = 20
height = 1.78
is_student = True

print(f"{name}，明年你就{age + 1}岁了")
n = int(input("请输入整数："))
```

- 变量直接赋值，不需要先声明类型；常见类型有 `int`、`float`、`str`、`bool`。
- `input()` 返回字符串；数值计算前按需使用 `int()` / `float()`。
- `type(x)` 查看运行时类型；`f"...{x}..."` 用于格式化字符串。
- 类型注解、模块导入和异常处理只做过入门介绍，尚未独立练习。

### 条件与循环

```python
if n > 0:
    print("正数")
elif n == 0:
    print("零")
else:
    print("负数")

for i in range(1, 11, 2):
    print(i)  # 1、3、5、7、9

while n > 0:
    print(n)
    n -= 1
```

- `if` / `elif` / `else`、`for`、`while` 后需要冒号，用缩进表示代码块。
- `range(start, stop, step)` 包含起点、不包含终点；`range(1, 101)` 才包含 100。
- Python 没有 `i++` / `i--`，使用 `i += 1` / `i -= 1`。
- `/` 是普通除法，`//` 是整除，`%` 是取余；判断偶数使用 `x % 2 == 0`。
- `while` 要确保循环变量变化，否则可能死循环。
- 用累加变量求和时先初始化，例如 `total = 0`。

### 列表与下标

```python
nums = [3, 8, 2, 7, 10]
print(nums[0])   # 3
print(nums[-1])  # 10
print(nums[-2])  # 7
print(len(nums)) # 5

result = []
for x in nums:
    if x > 5:
        result.append(x * 2)
print(result)  # [16, 14, 20]
```

- `list` 类似动态数组；`append()` 末尾追加，`len()` 获取长度。
- 负数下标从末尾往前数，`-1` 是最后一个，`-2` 是倒数第二个。
- `nums[a:b]` 是切片，包含 `a`、不包含 `b`。
- 需要下标时使用 `for i, x in enumerate(nums):`；不需要下标就直接 `for x in nums:`。
- 找最大/最小值时，非空列表可用第一个元素初始化，不能一律用 0，否则全负数列表会出错。
- 需要返回下标时，除了最佳值还要保存对应下标；不要误把循环结束后的 `i` 当成答案。

### 函数与返回值

```python
def count_even(nums):
    ans = 0
    for x in nums:
        if x % 2 == 0:
            ans += 1
    return ans

print(count_even([3, 8, 2, 7, 10]))  # 3
```

- `def` 定义函数，参数在括号内，`return` 把结果交给调用者。
- `print()` 只是输出，不等于返回值。
- 删除未使用的变量；避免用 `sum`、`min`、`max` 作为变量名覆盖内置函数。

### 字典 dict

```python
count = {}
for x in [4, 4, 2, 4, 2, 1]:
    if x in count:
        count[x] += 1
    else:
        count[x] = 1
print(count)  # {4: 3, 2: 2, 1: 1}
```

- 字典保存“键 → 值”，类似 C++ 的 `unordered_map`。
- `count[x]` 通过键访问值，不是列表下标；字典没有相应键时直接读取会报 `KeyError`。
- `x in count` 判断键是否存在；第一次遇到设为 1，以后加 1。
- `for key, value in count.items():` 同时遍历键和值。
- 找出现次数最多的数字时，同时保存最大次数与对应数字；不能只返回次数。

### 集合 set

```python
seen = set()
seen.add(3)
seen.add(5)
seen.add(3)
print(3 in seen)  # True
```

- 集合只保存元素，常用于去重和存在性判断；空集合写 `set()`，`{}` 是空字典。
- 当前只看过示例，尚未完成独立去重题。

## 下一次复习

2026-09-10 先无提示回忆，再针对错误讲解。建议依次检查：

1. 输入 n，用 `while` 求 1 到 n 的和，检查 `int()`、边界与变量更新。
2. 从含负数的非空列表中找最大值及下标，检查初始化、`enumerate()` 与返回值。
3. 用字典统计数字次数，再找出现次数最多的数字及次数。
4. 用 `set()`、`add()` 完成 `[1, 2, 2, 3, 3, 3]` 去重。

后续再进入字符串、切片练习、文件操作与模块。不要把只看过的内容提前记为掌握。
