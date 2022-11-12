# Overview

An optimizing, ahead-of-time compiler is usually structured as:

1. A frontend that converts source code into an intermediate representation (IR)
2. A target-independent optimization pipeline: a sequence of passes that successively rewrite the IR to eliminate inefficiencies and forms that cannot be readily translated into machine code. Sometimes called the “middle end.”
3. A target-dependent backend that generates assembly code or machine code.

# opt

支持的优化选项: `-O0, -O1, -O2, -O3, -Os, Oz`
- `O0` 表示 `不作优化`：这个级别编译最快, 生成的代码调试信息最丰富
- `O1` 介于 `O0` 和 `O2` 之间的优化级别
- `O2` 是一个适度的优化级别, 开启了大部分优化
- `O3` 和 `O2` 相似, 除了它开启更多的优化, 这些优化执行更长的时间, 或者可能产生更长的代码（以试图让程序运行得更快）
- `Os` 和 `O2` 相似, 额外开启减小代码长度的优化
- `Oz` 和 `Os` 相似, 进一步减小代码长度

内置 pass 分类: Analysis Passes、Transform Passes、Utility Passes
- Analysis Passes: 用于计算分析和输出一些 IR 信息, 用于调试用途、可视化用途等等
- Transform Passes: 实现具体的 IR 优化
- Utility Passes: 其他类别, 比如将函数释放成字节码，或者将某个模块生成字节码

## optimization list

Tips: 有时候这一轮优化的结果，就是下一轮优化的前提，所以同一个优化 pass 可以执行多次

### Analysis Passes

-aa-eval: Exhaustive Alias Analysis Precision Evaluator
-basicaa: Basic Alias Analysis (stateless AA impl)
-basiccg: Basic CallGraph Construction
-count-aa: Count Alias Analysis Query Responses
-da: Dependence Analysis
-debug-aa: AA use debugger
-domfrontier: Dominance Frontier Construction
-domtree: Dominator Tree Construction
-dot-callgraph: Print Call Graph to “dot” file
-dot-cfg: Print CFG of function to “dot” file
-dot-cfg-only: Print CFG of function to “dot” file (with no function bodies)
-dot-dom: Print dominance tree of function to “dot” file
-dot-dom-only: Print dominance tree of function to “dot” file (with no function bodies)
-dot-postdom: Print postdominance tree of function to “dot” file
-dot-postdom-only: Print postdominance tree of function to “dot” file (with no function bodies)
-globalsmodref-aa: Simple mod/ref analysis for globals
-instcount: Counts the various types of Instructions
-intervals: Interval Partition Construction
-iv-users: Induction Variable Users
-lazy-value-info: Lazy Value Information Analysis
-libcall-aa: LibCall Alias Analysis
-lint: Statically lint-checks LLVM IR
-loops: Natural Loop Information
-memdep: Memory Dependence Analysis
-module-debuginfo: Decodes module-level debug info
-postdomfrontier: Post-Dominance Frontier Construction
-postdomtree: Post-Dominator Tree Construction
-print-alias-sets: Alias Set Printer
-print-callgraph: Print a call graph
-print-callgraph-sccs: Print SCCs of the Call Graph
-print-cfg-sccs: Print SCCs of each function CFG
-print-dom-info: Dominator Info Printer
-print-externalfnconstants: Print external fn callsites passed constants
-print-function: Print function to stderr
-print-module: Print module to stderr
-print-used-types: Find Used Types
-regions: Detect single entry single exit regions
-scalar-evolution: Scalar Evolution Analysis
-scev-aa: ScalarEvolution-based Alias Analysis
-stack-safety: Stack Safety Analysis
-targetdata: Target Data Layout

### Transform Passes

-adce: Aggressive Dead Code Elimination
-always-inline: Inliner for always_inline functions
-argpromotion: Promote ‘by reference’ arguments to scalars
-bb-vectorize: Basic-Block Vectorization
-block-placement: Profile Guided Basic Block Placement
-break-crit-edges: Break critical edges in CFG
-codegenprepare: Optimize for code generation
-constmerge: Merge Duplicate Global Constants
-constprop: Simple constant propagation
-dce: Dead Code Elimination
-deadargelim: Dead Argument Elimination
-deadtypeelim: Dead Type Elimination
-die: Dead Instruction Elimination
-dse: Dead Store Elimination
-functionattrs: Deduce function attributes
-globaldce: Dead Global Elimination
-globalopt: Global Variable Optimizer
-gvn: Global Value Numbering
-indvars: Canonicalize Induction Variables
-inline: Function Integration/Inlining
-instcombine: Combine redundant instructions
-aggressive-instcombine: Combine expression patterns
-internalize: Internalize Global Symbols
-ipconstprop: Interprocedural constant propagation
-ipsccp: Interprocedural Sparse Conditional Constant Propagation
-jump-threading: Jump Threading
-lcssa: Loop-Closed SSA Form Pass
-licm: Loop Invariant Code Motion
-loop-deletion: Delete dead loops
-loop-extract: Extract loops into new functions
-loop-extract-single: Extract at most one loop into a new function
-loop-reduce: Loop Strength Reduction
-loop-rotate: Rotate Loops
-loop-simplify: Canonicalize natural loops
-loop-unroll: Unroll loops
-loop-unroll-and-jam: Unroll and Jam loops
-loop-unswitch: Unswitch loops
-loweratomic: Lower atomic intrinsics to non-atomic form
-lowerinvoke: Lower invokes to calls, for unwindless code generators
-lowerswitch: Lower SwitchInsts to branches
-mem2reg: Promote Memory to Register
-memcpyopt: MemCpy Optimization
-mergefunc: Merge Functions
-mergereturn: Unify function exit nodes
-partial-inliner: Partial Inliner
-prune-eh: Remove unused exception handling info
-reassociate: Reassociate expressions
-reg2mem: Demote all values to stack slots
-sroa: Scalar Replacement of Aggregates
-sccp: Sparse Conditional Constant Propagation
-simplifycfg: Simplify the CFG
-sink: Code sinking
-strip: Strip all symbols from a module
-strip-dead-debug-info: Strip debug info for unused symbols
-strip-dead-prototypes: Strip Unused Function Prototypes
-strip-debug-declare: Strip all llvm.dbg.declare intrinsics
-strip-nondebug: Strip all symbols, except dbg symbols, from a module
-tailcallelim: Tail Call Elimination

