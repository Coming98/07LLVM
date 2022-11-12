# Key

```json
{
    "-chr": {
        "name": "Reduce control height in the hot paths",
        "des": "This pass merges conditional blocks of code and reduces the number of conditional branches in the hot paths based on profiles.",
        "href": "https://llvm.org/doxygen/ControlHeightReduction_8cpp_source.html",
        "useful": true
    },
    "-gvn-hoist": {
        "name": "Early GVN Hoisting of Expressions",
        "des": "This pass hoists expressions from branches to a common dominator. It uses GVN (global value numbering) to discover expressions computing the same values. The primary goals of code-hoisting are: 1. To reduce the code size. 2. In some cases reduce critical path (by exposing more ILP).",
        "href": "https://llvm.org/doxygen/GVNHoist_8cpp_source.html",
        "useful": true
    },
    "-instruction-select": {
        "name": "Select target instructions out of generic instructions",
        "des": "This pass transforms generic machine instructions into equivalent target-specific instructions. It traverses the MachineFunction bottom-up, selecting uses before definitions, enabling trivial dead code elimination.",
        "href": "https://llvm.org/docs/GlobalISel/InstructionSelect.html",
        "useful": null
    },
    "-div-rem-pairs": {
        "name": "Hoist/decompose integer division and remainder",
        "des": "This pass hoists and/or decomposes/recomposes integer division and remainder instructions to enable CFG improvements and better codegen.",
        "href": "https://llvm.org/doxygen/DivRemPairs_8cpp_source.html",
        "useful": true
    },
    "-interleaved-access": {
        "name": "Lower interleaved memory accesses to target specific intrinsics",
        "des": "This file implements the Interleaved Access pass, which identifies interleaved memory accesses and transforms them into target specific intrinsics.",
        "href": "https://llvm.org/doxygen/InterleavedAccessPass_8cpp_source.html",
        "useful": true
    },
    "-gvn-sink": {
        "name": "Early GVN sinking of Expressions",
        "des": "This pass attempts to sink instructions into successors, reducing static instruction count and enabling if-conversion.",
        "href": "https://llvm.org/doxygen/GVNSink_8cpp_source.html",
        "useful": true
    },
    "-elim-avail-extern": {
        "name": "Eliminate Available Externally Globals",
        "des": "This transform is designed to eliminate available external global definitions from the program, turning them into declarations.",
        "href": "https://llvm.org/doxygen/ElimAvailExtern_8cpp_source.html",
        "useful": true
    },
    "-flattencfg": {
        "name": "Flatten the CFG",
        "des": "Reduce conditional branches in CFG.",
        "href": "https://llvm.org/doxygen/FlattenCFG_8cpp_source.html",
        "useful": true
    },
    "-localizer": {
        "name": "Move/duplicate certain instructions close to their use",
        "des": "This file implements the Localizer class.",
        "href": "https://llvm.org/doxygen/Localizer_8cpp_source.html",
        "useful": true
    },
    "-loop-idiom": {
        "name": "Recognize loop idioms",
        "des": "This pass implements an idiom recognizer that transforms simple loops into a non-loop form. In cases that this kicks in, it can be a significant performance win.",
        "href": "https://llvm.org/doxygen/LoopIdiomRecognize_8cpp_source.html",
        "useful": true
    },
    "-loop-instsimplify": {
        "name": "Simplify instructions in loops",
        "des": "This pass performs lightweight instruction simplification on loop bodies.",
        "href": "https://llvm.org/doxygen/LoopInstSimplify_8cpp_source.html",
        "useful": true
    },
    "-loop-simplifycfg": {
        "name": "Simplify loop CFG",
        "des": "This file implements the Loop SimplifyCFG Pass. This pass is responsible forbasic loop CFG cleanup, primarily to assist other loop passes. If youencounter a noncanonical CFG construct that causes another loop pass toperform suboptimally, this is the place to fix it up.",
        "href": "https://llvm.org/doxygen/LoopSimplifyCFG_8cpp_source.html",
        "useful": true
    },
    "-metarenamer": {
        "name": "Assign new names to everything",
        "des": "This pass renames everything with metasyntatic names. The intent is to use this pass after bugpoint reduction to conceal the nature of the original program.",
        "href": "https://llvm.org/doxygen/MetaRenamer_8cpp_source.html",
        "useful": true
    },
    "-mldst-motion": {
        "name": "MergedLoadStoreMotion",
        "des": "This pass performs merges of loads and stores on both sides of a diamond (hammock). It hoists the loads and sinks the stores.",
        "href": "https://llvm.org/doxygen/MergedLoadStoreMotion_8cpp_source.html",
        "useful": true
    },
    "-msan": {
        "name": "MemorySanitizer:  detects uninitialized reads.",
        "des": "This file is a part of MemorySanitizer, a detector of uninitialized reads.",
        "href": "https://llvm.org/doxygen/MemorySanitizer_8cpp_source.html",
        "useful": true
    },
    "-nary-reassociate": {
        "name": "Nary reassociation",
        "des": "This pass reassociates n-ary add expressions and eliminates the redundancy exposed by the reassociation.",
        "href": "https://llvm.org/doxygen/NaryReassociate_8cpp_source.html",
        "useful": true
    },
    "-objc-arc-contract": {
        "name": "ObjC ARC contraction",
        "des": "This specific file mainly deals with ``contracting'' multiple lower level operations into singular higher level operations through pattern matching.",
        "href": "https://llvm.org/doxygen/ObjCARCContract_8cpp_source.html",
        "useful": true
    },
    "-polly-optree": {
        "name": "Polly:  Forward operand tree",
        "des": "Move instructions between statements.",
        "href": "https://polly.llvm.org/doxygen/ForwardOpTree_8cpp_source.html",
        "useful": true
    },
    "-separate-const-offset-from-gep": {
        "name": "Split GEPs to a variadic base and a constant offset for better CSE",
        "des": "Loop unrolling may create many similar GEPs for array accesses. ",
        "href": "https://llvm.org/doxygen/SeparateConstOffsetFromGEP_8cpp_source.html",
        "useful": true
    },
    "-simple-loop-unswitch": {
        "name": "Simple unswitch loops",
        "des": "This pass transforms loops that contain branches or switches on loop-invariant conditions to have multiple loops",
        "href": "https://llvm.org/doxygen/SimpleLoopUnswitch_8cpp_source.html",
        "useful": true
    },
    "-slp-vectorizer": {
        "name": "SLP Vectorizer",
        "des": "This pass implements the Bottom Up SLP vectorizer. It detects consecutive stores that can be put together into vector-stores. Next, it attempts to construct vectorizable tree using the use-def chains. If a profitable tree was found, the SLP vectorizer performs vectorization on the tree.",
        "href": "https://llvm.org/doxygen/SLPVectorizer_8cpp_source.html",
        "useful": true
    },
    "-slsr": {
        "name": "Straight line strength reduction",
        "des": "This file implements straight-line strength reduction (SLSR). Unlike loopstrength reduction, this algorithm is designed to reduce arithmeticredundancy in straight-line code instead of loops. It has proven to beeffective in simplifying arithmetic statements derived from an unrolled loop.It can also simplify the logic of SeparateConstOffsetFromGEP.There are many optimizations we can perform in the domain of SLSR. ",
        "href": "https://llvm.org/doxygen/StraightLineStrengthReduce_8cpp_source.html",
        "useful": true
    },
    "-structurizecfg": {
        "name": "Structurize the CFG",
        "des": "",
        "href": "https://llvm.org/doxygen/StructurizeCFG_8cpp_source.html",
        "useful": true
    },
    "-unreachableblockelim": {
        "name": "Remove unreachable blocks from the CFG",
        "des": "This pass is an extremely simple version of the SimplifyCFG pass.  Its solejob is to delete LLVM basic blocks that are not reachable from the entrynode.  To do this, it performs a simple depth first traversal of the CFG,then deletes any unvisited nodes.",
        "href": "https://llvm.org/doxygen/UnreachableBlockElim_8cpp_source.html",
        "useful": false
    },
    "-x86-cf-opt": {
        "name": "X86 Call Frame Optimization",
        "des": "This file defines a pass that optimizes call sequences on x86. ",
        "href": "https://llvm.org/doxygen/X86CallFrameOptimization_8cpp_source.html",
        "useful": true
    },
    "-always-inline": {
        "name": "Inliner for always_inline functions",
        "des": "This file implements a custom inliner that handles only functions that are marked as always inline.",
        "href": "https://llvm.org/doxygen/AlwaysInliner_8cpp_source.html",
        "useful": true
    },
    "-bb-vectorize": {
        "name": "Basic-Block Vectorization",
        "des": "This header file defines prototypes for accessor functions that expose passes in the Vectorize transformations library.",
        "href": "https://llvm.org/doxygen/Transforms_2Vectorize_8h_source.html",
        "useful": true
    },
    "-block-placement": {
        "name": "Profile Guided Basic Block Placement",
        "des": "This file implements basic block placement transformations using the CFG structure and branch probability estimates.",
        "href": "https://llvm.org/doxygen/MachineBlockPlacement_8cpp_source.html",
        "useful": true
    },
    "-deadargelim": {
        "name": "Dead Argument Elimination",
        "des": "Dead argument elimination removes arguments which are directly dead, as well as arguments only passed into function calls as dead arguments of other functions. This pass also deletes dead return values in a similar way.",
        "href": "https://llvm.org/doxygen/DeadArgumentElimination_8cpp_source.html",
        "useful": true
    },
    "-globalopt": {
        "name": "Global Variable Optimizer",
        "des": "This pass transforms simple global variables that never have their address taken. If obviously true, it marks read/write globals as constant, deletes variables only stored to, etc.",
        "href": "https://llvm.org/doxygen/GlobalOpt_8cpp_source.html",
        "useful": true
    },
    "-indvars": {
        "name": "Canonicalize Induction Variables",
        "des": "This transformation analyzes and transforms the induction variables (and computations derived from them) into simpler forms suitable for subsequent analysis and transformation.",
        "href": "https://llvm.org/doxygen/IndVarSimplify_8cpp_source.html",
        "useful": true
    },
    "-instcombine": {
        "name": "Combine redundant instructions",
        "des": "InstructionCombining - Combine instructions to form fewer, simple instructions.",
        "href": "https://llvm.org/doxygen/InstructionCombining_8cpp_source.html",
        "useful": true
    },
    "-jump-threading": {
        "name": "Jump Threading",
        "des": "This file implements the Jump Threading pass.",
        "href": "https://llvm.org/doxygen/JumpThreading_8cpp_source.html",
        "useful": true
    },
    "-lcssa": {
        "name": "Loop-Closed SSA Form Pass",
        "des": "This pass transforms loops by placing phi nodes at the end of the loops for all values that are live across the loop boundary.  For example, it turns the left into the right code",
        "href": "https://llvm.org/doxygen/LCSSA_8cpp_source.html",
        "useful": true
    },
    "-licm": {
        "name": "Loop Invariant Code Motion",
        "des": "This pass performs loop invariant code motion, attempting to remove as much code from the body of a loop as possible.",
        "href": "https://llvm.org/doxygen/LICM_8cpp_source.html",
        "useful": true
    },
    "-loop-deletion": {
        "name": "Delete dead loops",
        "des": "This file implements the Dead Loop Deletion Pass. This pass is responsible for eliminating loops with non-infinite computable trip counts that have no side effects or volatile instructions, and do not contribute to the  computation of the function's return value.",
        "href": "https://llvm.org/doxygen/LoopDeletion_8cpp_source.html",
        "useful": true
    },
    "-loop-extract": {
        "name": "Extract loops into new functions",
        "des": "A pass wrapper around the ExtractLoop() scalar transformation to extract eachtop-level loop into its own new function. If the loop is the ONLY loop in agiven function, it is not touched. This is a pass most useful for debuggingvia bugpoint.",
        "href": "https://llvm.org/doxygen/LoopExtractor_8cpp_source.html",
        "useful": true
    },
    "-loop-extract-single": {
        "name": "Extract at most one loop into a new function",
        "des": "A pass wrapper around the ExtractLoop() scalar transformation to extract eachtop-level loop into its own new function. If the loop is the ONLY loop in agiven function, it is not touched. This is a pass most useful for debuggingvia bugpoint.",
        "href": "https://llvm.org/doxygen/LoopExtractor_8cpp_source.html",
        "useful": true
    },
    "-loop-simplify": {
        "name": "Canonicalize natural loops",
        "des": "This pass performs several transformations to transform natural loops into a simpler form, which makes subsequent analyses and transformations simpler and more effective.",
        "href": "https://llvm.org/doxygen/LoopSimplify_8cpp_source.html",
        "useful": true
    },
    "-loop-unroll": {
        "name": "Unroll loops",
        "des": "This file implements some loop unrolling utilities for loops with run-timetrip counts",
        "href": "https://llvm.org/doxygen/LoopUnrollRuntime_8cpp_source.html",
        "useful": true
    },
    "-loop-unswitch": {
        "name": "Unswitch loops",
        "des": "This pass transforms loops that contain branches or switches on loop-invariant conditions to have multiple loops",
        "href": "https://llvm.org/doxygen/SimpleLoopUnswitch_8cpp_source.html",
        "useful": true
    },
    "-lowerswitch": {
        "name": "Lower SwitchInsts to branches",
        "des": "The LowerSwitch transformation rewrites switch instructions with a sequence of branches, which allows targets to get away with not implementing the switch instruction until it is convenient.",
        "href": "https://llvm.org/doxygen/LowerSwitch_8cpp_source.html",
        "useful": true
    },
    "-reassociate": {
        "name": "Reassociate expressions",
        "des": "This pass reassociates commutative expressions in an order that is designed to promote better constant propagation, GCSE, LICM, PRE, etc.",
        "href": "https://llvm.org/doxygen/Reassociate_8cpp_source.html",
        "useful": true
    },
    "-simplifycfg": {
        "name": "Simplify the CFG",
        "des": "https://llvm.org/doxygen/SimplifyCFG_8cpp_source.html",
        "href": "https://llvm.org/doxygen/SimplifyCFG_8cpp_source.html",
        "useful": true
    },
}
```