---
layout: default
title: Performance Evaluation
parent: hiconfit-core
nav_order: 3
permalink: core/eval
---

# Performance Evaluation
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.0</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase.hiconfit</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>eval</em></dd>
</dl>{: .label .label-yellow }

_**eval**_ provides an evaluation approach to measure the algorithm performance in terms of runtime or the number of actions performed by an algorithm.

TBD
{: .label .label-yellow }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What _eval_ provides

This package provides a performance evaluator ([`PerformanceEvaluator`]), i.e., counters ([`Counter`]) and timers ([`Timer`]), which could be used to measure the performance of algorithms.

## How-tos

### Using `PerformanceEvaluator` as well as `Counter` and `Timer`

{: .important-title }
> Examples
>
> -	[Unit test]
> -	[RuntimeForTestcasesV2]
> -	[WipeOutTEvaluationV2]

<!-- Links -->
[`PerformanceEvaluator`]: https://github.com/HiConfiT/hiconfit-core/blob/main/eval-package/src/main/java/at/tugraz/ist/ase/hiconfit/eval/PerformanceEvaluator.java
[`Counter`]: https://github.com/HiConfiT/hiconfit-core/blob/main/eval-package/src/main/java/at/tugraz/ist/ase/hiconfit/eval/Counter.java
[`Timer`]: https://github.com/HiConfiT/hiconfit-core/blob/main/eval-package/src/main/java/at/tugraz/ist/ase/hiconfit/eval/Timer.java

[Unit test]: https://github.com/HiConfiT/hiconfit-core/blob/main/eval-package/src/test/java/at/tugraz/ist/ase/hiconfit/eval/PerformanceEvaluatorTest.java
[RuntimeForTestcasesV2]: https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/RuntimeForTestcasesV2.java
[WipeOutTEvaluationV2]: https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/WipeOutRTEvaluationV2.java