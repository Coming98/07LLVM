# Loop Vectorization



SIMD, Single Instruction Multiple Data, 即对批量的数据同时进行同样的操作以提高效率

## Refs

- [循环优化之向量化并行（vectorization）](https://zhuanlan.zhihu.com/p/337756824)

# Inlining

Target: 消除函数调用的开销 + 函数内联可以展开被调用函数的代码从而可以创造更多的优化机会

- SimpleInliner: 其 Cost 计算相对比较复杂，主要的流程是遍历被调函数的所有指令，根据执行的指令评估函数调用代价，从而获取对被调函数进行内联的收益来决定内联的行为
- 
