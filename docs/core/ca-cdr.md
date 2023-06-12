---
layout: default
title: Consistency-based Algorithms
parent: hiconfit-core
nav_order: 8
<!-- has_children: true -->
permalink: core/ca-cdr
<!-- has_toc: true -->
---

# Consistency-based Algorithms
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.0</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase.hiconfit</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>ca-cdr</em></dd>
    </dl>{: .label .label-yellow }

_**ca-cdr**_ is a library for **Consistency-based Algorithms for Conflict Detection and Resolution** (CA-CDR).

{: .highlight }
**Conflict Detection and Resolution** is a substantial task in **Knowledge Base Engineering** (KBE).
Intelligent mechanisms are urgently needed, especially in large-scale knowledge bases.
This repository publishes our implementations for some/our consistency-based algorithms,
which can be utilized in all three phases of KBE, i.e., _design_, _testing and debugging_,
and _configuration_.

TBD
{: .label .label-yellow }

## List of algorithms:

_**ca-cdr**_ provides the following algorithms:

1. [QuickXPlain] - [1]
2. [FastDiag] - [2]
3. [MSS-based FastDiag] - [15]
4. [FlexDiag] - [3]
5. [HS-tree] - [8]
6. [HSDAG] - [9]
7. [DirectDebug] - [4, 5, 6, 7]
8. [DirectDiag]
9. WipeOutR_T - [12, 13] <span>COMING SOON</span>{: .label .label-yellow .fs-1 }
10. [WipeOutR_FM] - [12, 13]
11. AggregatedTest - [14] <span>COMING SOON</span>{: .label .label-yellow .fs-1 }
12. LevelWiseParallelHSDAG - [10, 11] <span>COMING SOON</span>{: .label .label-yellow .fs-1 }
13. FullParallelHSDAG - [10, 11] <span>COMING SOON</span>{: .label .label-yellow .fs-1 }
14. FastDiagP - [15] - [Python implementation] <span>COMING SOON</span>{: .label .label-yellow .fs-1 }
15. KBDiag [the related paper submitted on January 2023] <span>COMING SOON</span>{: .label .label-yellow .fs-1 }
16. InformedQX <span>COMING SOON</span>{: .label .label-yellow .fs-1 }
17. ParallelWipeOutR_T <span>COMING SOON</span>{: .label .label-yellow .fs-1 }
18. ParallelWipeOutR_FM <span>COMING SOON</span>{: .label .label-yellow .fs-1 }

### Examples
{: .no_toc }

There are some test models in [here](https://github.com/manleviet/CDRModel/tree/main/src/main/java/at/tugraz/ist/ase/cdrmodel/test/model) and some examples showing how to use these algorithms in [here](https://github.com/manleviet/CA-CDR/tree/main/src/test/java/at/tugraz/ist/ase/cacdr/algorithms).

## [References](/references)

<!-- Links -->
[QuickXPlain]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/QuickXPlain.java
[FastDiag]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/FastDiagV2.java
[MSS-based FastDiag]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/FastDiagV3.java
[FlexDiag]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/FlexDiag.java
[HS-tree]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/hs/HSTree.java
[HSDAG]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/hs/HSDAG.java
[DirectDebug]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/DirectDebug.java
[DirectDiag]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/DirectDiag.java
[WipeOutR_FM]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr/algorithms/WipeOutR_FM.java
[Python implementation]: https://github.com/AIG-ist-tugraz/FastDiagP