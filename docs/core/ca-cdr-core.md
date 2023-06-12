---
layout: default
title: Core Classes
parent: hiconfit-core
nav_order: 6
permalink: core/ca-cdr-core
---

# Core Classes
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.0</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase.hiconfit</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>ca-cdr-core</em></dd>
    </dl>{: .label .label-yellow }

_**ca-cdr-core**_ provides core classes for representing user requirements and solutions of a configurator as well as for managing test cases and test suites.

TBD
{: .label .label-yellow }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What _ca-cdr-core_ provides

### `TestCase`

{: .highlight }
In Knowledge Base Enginering, test cases are used to induce conflicts in the knowledge base.
It’s worth noting that Test Case Driven Algorithms [4] are also made available by [_**ca-cdr**_].
Thus, _**ca-cdr-core**_ offers base classes for managing test cases and test suites.
We refer to [4] in [References] for more details related to knowledge base test cases.

A test case is a conjunction of assignments, e.g., `A=a1 & B=b3 & C=c2 & …`, where `A=a1` is an assignment, ‘&’ represents an AND operator. To feature models, test cases are simpler, e.g., `A & ~B & C`, where `A` represents `A=true` and `~B` represents `B=false`.

A test suite is a set of test cases.

_**ca-cdr-core**_ provides the following classes:

1.	[`ITestCase`] – an interface that defines which functionalities every type of test case needs to support.
<!-- In another project, I have a new type of test case called AggregatedTestCase. -->
2.	[`TestCase`] – a test case that manages a list of assignments, a corresponding list of Choco constraints, and maybe a corresponding list of negative Choco constraints.
3.	[`TestSuite`] – manages a list of [`ITestCase`].
<!-- 4.	[`TestSuiteBuilder`] – provides a function (`buildTestSuite`) that reads a test suite from a test suite file. -->
<!-- A test suite file will contain a total number of test cases in the first line and each test case written in other lines. If you need to support other structures of test suite files, you need to implement the interface [`ITestSuiteBuildable`]. -->
5.	[`FMTestCaseBuilder`] – can translate a feature model test case into a [`TestCase`] object.
To support other test case types (such as [Renault] test case - `Var1 = S64 & Var3 = M9`), you need to implement the interface [`ITestCaseBuildable`].

## How-tos

### Using `TestCase` and `TestSuite` classes

{: .important-title }
> Examples
>
> -	[Unit tests]
> -	[WipeOutR_T_Model1]
> -	[WipeOutR_T_Model2]
> -	[RuntimeForTestcasesV2]
> -	[WipeOutTEvaluationV2]


TBD
{: .label .label-yellow }

<!-- Links -->
[_**ca-cdr**_]: /core/ca-cdr
[References]: /references

[`ITestCase`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/ITestCase.java
[`TestCase`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/TestCase.java
[`TestSuite`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/TestSuite.java
[`FMTestCaseBuilder`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/builder/fm/FMTestCaseBuilder.java
[`ITestCaseBuildable`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/builder/ITestCaseBuildable.java
[Renault]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/renault/RenaultKB.java

[Unit tests]: https://github.com/HiConfiT/hiconfit-core/tree/main/ca-cdr-core-package/src/test/java/at/tugraz/ist/ase/hiconfit/cacdr_core/builder/fm
[WipeOutR_T_Model1]: https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/test/java/at/tugraz/ist/ase/wipeoutr/testmodel/WipeOutR_T_Model1.java
[WipeOutR_T_Model2]: https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/test/java/at/tugraz/ist/ase/wipeoutr/testmodel/WipeOutR_T_Model2.java
[RuntimeForTestcasesV2]: https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/RuntimeForTestcasesV2.java
[WipeOutTEvaluationV2]: https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/WipeOutRTEvaluationV2.java