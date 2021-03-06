提示: 如果需要使用目录请到[这里](https://github.com/sam01101/HowToLua/blob/main/basic/intro.md)观看文档
<details><summary>目录</summary>
<p>

- [脚本式编程](#脚本式编程)
    - [Hello World](#Hello-World)
- [注释](#注释)
    - [单行注释](#单行注释)
    - [多行注释](#多行注释)
- [字符串的引号](#字符串的双引号)
- [多行引号/注释的冲突](#多行引号/多行注释-的冲突)
- [变量起名](#变量起名)
- [保留字](#关键词/保留字)

</p>
</details>

# Lua 基本语法
> Lua 学习起来非常简单(也可以很地狱)，我们可以创建第一个 Lua 程序！

这里我不会写[交互式编程](https://www.runoob.com/lua/lua-basic-syntax.html),
有兴趣的可以自己去看, 因为没什么好补充的

## 脚本式编程

Lua 的 文件结尾都是`.lua`

首先, 我们来写个每个程序都会写的 "Hello World"

#### Hello World

```lua
print("Hello World!")
```

| 类型 | 说明 |
| ---  | ---- |
| `print` | **打印函数** |
| `"Hello World!"` | **字符串** |

`print` 的英文为"打印", 字面意思, 是 **底层函数(Base Function)** 的其中一个

`Hello World!`被一层引号`""`包住, 引号里面的内容我们称之为**字符串**

## 注释

注释是大部分程序的标配, 可以帮助其他人理解代码的意思

但请注意, 错误地注释比没有注释更糟, 因为它会误导后来者。

在Lua中, 我们使用`--`来进行注释 (举例, 如果是Java程序就是`//`)

| 类型 | 说明 |
| ---  | ---- |
| `--`| **单行注释** |
| `--[[]]` | **多行注释** | 
| `--[=[]=]` | **"进阶版"多行注释** | 

#### 单行注释

```lua
-- 这就是单行注释
```

#### 多行注释

普通的多行注释:

```lua
--[[
多行注释就是
两个`[`号
]]
```

"进阶版"多行注释:

```lua
--[=[
你可以添加任意"="号来延申
]=]
```

## 字符串的双引号

字符串除了`""`之外, 其实还有其它的

| 类型 | 说明 |
| ---  | ---- |
| `''` | **单引号** |
| `""` | **双引号** |
| `[[]]` | **多行引号(暂称)** |
| `[=[]=]` | **"进阶版"多行引号** |

`''` 也可以, 但我们**强烈建议**用双引号表示字符串

```lua
print('hello world!')
```

包括 `[[]]` 也是

```lua
local _ = [[
字符串可以这样包住哦, 而且连换行符(\n)和Tab(\t)也一并包括哦
]]
```

```lua
local _ = [=[
当然你也可以这样, 如同"进阶版"多行注释一样
]=]
```

## 多行引号/多行注释 的冲突

我们都知道`[[]]`这个符号可以多行, 但如果我想在里面也加这个符号怎么办?

```lua
local _ = [=[
这样就可以添加[[多行
符号]]了, `=`号可以无限添加以便应付后续情况
]=]

local _ = [==[
a [=[b]=] [[c]]
]==]
```

## 变量起名

变量起名规则:

| 类型 | 说明 |
| ---  | ---- |
| _开头_ | **必须**`英文字符A-Z a-z 或者 下划线(_)` |
| 建议 | 开头**不要使用下划线加大写字母** |
| 不允许 | 使用特殊字符`@`, `$`, `%` | 

以下为正确变量名称的(官方)例子:

```
mohd         zara      abc     move_name    a_123

myname50     _temp     j       a23b9        retVal
```

## 关键词/保留字

以下为Lua的关键词/保留字, 不能作为变量使用

> 一般约定, 以"_"开头, 连接一串大写字母的名字 (比如 _VERSION) 被保留用于 Lua 内部全局变量.

| 关键词 | 说明 |
| ---  | ---- |
| 逻辑判断: | ---- |
| `if` | 如果 |
| `then` | 则 |
| `else` | 否则 |
| `elseif` | 否则如果 |
| 关联字符: | ---- |
| `and` | 和 |
| `or` | 或 |
| 循环: | ---- |
| `for` | 从某个数到某个数 |
| `in` | 用于`for call`(稍后解释) |
| `while` | while循环 |
| `repeat` | 重复 |
| `until` | 直到条件达成 |
| `goto` | 跳到某个位置 |
| `break` | 强制中断循环 |
| 变量定义: | ---- |
| `local` | 局部变量定义 |
| 数据类型: | ---- |
| `not` | 非 |
| `true` | 是 |
| `false` | 否 |
| `nil` | 空(Null) |
| 区块类: | ---- |
| `do` | do区块识别符 |
| `function` | 函数定义 |
| `return` | 返回 |
| `end` | 结束 |