### Utility Passes

-deadarghaX0r: Dead Argument Hacking (BUGPOINT USE ONLY; DO NOT USE)
-extract-blocks: Extract Basic Blocks From Module (for bugpoint use)
-instnamer: Assign names to anonymous instructions
-verify: Module Verifier
-view-cfg: View CFG of function
-view-cfg-only: View CFG of function (with no function bodies)
-view-dom: View dominance tree of function
-view-dom-only: View dominance tree of function (with no function bodies)
-view-postdom: View postdominance tree of function
-view-postdom-only: View postdominance tree of function (with no function bodies)
-transform-warning: Report missed forced transformations

## ALL

-X86CondBrFolding: X86CondBrFolding
-aa: Function Alias Analysis Results
-aa-eval: Exhaustive Alias Analysis Precision Evaluator
-aarch64-a57-fp-load-balancing: AArch64 A57 FP Load-Balancing
-aarch64-branch-targets: AArch64 Branch Targets
-aarch64-ccmp: AArch64 CCMP Pass
-aarch64-collect-loh: AArch64 Collect Linker Optimization Hint (LOH)
-aarch64-condopt: AArch64 CondOpt Pass
-aarch64-copyelim: AArch64 redundant copy elimination pass
-aarch64-dead-defs: AArch64 Dead register definitions
-aarch64-expand-pseudo: AArch64 pseudo instruction expansion pass
-aarch64-fix-cortex-a53-835769-pass: AArch64 fix for A53 erratum 835769
-aarch64-jump-tables: AArch64 compress jump tables pass
-aarch64-ldst-opt: AArch64 load / store optimization pass
-aarch64-local-dynamic-tls-cleanup: AArch64 Local Dynamic TLS Access Clean-up
-aarch64-prelegalizer-combiner: Combine AArch64 machine instrs before legalization
-aarch64-promote-const: AArch64 Promote Constant Pass
-aarch64-simd-scalar: AdvSIMD Scalar Operation Optimization
-aarch64-simdinstr-opt: AArch64 SIMD instructions optimization pass
-aarch64-speculation-hardening: AArch64 speculation hardening pass
-aarch64-stp-suppress: AArch64 Store Pair Suppression
-adce: Aggressive Dead Code Elimination
-add-discriminators: Add DWARF path discriminators
-aggressive-instcombine: Combine pattern based expressions
-alignment-from-assumptions: Alignment from assumptions
-alloca-hoisting: Hoisting alloca instructions in non-entry blocks to the entry block
-always-inline: Inliner for always_inline functions
-amdgpu-aa: AMDGPU Address space based Alias Analysis
-amdgpu-aa-wrapper: AMDGPU Address space based Alias Analysis Wrapper
-amdgpu-always-inline: AMDGPU Inline All Functions
-amdgpu-annotate-kernel-features: Add AMDGPU function attributes
-amdgpu-annotate-uniform: Add AMDGPU uniform metadata
-amdgpu-argument-reg-usage-info: Argument Register Usage Information Storage
-amdgpu-atomic-optimizer: AMDGPU atomic optimizations
-amdgpu-codegenprepare: AMDGPU IR optimizations
-amdgpu-fix-function-bitcasts: Fix function bitcasts for AMDGPU
-amdgpu-inline: AMDGPU Function Integration/Inlining
-amdgpu-isel: AMDGPU DAG->DAG Pattern Instruction Selection
-amdgpu-lower-enqueued-block: Lower OpenCL enqueued blocks
-amdgpu-lower-intrinsics: Lower intrinsics
-amdgpu-lower-kernel-arguments: AMDGPU Lower Kernel Arguments
-amdgpu-lower-kernel-attributes: AMDGPU IR optimizations
-amdgpu-perf-hint: Analysis if a function is memory bound
-amdgpu-promote-alloca: AMDGPU promote alloca to vector or LDS
-amdgpu-rewrite-out-arguments: AMDGPU Rewrite Out Arguments
-amdgpu-simplifylib: Simplify well-known AMD library calls
-amdgpu-unify-divergent-exit-nodes: Unify divergent function exit nodes
-amdgpu-unify-metadata: Unify multiple OpenCL metadata due to linking
-amdgpu-usenative: Replace builtin math calls with that native versions.
-amode-opt: Optimize addressing mode
-argpromotion: Promote 'by reference' arguments to scalars
-arm-codegenprepare: ARM IR optimizations
-arm-cp-islands: ARM constant island placement and branch shortening pass
-arm-execution-domain-fix: ARM Execution Domain Fix
-arm-ldst-opt: ARM load / store optimization pass
-arm-parallel-dsp: Transform loops to use DSP intrinsics
-arm-prera-ldst-opt: ARM pre- register allocation load / store optimization pass
-arm-pseudo: ARM pseudo instruction expansion pass
-asan: AddressSanitizer: detects use-after-free and out-of-bounds bugs.
-asan-module: AddressSanitizer: detects use-after-free and out-of-bounds bugs.ModulePass
-assumption-cache-tracker: Assumption Cache Tracker
-atomic-expand: Expand Atomic instructions
-avr-expand-pseudo: AVR pseudo instruction expansion pass
-avr-relax-mem: AVR memory operation relaxation pass
-barrier: A No-Op Barrier Pass
-basicaa: Basic Alias Analysis (stateless AA impl)
-basiccg: CallGraph Construction
-bdce: Bit-Tracking Dead Code Elimination
-block-freq: Block Frequency Analysis
-bool-ret-to-int: Convert i1 constants to i32/i64 if they are returned
-bounds-checking: Run-time bounds checking
-bpf-mi-zext-elim: BPF MachineSSA Peephole Optimization
-branch-prob: Branch Probability Analysis
-break-crit-edges: Break critical edges in CFG
-called-value-propagation: Called Value Propagation
-callsite-splitting: Call-site splitting
-canonicalize-aliases: Canonicalize aliases
-cfl-anders-aa: Inclusion-Based CFL Alias Analysis
-cfl-steens-aa: Unification-Based CFL Alias Analysis
-check-debugify: Check debug info from -debugify
-check-debugify-function: Check debug info from -debugify-function
-chr: Reduce control height in the hot paths
-codegenprepare: Optimize for code generation
-consthoist: Constant Hoisting
-constmerge: Merge Duplicate Global Constants
-constprop: Simple constant propagation
-coro-cleanup: Lower all coroutine related intrinsics
-coro-early: Lower early coroutine intrinsics
-coro-elide: Coroutine frame allocation elision and indirect calls replacement
-coro-split: Split coroutine into a set of functions driving its state machine
-correlated-propagation: Value Propagation
-cost-model: Cost Model Analysis
-cross-dso-cfi: Cross-DSO CFI
-cseinfo: Analysis containing CSE Info
-da: Dependence Analysis
-dce: Dead Code Elimination
-deadargelim: Dead Argument Elimination
-deadarghaX0r: Dead Argument Hacking (BUGPOINT USE ONLY; DO NOT USE)
-debugify: Attach debug info to everything
-debugify-function: Attach debug info to a function
-delinearize: Delinearization
-demanded-bits: Demanded bits analysis
-dfsan: DataFlowSanitizer: dynamic data flow analysis.
-die: Dead Instruction Elimination
-div-rem-pairs: Hoist/decompose integer division and remainder
-divergence: Legacy Divergence Analysis
-domfrontier: Dominance Frontier Construction
-domtree: Dominator Tree Construction
-dot-callgraph: Print call graph to 'dot' file
-dot-cfg: Print CFG of function to 'dot' file
-dot-cfg-only: Print CFG of function to 'dot' file (with no function bodies)
-dot-dom: Print dominance tree of function to 'dot' file
-dot-dom-only: Print dominance tree of function to 'dot' file (with no function bodies)
-dot-postdom: Print postdominance tree of function to 'dot' file
-dot-postdom-only: Print postdominance tree of function to 'dot' file (with no function bodies)
-dot-regions: Print regions of function to 'dot' file
-dot-regions-only: Print regions of function to 'dot' file (with no function bodies)
-dot-scops: Polly: Print Scops of function
-dot-scops-only: Polly: Print Scops of function (with no function bodies)
-dse: Dead Store Elimination
-dwarfehprepare: Prepare DWARF exceptions
-early-cse: Early CSE
-early-cse-memssa: Early CSE w/ MemorySSA
-ee-instrument: Instrument function entry/exit with calls to e.g. mcount() (pre inlining)
-elim-avail-extern: Eliminate Available Externally Globals
-esan: EfficiencySanitizer: finds performance issues.
-expand-reductions: Expand reduction intrinsics
-expandmemcmp: Expand memcmp() to load/stores
-external-aa: External Alias Analysis
-extract-blocks: Extract basic blocks from module
-falkor-hwpf-fix: Falkor HW Prefetch Fix
-falkor-hwpf-fix-late: Falkor HW Prefetch Fix Late Phase
-flattencfg: Flatten the CFG
-float2int: Float to int
-forceattrs: Force set function attributes
-function-import: Summary Based Function Import
-functionattrs: Deduce function attributes
-gcn-dpp-combine: GCN DPP Combine
-generic-to-nvvm: Ensure that the global variables are in the global address space
-global-merge: Merge global variables
-globaldce: Dead Global Elimination
-globalopt: Global Variable Optimizer
-globals-aa: Globals Alias Analysis
-globalsplit: Global splitter
-guard-widening: Widen guards
-gvn: Global Value Numbering
-gvn-hoist: Early GVN Hoisting of Expressions
-gvn-sink: Early GVN sinking of Expressions
-hexagon-bit-simplify: Hexagon bit simplification
-hexagon-cext-opt: Hexagon constant-extender optimization
-hexagon-constp: Hexagon Constant Propagation
-hexagon-early-if: Hexagon early if conversion
-hexagon-gen-mux: Hexagon generate mux instructions
-hexagon-loop-idiom: Recognize Hexagon-specific loop idioms
-hexagon-nvj: Hexagon NewValueJump
-hexagon-packetizer: Hexagon Packetizer
-hexagon-rdf-opt: Hexagon RDF optimizations
-hexagon-split-double: Hexagon Split Double Registers
-hexagon-vextract: Hexagon optimize vextract
-hexagon-vlcr: Hexagon-specific predictive commoning for HVX vectors
-hotcoldsplit: Hot Cold Splitting
-hwasan: HWAddressSanitizer: detect memory bugs using tagged addressing.
-hwloops: Hexagon Hardware Loops
-indirectbr-expand: Expand indirectbr instructions
-indvars: Induction Variable Simplification
-infer-address-spaces: Infer address spaces
-inferattrs: Infer set function attributes
-inline: Function Integration/Inlining
-insert-gcov-profiling: Insert instrumentation for GCOV profiling
-instcombine: Combine redundant instructions
-instcount: Counts the various types of Instructions
-instnamer: Assign names to anonymous instructions
-instrprof: Frontend instrumentation-based coverage lowering.
-instruction-select: Select target instructions out of generic instructions
-instsimplify: Remove redundant instructions
-interleaved-access: Lower interleaved memory accesses to target specific intrinsics
-interleaved-load-combine: Combine interleaved loads into wide loads and shufflevector instructions
-internalize: Internalize Global Symbols
-intervals: Interval Partition Construction
-ipconstprop: Interprocedural constant propagation
-ipsccp: Interprocedural Sparse Conditional Constant Propagation
-irce: Inductive range check elimination
-irtranslator: IRTranslator LLVM IR -> MI
-iv-users: Induction Variable Users
-jump-threading: Jump Threading
-lazy-block-freq: Lazy Block Frequency Analysis
-lazy-branch-prob: Lazy Branch Probability Analysis
-lazy-value-info: Lazy Value Information Analysis
-lcssa: Loop-Closed SSA Form Pass
-lcssa-verification: LCSSA Verifier
-legalizer: Legalize the Machine IR a function's Machine IR
-libcalls-shrinkwrap: Conditionally eliminate dead library calls
-licm: Loop Invariant Code Motion
-lint: Statically lint-checks LLVM IR
-liveintervals: Live Interval Analysis
-load-store-vectorizer: Vectorize load and store instructions
-localizer: Move/duplicate certain instructions close to their use
-loop-accesses: Loop Access Analysis
-loop-data-prefetch: Loop Data Prefetch
-loop-deletion: Delete dead loops
-loop-distribute: Loop Distribution
-loop-extract: Extract loops into new functions
-loop-extract-single: Extract at most one loop into a new function
-loop-guard-widening: Widen guards (within a single loop, as a loop pass)
-loop-idiom: Recognize loop idioms
-loop-instsimplify: Simplify instructions in loops
-loop-interchange: Interchanges loops for cache reuse
-loop-load-elim: Loop Load Elimination
-loop-predication: Loop predication
-loop-reduce: Loop Strength Reduction
-loop-reroll: Reroll loops
-loop-rotate: Rotate Loops
-loop-simplify: Canonicalize natural loops
-loop-simplifycfg: Simplify loop CFG
-loop-sink: Loop Sink
-loop-unroll: Unroll loops
-loop-unroll-and-jam: Unroll and Jam loops
-loop-unswitch: Unswitch loops
-loop-vectorize: Loop Vectorization
-loop-versioning: Loop Versioning
-loop-versioning-licm: Loop Versioning For LICM
-loops: Natural Loop Information
-lower-expect: Lower 'expect' Intrinsics
-lower-guard-intrinsic: Lower the guard intrinsic to normal control flow
-loweratomic: Lower atomic intrinsics to non-atomic form
-lowerinvoke: Lower invoke and unwind, for unwindless code generators
-lowerswitch: Lower SwitchInst's to branches
-lowertypetests: Lower type metadata
-machine-block-freq: Machine Block Frequency Analysis
-machine-branch-prob: Machine Branch Probability Analysis
-machine-domfrontier: Machine Dominance Frontier Construction
-machine-loops: Machine Natural Loop Construction
-machine-trace-metrics: Machine Trace Metrics
-machinedomtree: MachineDominator Tree Construction
-machinepostdomtree: MachinePostDominator Tree Construction
-make-guards-explicit: Lower the guard intrinsic to explicit control flow form
-mem2reg: Promote Memory to Register
-memcpyopt: MemCpy Optimization
-memdep: Memory Dependence Analysis
-memoryssa: Memory SSA
-mergefunc: Merge Functions
-mergeicmps: Merge contiguous icmps into a memcmp
-mergereturn: Unify function exit nodes
-metarenamer: Assign new names to everything
-micromips-reduce-size: MicroMips instruction size reduce pass
-mips-branch-expansion: Expand out of range branch instructions and fix forbidden slot hazards
-mips-delay-slot-filler: Fill delay slot for MIPS
-mips-prelegalizer-combiner: Combine Mips machine instrs before legalization
-mldst-motion: MergedLoadStoreMotion
-module-debuginfo: Decodes module-level debug info
-module-summary-analysis: Module Summary Analysis
-msan: MemorySanitizer: detects uninitialized reads.
-name-anon-globals: Provide a name to nameless globals
-nary-reassociate: Nary reassociation
-newgvn: Global Value Numbering
-nvptx-assign-valid-global-names: Assign valid PTX names to globals
-nvptx-lower-aggr-copies: Lower aggregate copies, and llvm.mem* intrinsics into loops
-nvptx-lower-alloca: Lower Alloca
-nvptx-lower-args: Lower arguments (NVPTX)
-nvptx-proxyreg-erasure: NVPTX ProxyReg Erasure
-nvvm-intr-range: Add !range metadata to NVVM intrinsics.
-nvvm-reflect: Replace occurrences of __nvvm_reflect() calls with 0/1
-objc-arc: ObjC ARC optimization
-objc-arc-aa: ObjC-ARC-Based Alias Analysis
-objc-arc-apelim: ObjC ARC autorelease pool elimination
-objc-arc-contract: ObjC ARC contraction
-objc-arc-expand: ObjC ARC expansion
-opt-remark-emitter: Optimization Remark Emitter
-pa-eval: Evaluate ProvenanceAnalysis on all pairs
-packets: R600 Packetizer
-partial-inliner: Partial Inliner
-partially-inline-libcalls: Partially inline calls to library functions
-pgo-icall-prom: Use PGO instrumentation profile to promote indirect calls to direct calls.
-pgo-instr-gen: PGO instrumentation.
-pgo-instr-use: Read PGO instrumentation profile.
-pgo-memop-opt: Optimize memory intrinsic using its size value profile
-phi-values: Phi Values Analysis
-place-backedge-safepoints-impl: Place Backedge Safepoints
-place-safepoints: Place Safepoints
-polly-ast: Polly: Generate an AST from the SCoP (isl)
-polly-canonicalize: Polly: Run canonicalization passes
-polly-cleanup: Polly: Cleanup after code generation
-polly-codegen: Polly: Create LLVM-IR from SCoPs
-polly-dce: Polly: Remove dead iterations
-polly-delicm: Polly: DeLICM/DePRE
-polly-dependences: Polly: Calculate dependences
-polly-detect: Polly: Detect static control parts (SCoPs)
-polly-dump-module: Polly: Dump Module
-polly-export-jscop: Polly: Export Scops as JSON (Writes a .jscop file for each Scop)
-polly-flatten-schedule: Polly: Flatten schedule
-polly-function-dependences: Polly: Calculate dependences for all the SCoPs of a function
-polly-function-scops: Polly: Create polyhedral description of all Scops of a function
-polly-import-jscop: Polly: Import Scops from JSON (Reads a .jscop file for each Scop)
-polly-mse: Polly: Maximal static expansion of SCoP
-polly-opt-isl: Polly: Optimize schedule of SCoP
-polly-optree: Polly: Forward operand tree
-polly-prepare: Polly: Prepare code for polly
-polly-prune-unprofitable: Polly: Prune unprofitable SCoPs
-polly-rewrite-byref-params: Polly: Rewrite by reference parameters
-polly-scop-inliner: inline functions based on how much of the function is a scop.
-polly-scops: Polly: Create polyhedral description of Scops
-polly-simplify: Polly: Simplify
-polyhedral-info: Polly: Interface to polyhedral analysis engine
-post-inline-ee-instrument: Instrument function entry/exit with calls to e.g. mcount() (post inlining)
-postdomtree: Post-Dominator Tree Construction
-ppc-expand-isel: PowerPC Expand ISEL Generation
-ppc-mi-peepholes: PowerPC MI Peephole Optimization
-ppc-pre-emit-peephole: PowerPC Pre-Emit Peephole
-ppc-tls-dynamic-call: PowerPC TLS Dynamic Call Fixup
-pre-isel-intrinsic-lowering: Pre-ISel Intrinsic Lowering
-print-alias-sets: Alias Set Printer
-print-bb: Print BB to stderr
-print-callgraph: Print a call graph
-print-callgraph-sccs: Print SCCs of the Call Graph
-print-cfg-sccs: Print SCCs of each function CFG
-print-dom-info: Dominator Info Printer
-print-externalfnconstants: Print external fn callsites passed constants
-print-function: Print function to stderr
-print-lazy-value-info: Lazy Value Info Printer Pass
-print-memdeps: Print MemDeps of function
-print-memderefs: Memory Dereferenciblity of pointers in function
-print-memoryssa: Memory SSA Printer
-print-module: Print module to stderr
-print-mustexecute: Instructions which execute on loop entry
-print-predicateinfo: PredicateInfo Printer
-profile-summary-info: Profile summary info
-prune-eh: Remove unused exception handling info
-r600-expand-special-instrs: R600ExpandSpecialInstrs
-r600cf: R600 Control Flow Finalizer
-r600mergeclause: R600 Clause Merge
-reaching-deps-analysis: ReachingDefAnalysis
-reassociate: Reassociate expressions
-reg2mem: Demote all values to stack slots
-regbankselect: Assign register bank of generic virtual registers
-regions: Detect single entry single exit regions
-rewrite-statepoints-for-gc: Make relocations explicit at statepoints
-rewrite-symbols: Rewrite Symbols
-rpo-functionattrs: Deduce function attributes in RPO
-safe-stack: Safe Stack instrumentation pass
-sample-profile: Sample Profile loader
-sancov: SanitizerCoverage: TODO.ModulePass
-scalar-evolution: Scalar Evolution Analysis
-scalarize-masked-mem-intrin: Scalarize unsupported masked memory intrinsics
-scalarizer: Scalarize vector operations
-sccp: Sparse Conditional Constant Propagation
-scev-aa: ScalarEvolution-based Alias Analysis
-scoped-noalias: Scoped NoAlias Alias Analysis
-separate-const-offset-from-gep: Split GEPs to a variadic base and a constant offset for better CSE
-shadow-call-stack: Shadow Call Stack
-si-annotate-control-flow: Annotate SI Control Flow
-si-debugger-insert-nops: SI Debugger Insert Nops
-si-fix-sgpr-copies: SI Fix SGPR copies
-si-fix-vgpr-copies: SI Fix VGPR copies
-si-fix-wwm-liveness: SI fix WWM liveness
-si-fixup-vector-isel: SI Fixup Vector ISel
-si-fold-operands: SI Fold Operands
-si-form-memory-clauses: SI Form memory clauses
-si-i1-copies: SI Lower i1 Copies
-si-insert-skips: SI insert s_cbranch_execz instructions
-si-insert-waitcnts: SI Insert Waitcnts
-si-load-store-opt: SI Load Store Optimizer
-si-lower-control-flow: SI lower control flow
-si-memory-legalizer: SI Memory Legalizer
-si-mode-register: Insert required mode register values
-si-optimize-exec-masking: SI optimize exec mask operations
-si-optimize-exec-masking-pre-ra: SI optimize exec mask operations pre-RA
-si-peephole-sdwa: SI Peephole SDWA
-si-shrink-instructions: SI Shrink Instructions
-si-wqm: SI Whole Quad Mode
-simple-loop-unswitch: Simple unswitch loops
-simplifycfg: Simplify the CFG
-sink: Code sinking
-sjljehprepare: Prepare SjLj exceptions
-slotindexes: Slot index numbering
-slp-vectorizer: SLP Vectorizer
-slsr: Straight line strength reduction
-speculative-execution: Speculatively execute instructions
-sroa: Scalar Replacement Of Aggregates
-stack-safety: Stack Safety Analysis
-stack-safety-local: Stack Safety Local Analysis
-strip: Strip all symbols from a module
-strip-dead-debug-info: Strip debug info for unused symbols
-strip-dead-prototypes: Strip Unused Function Prototypes
-strip-debug-declare: Strip all llvm.dbg.declare intrinsics
-strip-gc-relocates: Strip gc.relocates inserted through RewriteStatepointsForGC
-strip-nondebug: Strip all symbols, except dbg symbols, from a module
-strip-nonlinetable-debuginfo: Strip all debug info except linetables
-structurizecfg: Structurize the CFG
-t2-reduce-size: Thumb2 instruction size reduce pass
-tailcallelim: Tail Call Elimination
-targetlibinfo: Target Library Information
-targetpassconfig: Target Pass Configuration
-tbaa: Type-Based Alias Analysis
-transform-warning: Warn about non-applied transformations
-tsan: ThreadSanitizer: detects data races.
-tti: Target Transform Information
-unreachableblockelim: Remove unreachable blocks from the CFG
-vec-merger: R600 Vector Reg Merger
-verify: Module Verifier
-verify-safepoint-ir: Safepoint IR Verifier
-view-callgraph: View call graph
-view-cfg: View CFG of function
-view-cfg-only: View CFG of function (with no function bodies)
-view-dom: View dominance tree of function
-view-dom-only: View dominance tree of function (with no function bodies)
-view-postdom: View postdominance tree of function
-view-postdom-only: View postdominance tree of function (with no function bodies)
-view-regions: View regions of function
-view-regions-only: View regions of function (with no function bodies)
-view-scops: Polly: View Scops of function
-view-scops-only: Polly: View Scops of function (with no function bodies)
-wasm-add-missing-prototypes: Add prototypes to prototypes-less functions
-wasm-argument-move: Move ARGUMENT instructions for WebAssembly
-wasm-call-indirect-fixup: Rewrite call_indirect argument orderings
-wasm-cfg-sort: Reorders blocks in topological order
-wasm-cfg-stackify: Insert BLOCK and LOOP markers for WebAssembly scopes
-wasm-eh-restore-stack-pointer: Restore Stack Pointer for Exception Handling
-wasm-exception-info: WebAssembly Exception Information
-wasm-exception-prepare: WebAssembly Late Exception Preparation
-wasm-explicit-locals: Convert registers to WebAssembly locals
-wasm-fix-function-bitcasts: Fix mismatching bitcasts for WebAssembly
-wasm-fix-irreducible-control-flow: Removes irreducible control flow
-wasm-lower-br_unless: Lowers br_unless into inverted br_if
-wasm-lower-em-ehsjlj: WebAssembly Lower Emscripten Exceptions / Setjmp / Longjmp
-wasm-lower-global-dtors: Lower @llvm.global_dtors for WebAssembly
-wasm-mem-intrinsic-results: Optimize memory intrinsic result values for WebAssembly
-wasm-optimize-live-intervals: Optimize LiveIntervals for WebAssembly
-wasm-optimize-returned: Optimize calls with "returned" attributes for WebAssembly
-wasm-peephole: WebAssembly peephole optimizations
-wasm-prepare-for-live-intervals: Fix up code for LiveIntervals
-wasm-reg-coloring: Minimize number of registers used
-wasm-reg-numbering: Assigns WebAssembly register numbers for virtual registers
-wasm-reg-stackify: Reorder instructions to use the WebAssembly value stack
-wasm-replace-phys-regs: Replace physical registers with virtual registers
-wasm-set-p2align-operands: Set the p2align operands for WebAssembly loads and stores
-wasmehprepare: Prepare WebAssembly exceptions
-wholeprogramdevirt: Whole program devirtualization
-winehprepare: Prepare Windows exceptions
-write-bitcode: Write Bitcode
-x86-avoid-SFB: Machine code sinking
-x86-cf-opt: X86 Call Frame Optimization
-x86-cmov-conversion: X86 cmov Conversion
-x86-domain-reassignment: X86 Domain Reassignment Pass
-x86-evex-to-vex-compress: Compressing EVEX instrs to VEX encoding when possible
-x86-execution-domain-fix: X86 Execution Domain Fix
-x86-fixup-LEAs: X86 LEA Fixup
-x86-fixup-bw-insts: X86 Byte/Word Instruction Fixup
-x86-flags-copy-lowering: X86 EFLAGS copy lowering
-x86-slh: X86 speculative load hardener
-x86-winehstate: Insert stores for EH state numbers

