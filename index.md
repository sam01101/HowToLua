<details>
<summary>目录</summary>
<p>

- [背景](#背景)
- [特性](#特性)
- [应用场景](#应用)
- [动机](#动机)
- [内容目录](#内容目录)
- [资料引用 / 参考](#参考)

</p>
</details>

## 背景

Lua 是一种轻量小巧的脚本语言，用标准C语言编写并以源代码形式开放， 其设计目的是为了嵌入应用程序中，从而为应用程序提供灵活的扩展和定制功能。

## 特性

- __轻量级__: 它用标准C语言编写并以源代码形式开放，编译后仅仅一百余K，可以很方便地嵌入别的程序里。
- __可扩展__: Lua提供了非常易于使用的扩展接口和机制：由宿主语言(通常是C或C++)提供这些功能，Lua可以使用它们，就像是本来就内置的功能一样。
- __其它特性__:
    - 支持面向过程(procedure-oriented)编程和函数式编程(functional programming)；
    - 自动内存管理；只提供了一种通用类型的表（table），用它可以实现数组，哈希表，集合，对象；
    - 语言内置模式匹配；闭包(closure)；函数也可以看做一个值；提供多线程（协同进程，并非操作系统所支持的线程）支持；
    - 通过闭包和table可以很方便地支持面向对象编程所需要的一些关键机制，比如数据抽象，虚函数，继承和重载等。
    
## 应用

- 游戏开发如: 梦幻西游 <!-- 你觉得网易的我会给你链接吗? -->
- 独立应用脚本
- Web 应用脚本: [lua-nginx-module](https://github.com/openresty/lua-nginx-module)
- 扩展和数据库插件如: [MySQL Proxy](https://downloads.mysql.com/docs/mysql-proxy-en.a4.pdf) 和 [MySQL WorkBench](https://www.mysql.com/cn/products/workbench/index.html)
- 安全系统，如入侵检测系统, [防火墙](https://www.bt.cn/bbs/thread-13647-1-1.html)
- 游戏作弊的脚本引擎如: [GameGuardian](https://gameguardian.net)

## 动机

> Lua 是一种轻量小巧的脚本语言，用标准C语言编写并以源代码形式开放

基于容易学会与轻量的优点, 此语言被用于多种的环境中.

此教程会基于Lua 5.2 版本讲解, 除了基本的语法之外, 还有有关二进制格式及其指令等。

这个项目的名字来源于 HowToBasic 的频道名称

## 内容目录
###### 我们假定你已经安装了Lua 5.2的环境并可以正常运行
- 基础: Lua基础知识
    - 简介
    - 数据类型 (数字, 字符, boolean, nil)
    - 变量 (局部变量local, 全局变量globals)
    - 循环 (for, while, repeat)
    - 逻辑语句 (if, then, elseif, end)
    - 函数 (function)
    - 运算符 (+, -, *, %)
    - 字符串 ("string")
    - 数组
    - 迭代器 (pairs, ipairs, iterator)
    - 表 ({table})
    - 模块与包 (Package)
    - 元表 (Metatable)
    - 协同 (Coroutine)
    - 文件处理 (io)
    - 错误处理 (error)
    - 面向对象 (OOP)
    - 附: 基本函数列表
    - [ ] 附赠的教程
        - 源码加密
        - 解密还原
        - 加解密对抗实战


- [ ] 进阶: 二进制区块
    - 简介
        - 区块格式
        - 指令 (Instructions)
        - 常量 (Constants) 与其类型
        - 外部变量 (Upvalues)
        - 调试信息
        - 函数区块 (Proto)
    - 附赠的教程
        - 如何加密二进制
        - 如何还原被加密的二进制
        - 实战示范


# 参考
> Sam: 我衷心感谢现在大部分的资源都是免费的, 正因如此我才不用额外花费学习. 但请有能力的朋友们买正版书来支持作者

- [Lua 5.2 源码](https://www.lua.org/source/5.2/index.html)
- [Runoob](https://www.runoob.com/lua/lua-tutorial.html) _提供Lua基础知识_
- [CSDN](https://blog.csdn.net)
- [Lua 5.2 Bytecode and Virtual Machine](http://files.catwell.info/misc/mirror/lua-5.2-bytecode-vm-dirk-laurie/lua52vm.html) _及其[翻译](https://bbs.pediy.com/thread-222768.htm)_
- [A No-Frills Introduction to Lua 5.1 VM Instructions](http://luaforge.net/docman/83/98/ANoFrillsIntroToLua51VMInstructions.pdf) _及其翻译(收费)_
- [函数列表(部分过时)](https://www.gammon.com.au/scripts/doc.php?lua)
