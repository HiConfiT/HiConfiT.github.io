---
layout: default
title: Knowledge Bases
parent: hiconfit-core
nav_order: 5
permalink: core/kb
---

# Knowledge Bases
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.0</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase.hiconfit</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>kb</em></dd>
</dl>{: .label .label-yellow }

**hiconfit-core** allows to represent knowledge bases as [Constraint Satisfaction Problems].
_**kb**_ provides classes managing a (Choco) CSP representation of a knowledge base.
Besides, it also offers two core classes representing user requirements and solutions of a configurator.

{: .highlight }
Feature model is a type of knowledge representation.
For more details related to what **hiconfit-core** supports for feature models, we refer to [Feature models].

TBD
{: .label .label-yellow }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What _kb_ provides

_**kb**_ provides the following features:

- An abstract [`KB`] class managing variables ([`Variable`]), variable domains ([`Domain`]), and constraints ([`Constraint`]) of a knowledge base/feature model.
- Two types of variables:
    1. Integer variables ([`IntVariable`])
    2. Boolean variables ([`BoolVariable`])
- Two interfaces specifying the behaviors of the knowledge base:
    1. [`IIntVarKB`] returns Choco's [`IntVar`]
    2. [`IBoolVarKB`] returns Choco's [`BoolVar`]
- [`Constraint`] manages corresponding Choco constraints, as well as their negation.
- Two utility builders [`IntVarConstraintBuilder`] and [`BoolVarConstraintBuilder`] help to build a [`Constraint`] object from a list of Choco constraints.
- Already encoded knowledge bases:
    1. [`FMKB`] - an implementation for a CSP representation of a feature model.
    The input of [`FMKB`] is a [`FeatureModel`] object.
    So you can use [`FMKB`] for any feature models you have, i.e., no need to implement a specific [`KB`] class for an individual feature model.
    [`FMKB`] uses [`BoolVariable`]s, and conforms [`IBoolVarKB`]. [`FMKB`] uses [`BoolVarConstraintBuilder`] to build constraints.
    2. [`PCKB`] - an implementation of [PC Configuration Knowledge Base].
    [`PCKB`] uses [`IntVariable`]s, and conforms [`IIntVarKB`]. [`PCKB`] uses [`IntVarConstraintBuilder`] to build constraints.
    3. [`RenaultKB`] - an implementation of [Renault Configuration Knowledge Base].
    [`RenaultKB`] uses [`IntVariable`]s, and conforms [`IIntVarKB`]. [`RenaultKB`] uses [`IntVarConstraintBuilder`] to build constraints.
    4. [`CameraKB`] - an implementation of [Camera Configuration Knowledge Base].
    [`CameraKB`] uses [`IntVariable`]s, and conforms [`IIntVarKB`]. [`CameraKB`] uses [`IntVarConstraintBuilder`] to build constraints.
- [`Assignment`] class represents an assignment of a value to a variable.
It could represent a CSP assignment or a SAT clause, e.g., `F1 = true`.
Besides, it could represent a preference of a user requirement, e.g., `Modell = limousine`.
- Two interfaces [`IAssignmentsTranslatable`] and [`ILogOpCreatable`] specifying the behaviors of a translator from an assignment to Choco constraints.
[`FMAssignmentsTranslator`] is a specific translator for feature model's assignments.
- Utility functions for variables ([`VariableUtils`]) and constraints ([`ConstraitUtils`])

{: .highlight }
Negative constraints are used in the algorithms [WipeOutR_T], [WipeOutR_FM].

## How-tos

### Encoding your own knowledge base

You can implement your knowledge base by inheriting the [`KB`] class.

{: .important-title }
> Examples
>
> [`PCKB`], [`FMKB`]

### Creating a `FMKB` object for a feature model read from a file

The following code shows how to create a [`FMKB`] object for a feature model which is parsed from a file.

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/smartwatch.sxfm");

// create a parser for the given file
@Cleanup("dispose")
FeatureModelParser<Feature, AbstractRelationship<Feature>, CTConstraint>
    parser = FMParserFactory.getInstance().getParser(fileFM.getName());