## O3

Pass Arguments:  -tti -tbaa -scoped-noalias -assumption-cache-tracker -targetlibinfo -verify -ee-instrument -simplifycfg -domtree -sroa -early-cse -lower-expect
Pass Arguments:  -targetlibinfo -tti -tbaa -scoped-noalias -assumption-cache-tracker -profile-summary-info -forceattrs -inferattrs -domtree -callsite-splitting -ipsccp -called-value-propagation -globalopt -domtree -mem2reg -deadargelim -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -basiccg -globals-aa -prune-eh -inline -functionattrs -argpromotion -domtree -sroa -basicaa -aa -memoryssa -early-cse-memssa -speculative-execution -basicaa -aa -lazy-value-info -jump-threading -correlated-propagation -simplifycfg -domtree -aggressive-instcombine -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -libcalls-shrinkwrap -loops -branch-prob -block-freq -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -pgo-memop-opt -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -tailcallelim -simplifycfg -reassociate -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -licm -loop-unswitch -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -indvars -loop-idiom -loop-deletion -loop-unroll -mldst-motion -phi-values -basicaa -aa -memdep -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -gvn -phi-values -basicaa -aa -memdep -memcpyopt -sccp -demanded-bits -bdce -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -lazy-value-info -jump-threading -correlated-propagation -basicaa -aa -phi-values -memdep -dse -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -licm -postdomtree -adce -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -barrier -elim-avail-extern -basiccg -rpo-functionattrs -globalopt -globaldce -basiccg -globals-aa -float2int -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -loop-accesses -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-distribute -branch-prob -block-freq -scalar-evolution -basicaa -aa -loop-accesses -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-vectorize -loop-simplify -scalar-evolution -aa -loop-accesses -loop-load-elim -basicaa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -domtree -loops -scalar-evolution -basicaa -aa -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -slp-vectorizer -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-unroll -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -licm -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -transform-warning -alignment-from-assumptions -strip-dead-prototypes -globaldce -constmerge -domtree -loops -branch-prob -block-freq -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -branch-prob -block-freq -loop-sink -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instsimplify -div-rem-pairs -simplifycfg -verify
Pass Arguments:  -domtree
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq

