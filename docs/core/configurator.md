---
layout: default
title: Configurator
parent: hiconfit-core
nav_order: 11
permalink: core/configurator
---

# Configurator
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.1.2-alpha-11</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase.hiconfit</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>configurator</em></dd>
</dl>{: .label .label-yellow }

_**configurator**_

TBD
{: .label .label-yellow }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What _configurator_ provides

## How-tos

<!-- Supports two modes: -->
<!-- 1. Compact mode -->
<!-- 2. Control mode -->

<!-- Giai đoạn khởi tạo: -->
<!-- Compact mode: -->
<!-- 1. Khởi tạo có translator và/hoặc writer -->
<!-- Control mode: -->
<!-- 1. Khởi tạo không có translator và/hoặc writer -->
<!-- 2. Gán translator -->
<!-- 3. Gán writer -->

<!-- Giai đoạn sử dụng: -->
<!-- Compact mode: -->
<!-- - findAllSolutions -->
<!-- - findSolutions -->
<!-- Control mode: -->
<!-- 1. initializeWithKB or initializeWithNotKB -->
<!-- 2. setVVO -->
<!-- 3. setRequirement -->
<!-- 4. find -->
<!-- 5. removeRequirement -->
<!-- 6. clearVVO -->
<!-- 7. reset -->


<!-- Quy trình các câu lệnh như sau: -->

<!-- {% capture code %} -->
<!-- {% highlight java linenos %} -->
<!-- // create a configurator -->
<!-- Configurator configurator = new Configurator(kb, true, new FMSolutionTranslator()); -->

<!-- // initilize the configurator with KB or with not(KB) -->
<!-- configurator.initializeWithKB(); -->
<!-- // configurator.initializeWithNotKB(); -->

<!-- // identify solutions -->
<!-- configurator.find(43, 0); -->

<!-- // reset the configurator -->
<!-- configurator.reset(); -->

<!-- // print out the solutions -->
<!-- for (Solution s : configurator.getSolutions()) { -->
<!--     System.out.print(++counter + " " + s + " - "); -->
<!-- } -->

<!-- Sau khi reset, nếu thực hiện tìm lại thì sẽ lấy lại các solutions cũ. -->
<!-- {% endhighlight %} -->
<!-- {% endcapture %} -->
<!-- {% include fix_linenos.html code=code %} -->
<!-- {% assign code = nil %} -->

<!-- {: .highlight } -->
<!-- After resetting, -->

<!-- Example 1: Sử dụng vòng lặp tìm cho đến khi nào hết solutions thì dùng -->

<!-- Configurator configurator = new Configurator(kb, true, new FMSolutionTranslator()); -->
<!-- configurator.initializeWithKB(); -->

<!-- // Identify solutions -->
<!-- while (configurator.find(1, 0, null)) { -->
<!--     // Do something with the solution -->
<!--     } -->

<!-- configurator.reset(); -->