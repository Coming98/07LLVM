# Overview

- [Github](https://github.com/lifting-bits/mcsema)

McSema is an executable lifter. It translates ("lifts") executable binaries from native machine code to LLVM bitcode.

The lifted LLVM bitcode can also be fuzzed with libFuzzer, an LLVM-based instrumented fuzzer that would otherwise require the target source code.

The lifted bitcode can even be compiled back into a runnable program! This is a procedure known as static binary rewriting, binary translation, or binary recompilation.

## Two Steps

1. control flow recovery: `mcsema-disass` while relies on IDA Pro to disassemble a binary file and produce a control flow graph
2. instruction translation: `mcsema-lift` which converts the control flow graph into LLVM bitcode
- Under the hood, the instruction translation capability of mcsema-lift is implemented in the remill library. 
- The development of remill was a result of refactoring and improvements to McSema, and was first introduced with McSema version 2.0.0.

## Key Features
- Lifts 32- and 64-bit Linux ELF and Windows PE binaries to bitcode, including executables and shared libraries for each platform.
- McSema can cross-lift: it can translate Linux binaries on Windows, or Windows binaries on Linux.
- Output bitcode is compatible with the LLVM toolchain (versions 3.5 and up).
- Translated bitcode can be analyzed or [recompiled](https://github.com/lifting-bits/mcsema/blob/master/docs/McSemaWalkthrough.md) as a new, working executable with functionality identical to the original.

## Use-cases

- Binary Patching And Modification
- Re-use existing LLVM-based tools: [KLEE](https://klee.github.io/), LLVM optimization passes, [LibFuzzer](http://llvm.org/docs/LibFuzzer.html), [lifted bitcode](https://github.com/lifting-bits/mcsema/blob/master/docs/UsingLibFuzzer.md)
- Analyze the binary rather than the source
- Write one set of analysis tools: Lifting to LLVM IR means that one set of analysis tools can work on both the source and the binary

# Tools

## mcsema-disass

Usage:

```shell
mcsema-disass 
--disassembler path-to-IDA 
--os operating-system 
--arch architecture 
--output cfg-path 
--binary input-binary 
--entrypoint function 
[--log_file log-path]
```

- path-to-IDA:  the path to your IDA Pro disassembler executable, e.g., `~/ida-6.9/idal64`
- operating-system: the **OS of the binary** being disassembled: linux, or windows
- architecture: the instruction set architecture of the binary being disassembled: `amd64, amd64_avx, x86, x86_avx, or aarch64 (64-bit ARMv8)`
- cfg-path: the path a .cfg file where you want the recovered control flow graph to be saved  
- input-binary: the path to a binary executable to be disassembled
- function: the entry point function where the disassembler should start recovering control flow, e.g., main
- log-path: (optional) the path to a log file to save the logging output of McSema

```shell
mcsema-disass --disassembler ~/idademo-7.5/ida64 --os linux --arch amd64 --log_file ./xz.log --output ./xz.cfg --binary ./xz --entrypoint main --pie-mode --rebase 535822336

ida64.exe -S"C:\Users\cjc\Desktop\mcsema_disass\ida7\get_cfg.py --output C:\Users\cjc\Desktop\xz.cfg --log_file C:\Users\cjc\Desktop\xz.log --arch amd64 --os linux --entrypoint main --rebase 535822336 --pie-mode" C:\Users\cjc\Desktop\xz
```

## mcsema-lift

```shell
mcsema-lift-${version} 
--arch architecture 
--os operating-system  
--cfg cfg-path 
[--output output-path] 
[--libc_constructor init-function] 
[--libc_destructor fini-function]
```

- output-path: path to a .bc file where you want the lifted code to be saved. If the --output option is not specified, the bitcode will be written to stdout
- init-function: constructor function for running pre-main initializers. It is executed before the main and constructs the global objects. This feature is important for lifting the C++ programs. On GNU-based systems, this is typically __libc_csu_init
- fini-function: destructor function for running post-main finalizers. It is executed after the main function at program exit. On GNU-based systems, this is typically __libc_csu_fini

```shell
mcsema-lift-12 --os linux --arch amd64 --cfg ~/demo/demo.cfg --output ~/demo/demo.bc

mcsema-lift-12 \
    --arch amd64 \
    --os linux \
    --cfg xz.cfg \
    --output xz.bc \
    --explicit_args \
    --merge_segments \
    --name_lifted_sections

remill-clang-12 -o xz.lifted xz.bc -lpthread -lm -ldl -llzma -Wl,--section-start=.section_1ff00000=0x1ff00000
```

# Liminations

- Latest commit: 2017

1. McSema is desiged to translate compiler-generated binaries. It will probably not handle packed, encrypted, or otherwise obfuscated code.
2. We do not support raw binary blobs (e.g. firmware).
3. McSema currently pretends that exceptions do not exist; if they do, then it assumes something else will handle them correctly.