// parse the feature model file
FeatureModel<Feature, AbstractRelationship<Feature>, CTConstraint>
    fm = parser.parse(fileFM);

// create an FMKB object with the given feature model and requires to generate also the negative constraints
FMKB<Feature, AbstractRelationship<Feature>, CTConstraint>
    kb = new FMKB<>(fm, true);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

{: .highlight }
For more examples related to feature models, we refer to [Feature model].

### Creating and using an object of `FMKB`, `PCKB`, `RenaultKB`, and `CameraKB`

{: .important-title }
> Examples
>
> [`KBStatistics`], ['FMKBTest's], ['PCKBTest'], ['RenaultKBTest'], and ['CameraKBTest']

### Implementing a new assignment translator

{: .important-title }
> Example
>
> [`FMAssignmentsTranslator`]

### How to for Utility functions

TBD
{: .label .label-yellow }

<!-- Links -->
[Feature models]: /core/fm
[Constraint Satisfaction Problems]: https://en.wikipedia.org/wiki/Constraint_satisfaction_problem

[`KB`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/KB.java
[`Variable`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/Variable.java
[`Domain`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/Domain.java
[`Constraint`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/Constraint.java

[`IntVariable`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/IntVariable.java
[`BoolVariable`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/BoolVariable.java
[`IIntVarKB`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/IIntVarKB.java
[`IBoolVarKB`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/IBoolVarKB.java
[`IntVar`]: https://choco-solver.readthedocs.io/en/latest/2_modelling.html
[`BoolVar`]: https://choco-solver.readthedocs.io/en/latest/2_modelling.html

[`IntVarConstraintBuilder`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/builder/IntVarConstraintBuilder.java
[`BoolVarConstraintBuilder`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/core/builder/BoolVarConstraintBuilder.java

[`FMKB`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/fm/FMKB.java
[`FeatureModel`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fm-package/src/main/java/at/tugraz/ist/ase/hiconfit/fm/core/FeatureModel.java

[`PCKB`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/pc/PCKB.java
[PC Configuration Knowledge Base]: https://www.itu.dk/research/cla/externals/clib/

[`RenaultKB`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/renault/RenaultKB.java
[Renault Configuration Knowledge Base]: https://www.itu.dk/research/cla/externals/clib/

[`CameraKB`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/kb/camera/CameraKB.java
[Camera Configuration Knowledge Base]: https://www.itu.dk/research/cla/externals/clib/

[`Assignment`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/Assignment.java
[`IAssignmentsTranslatable`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/translator/IAssignmentsTranslatable.java
[`ILogOpCreatable`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/translator/ILogOpCreatable.java
[`FMAssignmentsTranslator`]: https://github.com/HiConfiT/hiconfit-core/blob/main/ca-cdr-core-package/src/main/java/at/tugraz/ist/ase/hiconfit/cacdr_core/translator/fm/FMAssignmentsTranslator.java
[`VariableUtils`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/common/VariableUtils.java
[`ConstraitUtils`]: https://github.com/HiConfiT/hiconfit-core/blob/main/kb-package/src/main/java/at/tugraz/ist/ase/hiconfit/common/ConstraintUtils.java

[WipeOutR_T]: /core/ca-cdr
[WipeOutR_FM]: /core/ca-cdr

[`KBStatistics`]: https://github.com/HiConfiT/KBStatistics/blob/main/src/main/java/at/tugraz/ist/ase/hiconfit/KBStatistics.java
['FMKBTest's]: https://github.com/HiConfiT/hiconfit-core/tree/main/kb-package/src/test/java/at/tugraz/ist/ase/hiconfit/kb/fm
['PCKBTest']: https://github.com/HiConfiT/hiconfit-core/tree/main/kb-package/src/test/java/at/tugraz/ist/ase/hiconfit/kb/pc
['RenaultKBTest']: https://github.com/HiConfiT/hiconfit-core/tree/main/kb-package/src/test/java/at/tugraz/ist/ase/hiconfit/kb/renault/RenaultKBTest.java
['CameraKBTest']: https://github.com/HiConfiT/hiconfit-core/tree/main/kb-package/src/test/java/at/tugraz/ist/ase/hiconfit/kb/camera/CameraKBTest.java