## O2

Pass Arguments:  -tti -tbaa -scoped-noalias -assumption-cache-tracker -targetlibinfo -verify -ee-instrument -simplifycfg -domtree -sroa -early-cse -lower-expect
Pass Arguments:  -targetlibinfo -tti -tbaa -scoped-noalias -assumption-cache-tracker -profile-summary-info -forceattrs -inferattrs -ipsccp -called-value-propagation -globalopt -domtree -mem2reg -deadargelim -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -basiccg -globals-aa -prune-eh -inline -functionattrs -domtree -sroa -basicaa -aa -memoryssa -early-cse-memssa -speculative-execution -basicaa -aa -lazy-value-info -jump-threading -correlated-propagation -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -libcalls-shrinkwrap -loops -branch-prob -block-freq -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -pgo-memop-opt -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -tailcallelim -simplifycfg -reassociate -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -licm -loop-unswitch -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -indvars -loop-idiom -loop-deletion -loop-unroll -mldst-motion -phi-values -basicaa -aa -memdep -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -gvn -phi-values -basicaa -aa -memdep -memcpyopt -sccp -demanded-bits -bdce -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -lazy-value-info -jump-threading -correlated-propagation -basicaa -aa -phi-values -memdep -dse -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -licm -postdomtree -adce -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -barrier -elim-avail-extern -basiccg -rpo-functionattrs -globalopt -globaldce -basiccg -globals-aa -float2int -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -loop-accesses -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-distribute -branch-prob -block-freq -scalar-evolution -basicaa -aa -loop-accesses -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-vectorize -loop-simplify -scalar-evolution -aa -loop-accesses -loop-load-elim -basicaa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -domtree -loops -scalar-evolution -basicaa -aa -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -slp-vectorizer -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-unroll -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -licm -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -transform-warning -alignment-from-assumptions -strip-dead-prototypes -globaldce -constmerge -domtree -loops -branch-prob -block-freq -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -branch-prob -block-freq -loop-sink -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instsimplify -div-rem-pairs -simplifycfg -verify
Pass Arguments:  -domtree
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq

