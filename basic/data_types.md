<details><summary>目录</summary>
<p>

- [简介](#Lua-数据类型)
- [nil](#nil)
    - [代码示范](#nil代码示范)
    - [type函数](#type函数讲解)
- [boolean](#字符串的双引号)
    - [代码示范](#boolean代码示范)
- [number](#number)
    - [代码示范](#number代码示范)
    - [判断是否为整数](#判断是否为整数)
- [string](#string)
    - [注意事项](#string注意事项)
    - [计算长度](#计算string长度)
- [table](#table)
    - [创建](#创建table)
    - [索引](#table索引)
        - [需要注意的地方](#table索引需要注意的地方)
    - [初始化数据的多赋值](#table初始化数据的多赋值)
    - [没赋值的情况](#table没赋值的情况)
    - [特性](#table的特性)
- [function](#function)
    - [匿名函数](#匿名函数-(Anonymous-function))
    - [特性](#function的特性)
- [thread](#thread)
- [userdata](#userdata)

</p>
</details>

# Lua 数据类型

Lua 是动态类型语言, 变量不需要强制规定其类型, 只需要赋值即可.

值(也就是数据)可以存储在变量里, 作为参数传递或作为结果返回.

Lua 中有 8 个基本类型: 

> 常用: `nil` `boolean` `number` `string` `table` `function`
>
> 不常用/不常见: `thread` `userdata` 
>
> `lightuserdata` (和`userdata`一样, 不介绍, 知道就好)

| 数据类型 | 	描述 |
| ------ | ---- |
| `nil` | `nil` 就是 `nil`, 相当于Java的Null, |
| ------ | **表示一个无效值/空值**, 可用于重置变量 |
| `boolean` | 布尔值, `true`和`false` |
| `number` | 数字, 包括整数和非整数 |
| `string` | 字符串, 先前的简介有介绍 |
| `function` | Lua 或者 C 的函数 |
| `userdata` | 表示任意存储在变量中的 C 数据结构 |
| `lightuserdata` | 同上, 不过是 `void*` 类型 |
| `thread` | 线程, 用于执行协同(异步)程序 |
| `table` | `array`, `list`, `dict` 集合一身的表(table) |

> 好复杂? 可以跳过不看这个表, 看下面的比较详细

# nil

nil (类型)表示一种没有任何数据的值, 

你可以尝试随便打印一个变量出来, 只要这个变量没被定义数值它就是nil

用途: 重置数值, 清理数据, 检查是否为空值

> 对于全局变量和 `table`, `nil` 还有一个"删除"作用, 给全局变量或者 `table` 表里的变量赋一个 `nil` 值, 等同于把它们删掉

#### nil代码示范

```lua
table1 = { key1 = "value1", key2 = "value2", "value3" } -- 创建table, 并预设数值在table里

for key, value in pairs(table1) do
    print(key .. " - " .. value)
    -- 输出结果:
    --[[
        1 - value3 -- value3 我们稍后在table章节的时候一并说明
        key1 - value1
        key2 - value2
    --]]
end

tab1.key1 = nil
-- 此时的table会变成:
--[[ 注意 key1 和 value1 "消失" 了
table1 = { key2 = "value2", "value3" }
--]]

for key, value in pairs(table1) do
    print(key .. " - " .. value)
    -- 输出结果:
    --[[
        1 - value3
        key2 - value2
    --]]
end
```

#### type函数讲解

```lua
x = nil -- x 是 nil
print(type(x))
-- 输出: nil
print(type(y))
-- 输出: nil (因为本来就没定义)
print(type(x) == nil) -- 判断 x 是否为 nil
-- 输出: false
```
这里就很奇妙了, 为什么是`false`?

我们来看下`type`函数的简介
>基本函数 `type`
>
>返回该变量的**类型**, 并以**string**返回其类型名称

那么, 我们就得知原来`type`是返回**字符**类型的名称, 而不是该类型

```lua
-- 我们给它加上双引号就可以了
print(type(x) == "nil")
-- 输出: true
```

## boolean

`boolean` 只有两个值: `true` 和 `false`.

Lua 把 `false` 和 `nil` 当成 `false`, 其他都是 `true`, 包括数字 `0`, 也是`true`

#### boolean代码示范

```lua
print(type(true))
-- 输出: boolean
print(type(false))
-- 输出: boolean
print(type(nil))
-- 输出: nil

if false or nil then
    print("至少有一个是 true")
else
    print("false 和 nil 都为 false")
end
-- 执行结果为: false 和 nil 都为 false

if 0 then
    print("数字 0 是 true")
else
    print("数字 0 为 false")
end
-- 执行结果为: 数字 0 是 true
```

## number

Lua 的`number`(数字)默认只有一种 -- `number`, 实际上都是`double`

#### number代码示范

```lua
print(type(2))
print(type(2.2))
print(type(0.2))
print(type(2e+1))
print(type(0.2e-1))
print(type(7.8263692594256e-06))

-- 全部输出都是 number
```

#### 判断是否为整数

如果要判断是否为整数, 我们可以用 `x % 1 == 0` 来判断

```lua
print(1.0 % 1 == 0)
print(1 % 1 == 0)
-- 输出都是 true
print(1.1 % 1 == 0)
print(1.0000001 % 1 == 0)
-- 输出都是 false
```

## string

string, 也就是`字符串`,

有趣的地方就是你可以混合字符串和数字来进行计算, 

但这样会导致每次执行的时候都要计算一次

> 注: 字符串必须只能是数字

```lua
print("2" + 6)
print("2" + "6")
-- 输出: 8.0
print("2 + 6")
-- 输出: 2 + 6
print("-2e2" * "6")
-- 输出: -1200.0
print("A" + 1)
--[[
    错误: attempt to perform arithmetic on a string value
    中文翻译: 尝试与字符串值进行算术运算
--]]
```

#### string注意事项

如果使用连接符号`..`并不会进行计算

```lua
print("a" .. 'b')
-- 输出: ab
print(157 .. 428)
print("157" .. 428)
-- 输出: 157428
```

#### 计算string长度

我们可以透过`#`符号来判断`string`的长度, 放在字符串前面

```lua
-- 先赋值后计算
len = "lua.docs.samtool.asia"
-- 直接计算
print(#"lua.docs.samtool.asia")
print(#len)

-- 输出都是 21
```

## table

> 万物皆可table

在 Lua 中, `table`是最有用的一个类型. 这里直接放代码示范

#### 创建table

```lua
-- 创建一个空的 table
table1 = {}

-- 创建一个初始包含数据的 table
table2 = {"Java", "Lua", "Python", "和什么"}
```

如果你有学过`Python`, 那么你应该知道`dict`这个类型,

如果没有不用担心, 其实`table`就像一个数据库一样, 分成`index`和`value`

`index`是索引, 就是用来识别数值(`value`)的

#### table索引

> 不同于其他语言的数组, 把`0`作为数组的初始索引. 在 Lua 里, 表的默认初始索引一般以`1`开始.

`table`不会固定长度大小, 有新数据添加时`table`长度会自动增长

注: 索引**不能是nil**

```lua
-- 创建一个空table
table1 = {}

table1[1] = true -- 设置table的索引1为true

table1["a"] = "你好" -- 设置table的索引"a"为"你好"

index = 5

table1[index] = 233 -- 设置table的索引 5 为 233

-- 进行计算
table1[index] = table1[index] + 11 -- 把 233 + 11 的计算结果保存到index(也就是5)里

for k, v in pairs(table1) do
    print(k .. " : " .. tostring(v))
    -- tostring 代表把该数值强制转成string类型
end
--[[ 输出结果
    1 : true
    a : 你好
    5 : 244
]]
```

#### table索引需要注意的地方

请注意数字并**不能直接赋值**, 如果必须赋值必须加上"[ ]"

```lua
table1 = {
    100 = "a" -- 报错: '}' expected near '='
}
```

```lua
table1 = {
    [100] = "a" -- 没问题!
}
```

#### table初始化数据的多赋值

你可以选择使用","或者";"来进行初始赋值

```lua
table1 = {
    1,
    2;
    3,
    4;
}
```

#### table没赋值的情况

没赋值的`table`的数值都是`nil`

```lua
table1 = {}
-- 往table填充1到10的数值
for int = 1, 10 do
    table1[int] = int
end

table1["key"] = "val"
print(table1["key"])
-- 输出: val
print(table1["null"])
-- 输出: nil
```

#### table的特性

`table`实际上是一个类似指针(`pointer`)的存在, 如果被`table`赋值到其它值, 它会指向原初的`table`

```lua
table1 = {"A"}
print(table1[1])
-- A

table2 = table1 -- 把table1的指针赋值到table2中

table2[1] = "B" -- 改变原table的数值
print("Table1: " .. table1[1])
-- Table1: B
print("Table2: " .. table2[1])
-- Table2: B
```

## function

在 Lua 中, 函数可以存在变量里

```lua
function a() end -- 一个函数a, 调用只会返回nil(也就是没任何返回值)

function ret1() -- 一个函数, 名称的长写是return 1(返回1), 调用会返回1
    return 1 -- 返回1
end

print(a())
-- 返回 nil
print(ret1())
-- 返回 1

retA = ret1 -- 把函数ret1赋到retA

print(retA())
-- 返回 1
```

#### 匿名函数 (Anonymous function)

临时的函数, 并没有被赋值在任何一个数值上

```lua
(function()
    print("简单的例子")
end)() -- 直接执行

-- 一个string.gsub例子(有关gsub函数的资料请看基本函数列表)
str = "IaIbIc"
after = str:gsub("I.",function(s) -- 这个函数也是匿名函数
    return s
end)
print(after)
-- abc
```

#### function的特性

和[table的特性](#table的特性)一样, 都是以类似指针的方式储存的

_这里只说单纯的赋值, 并没有涉及其它有关`function`的操作而导致的改变赋值_

## thread
在 Lua 里, 最主要的线程是协同程序(`coroutine`). 它跟线程(`thread`)差不多, 拥有自己独立的栈, 局部变量和指令指针,

可以跟其他协同程序共享全局变量和其他大部分东西.

补充: 协同程序其实就是异步执行(`asynchronous`)

| 线程(thread) | 协程(coroutine) |
| --- | --- |
| 可以同时多个运行 | 任意时刻只能运行一个 |
| --- | 只有被挂起(suspend)时才会暂停 |

## userdata
`userdata` 是一种用户自定义数据, 用于表示一种由应用程序或 C/C++ 语言库所创建的类型,

可以将任意 C/C++ 的任意数据类型的数据(通常是 架构(`struct`) 和 指针(`pointer`))存储到 Lua 变量中调用.