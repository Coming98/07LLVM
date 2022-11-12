# Overview

The LLVM code representation is designed to be used in three different forms:
1. in-memory compiler IR
2. on-disk bitcode representation (suitable for fast loading by a Just-In-Time compiler)
3. human readable assembly language representation

传统编译器的工作原理: 前端, 优化器, 后端
- 前端: 解析源代码，检查语法错误，并将其翻译为抽象的语法树
- 优化器: 对中间代码进行优化，试图使代码更高效
- 后端: 负责将优化器优化后的中间代码转换为目标机器的代码 (旨在最大化的利用目标机器的特殊指令，以提高代码的性能）

广义 LLVM: 一个完整的 LLVM 编译器框架系统，包括了前端、优化器、后端、众多的库函数以及很多的模块
狭义 LLVM：聚焦于编译器后端功能的一系列模块和库，包括代码优化、代码生成、JIT 等
SSA: 静态单赋值形式, static single assignment form, 是 IR 的特性, 表示每个变量仅被赋值一次
- 借由简化变量的特性，来进行简化及改进编译器优化的结果

```cpp
// original
y := 1
y := 2
x := y
// SSA
y1 := 1
y2 := 2
x1 := y2
// OPT
y1 := 2
x1 := y1
```

UD 链: use-define chain, 赋值代表 define，使用变量代表 use

# Sub Project

1. LLVM Core libraries: 现代的独立于源代码和目标的优化器, 用于优化 LLVM IR
2. Clang: LLVM native C/C++/Objective-C 编译器

# Target

The LLVM representation aims to be light-weight and low-level while being expressive, typed, and extensible at the same time.

It aims to be a “universal IR” of sorts, by being at a low enough level that high-level ideas may be cleanly mapped to it (similar to how microprocessors are “universal IR’s”, allowing many source languages to be mapped to them)

# Basic

- `;` 表示行注释
- Unnamed temporaries are created when the result of a computation is not assigned to a named value.
- Unnamed temporaries are numbered sequentially (using a per-function incrementing counter, starting with 0). Note that basic blocks and unnamed function parameters are included in this numbering.
- 

# Identifiers

使用前缀 % 或 @ 是为了防止与 LLVM 内置保留字冲突

there are three different formats for identifiers, for different purposes:
1. Named values are represented as a string of characters with their prefix

> `%foo, @DivisionByZero, %a.really.long.identifier`
> Identifiers that require other characters in their names can be surrounded with quotes
> Special characters may be escaped using "\xx" where xx is the ASCII code for the character in hexadecimal

2. Unnamed values are represented as an unsigned numeric value with their prefix

> `%12, @2, %44`

3. Constants, which are described in the section Constants below.

## Global identifiers

For functions, global variables, begin with the '@' character

## Local identifiers

For register names, types, begin with the '%' character