## O1

Pass Arguments:  -tti -tbaa -scoped-noalias -assumption-cache-tracker -targetlibinfo -verify -ee-instrument -simplifycfg -domtree -sroa -early-cse -lower-expect
Pass Arguments:  -targetlibinfo -tti -tbaa -scoped-noalias -assumption-cache-tracker -profile-summary-info -forceattrs -inferattrs -ipsccp -called-value-propagation -globalopt -domtree -mem2reg -deadargelim -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -basiccg -globals-aa -prune-eh -always-inline -functionattrs -domtree -sroa -basicaa -aa -memoryssa -early-cse-memssa -speculative-execution -basicaa -aa -lazy-value-info -jump-threading -correlated-propagation -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -libcalls-shrinkwrap -loops -branch-prob -block-freq -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -pgo-memop-opt -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -tailcallelim -simplifycfg -reassociate -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -licm -loop-unswitch -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -indvars -loop-idiom -loop-deletion -loop-unroll -phi-values -memdep -memcpyopt -sccp -demanded-bits -bdce -basicaa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -lazy-value-info -jump-threading -correlated-propagation -basicaa -aa -phi-values -memdep -dse -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -licm -postdomtree -adce -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -barrier -basiccg -rpo-functionattrs -globalopt -globaldce -basiccg -globals-aa -float2int -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -loop-accesses -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-distribute -branch-prob -block-freq -scalar-evolution -basicaa -aa -loop-accesses -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-vectorize -loop-simplify -scalar-evolution -aa -loop-accesses -loop-load-elim -basicaa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-unroll -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -licm -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -transform-warning -alignment-from-assumptions -strip-dead-prototypes -domtree -loops -branch-prob -block-freq -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -branch-prob -block-freq -loop-sink -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instsimplify -div-rem-pairs -simplifycfg -verify
Pass Arguments:  -domtree
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq

## O0

Pass Arguments:  -tti -verify -ee-instrument
Pass Arguments:  -targetlibinfo -tti -assumption-cache-tracker -profile-summary-info -forceattrs -basiccg -always-inline -barrier -verify

## Os

Pass Arguments:  -tti -tbaa -scoped-noalias -assumption-cache-tracker -targetlibinfo -verify -ee-instrument -simplifycfg -domtree -sroa -early-cse -lower-expect
Pass Arguments:  -targetlibinfo -tti -tbaa -scoped-noalias -assumption-cache-tracker -profile-summary-info -forceattrs -inferattrs -ipsccp -called-value-propagation -globalopt -domtree -mem2reg -deadargelim -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -basiccg -globals-aa -prune-eh -inline -functionattrs -domtree -sroa -basicaa -aa -memoryssa -early-cse-memssa -speculative-execution -basicaa -aa -lazy-value-info -jump-threading -correlated-propagation -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -opt-remark-emitter -tailcallelim -simplifycfg -reassociate -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -licm -loop-unswitch -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -indvars -loop-idiom -loop-deletion -loop-unroll -mldst-motion -phi-values -basicaa -aa -memdep -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -gvn -phi-values -basicaa -aa -memdep -memcpyopt -sccp -demanded-bits -bdce -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -lazy-value-info -jump-threading -correlated-propagation -basicaa -aa -phi-values -memdep -dse -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -licm -postdomtree -adce -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -barrier -elim-avail-extern -basiccg -rpo-functionattrs -globalopt -globaldce -basiccg -globals-aa -float2int -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -loop-accesses -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-distribute -branch-prob -block-freq -scalar-evolution -basicaa -aa -loop-accesses -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-vectorize -loop-simplify -scalar-evolution -aa -loop-accesses -loop-load-elim -basicaa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -domtree -loops -scalar-evolution -basicaa -aa -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -slp-vectorizer -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-unroll -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -licm -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -transform-warning -alignment-from-assumptions -strip-dead-prototypes -globaldce -constmerge -domtree -loops -branch-prob -block-freq -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -branch-prob -block-freq -loop-sink -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instsimplify -div-rem-pairs -simplifycfg -verify
Pass Arguments:  -domtree
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq

## Oz

Pass Arguments:  -tti -tbaa -scoped-noalias -assumption-cache-tracker -targetlibinfo -verify -ee-instrument -simplifycfg -domtree -sroa -early-cse -lower-expect
Pass Arguments:  -targetlibinfo -tti -tbaa -scoped-noalias -assumption-cache-tracker -profile-summary-info -forceattrs -inferattrs -ipsccp -called-value-propagation -globalopt -domtree -mem2reg -deadargelim -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -basiccg -globals-aa -prune-eh -inline -functionattrs -domtree -sroa -basicaa -aa -memoryssa -early-cse-memssa -speculative-execution -basicaa -aa -lazy-value-info -jump-threading -correlated-propagation -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -opt-remark-emitter -tailcallelim -simplifycfg -reassociate -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -licm -loop-unswitch -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -indvars -loop-idiom -loop-deletion -loop-unroll -mldst-motion -phi-values -basicaa -aa -memdep -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -gvn -phi-values -basicaa -aa -memdep -memcpyopt -sccp -demanded-bits -bdce -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -lazy-value-info -jump-threading -correlated-propagation -basicaa -aa -phi-values -memdep -dse -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -licm -postdomtree -adce -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -barrier -elim-avail-extern -basiccg -rpo-functionattrs -globalopt -globaldce -basiccg -globals-aa -float2int -domtree -loops -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -loop-rotate -loop-accesses -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-distribute -branch-prob -block-freq -scalar-evolution -basicaa -aa -loop-accesses -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-vectorize -loop-simplify -scalar-evolution -aa -loop-accesses -loop-load-elim -basicaa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -domtree -basicaa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-unroll -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -licm -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -transform-warning -alignment-from-assumptions -strip-dead-prototypes -globaldce -constmerge -domtree -loops -branch-prob -block-freq -loop-simplify -lcssa-verification -lcssa -basicaa -aa -scalar-evolution -branch-prob -block-freq -loop-sink -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instsimplify -div-rem-pairs -simplifycfg -verify
Pass Arguments:  -domtree
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -branch-prob -block-freq