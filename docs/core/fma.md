---
layout: default
title: Feature Model Analysis
parent: hiconfit-core
nav_order: 12
permalink: core/fma
---

# Feature Model Analysis
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.0</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase.hiconfit</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>fma</em></dd>
</dl>{: .label .label-yellow }

TBD
{: .label .label-yellow }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction

TBD
{: .label .label-yellow }

## How-tos

### Simple usage

The following example shows a simple usage:

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/basic_featureide_multiple1.xml");

// 1. Create the factory for anomaly feature models
IFeatureBuildable featureBuilder = new AnomalyAwareFeatureBuilder();
FMParserFactory<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    factory = FMParserFactory.getInstance(featureBuilder);

// 2. Create the parser
@Cleanup("dispose")
FeatureModelParser<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    parser = factory.getParser(fileFM.getName());

// 3. Parse the feature model
FeatureModel<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    featureModel = parser.parse(fileFM);

// 4. Create an analyzer
FMAnalyzer analyzer = new FMAnalyzer(featureModel);

// 5. Select analysis operations to be performed
EnumSet<AnomalyType> options = EnumSet.of(AnomalyType.DEAD,
                                        AnomalyType.FULLMANDATORY,
                                        AnomalyType.REDUNDANT);

// 6. Generate VoidFMAnalysis, DeadFeatureAnalysis, FullMandatoryAnalysis, and RedundancyAnalysis
// And Run the analyzer
// (true - trigger the corresponding explanator if the assumption is violated)
analyzer.generateAndRun(options, true);

// 7. Print the result
AutomatedAnalysisExplanation explanation = new AutomatedAnalysisExplanation();
System.out.println(explanation.getDescriptiveExplanation(analyzer.getAnalyses(), options));
// generated explanations depends on options
// in this case where options don't include VOID, the VoidFMAnalysis' results won't be printed
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

If you want to perform all built-in analyses, you can replace the statement in Step 5 by the following statement:

{% capture code %}
{% highlight java linenos %}
EnumSet<AnomalyType> options = EnumSet.allOf(AnomalyType.class);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

{: .important-title }
> Example
>
> [`testMultiple_1`]

### Usage of `FMAnalyzer`'s `run` method

Use `run` method if you read test cases from a file.

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/basic_featureide_multiple1.xml");

// 1. Create the factory for anomaly feature models
IFeatureBuildable featureBuilder = new AnomalyAwareFeatureBuilder();
FMParserFactory<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    factory = FMParserFactory.getInstance(featureBuilder);

// 2. Create the parser
@Cleanup("dispose")
FeatureModelParser<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    parser = factory.getParser(fileFM.getName());
// 3. Parse the feature model
FeatureModel<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    featureModel = parser.parse(fileFM);

// 4. Create an analyzer
FMAnalyzer analyzer = new FMAnalyzer(featureModel);

// 5. Read test cases from a file and add to analyzer
EnumSet<AnomalyType> options = EnumSet.allOf(AnomalyType.class);

// read pre-generated test cases from a file
XMLAssumptionAwareTestSuiteReader reader = new XMLAssumptionAwareTestSuiteReader(featureModel);
XMLAssumptionAwareTestCaseBuilder builder = new XMLAssumptionAwareTestCaseBuilder(featureModel);
@Cleanup
InputStream is = getInputStream(FMAnalyzerTest.class.getClassLoader(), "testsuite_multiple1.xml");
TestSuite testSuite = reader.read(is, builder);
// generates analyses and add them to the analyzer
AutomatedAnalysisBuilder analysisBuilder = new AutomatedAnalysisBuilder();
analysisBuilder.build(featureModel, testSuite, analyzer);

// 6. Run the analyzer
// (true - trigger the corresponding explanator if the assumption is violated)
// execute the VoidFMAnalysis first if there is any
analyzer.run(true);

// 8. Print the result
EnumSet<AnomalyType> options = EnumSet.allOf(AnomalyType.class);
AutomatedAnalysisExplanation explanation = new AutomatedAnalysisExplanation();
System.out.println(explanation.getDescriptiveExplanation(analyzer.getAnalyses(), options));
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

{: .highlight }
[`AutomatedAnalysisBuilder`] and [`AutomatedAnalysisExplanation`] are utility classes that provide useful and shortcut ways to build built-in analyses
and explanations.

{: .important-title }
> Example
>
> [`testMultiple_0`]

### Usage of a specific analysis builder and explanation

You can also use directly specific builder and explanation classes to build and explain analyses.
The following example shows how to analyze dead features by using [`DeadFeatureAnalysisBuilder`] and [`CompactExplanation`]:

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/bamboobike_featureide_deadfeature1.xml");

// 1. Create the factory for anomaly feature models
IFeatureBuildable featureBuilder = new AnomalyAwareFeatureBuilder();
FMParserFactory<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    factory = FMParserFactory.getInstance(featureBuilder);

// 2. Create the parser
@Cleanup("dispose")
FeatureModelParser<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    parser = factory.getParser(fileFM.getName());
// 3. Parse the feature model
FeatureModel<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    featureModel = parser.parse(fileFM);

// 4. Create an analyzer
FMAnalyzer analyzer = new FMAnalyzer(featureModel);

// (omitted) 5. Select analysis operations to be performed

// 6. Generates analyses and adds them to the analyzer (USING DeadFeatureAnalysisBuilder)
DeadFeatureAnalysisBuilder deadFeatureAnalysisBuilder = new DeadFeatureAnalysisBuilder();
deadFeatureAnalysisBuilder.build(featureModel, analyzer);

// 7. Run the analyzer
// (true - trigger the corresponding explanator if the assumption is violated)
analyzer.run(true);

// 8. Print the result (USING CompactExplanation)
CompactExplanation explanation = new CompactExplanation();
System.out.println(explanation.getDescriptiveExplanation(analyzer.getAnalyses(), DeadFeatureAnalysis.class, AnomalyType.DEAD));
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

{: .highlight }
> [`CompactExplanation`] provides explanations for four analyses, including [`DeadFeatureAnalysis`], [`FalseOptionalAnalysis`],
> [`FullMandatoryAnalysis`], and [`ConditionallyDeadAnalysis`].

{: .important-title }
> Example
>
> [testDeadFeature_0]

### Monitoring the progress of analysis

Before executing the analyzer, you can register a listener to monitor the progress of analysis.

{% capture code %}
{% highlight java linenos %}
analyzer.setMonitor(new ProgressMonitor()); // MONITOR
// 7. Run the analyzer
analyzer.run(true);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

[`ProgressMonitor`] as default will print the progress of analysis to the console.
By conforming to the interface [`IAnalysisMonitor`], you can direct the output of analysis to other streams.

{: .important-title }
> Example
>
> [testLargeModel_2]

### Implementing your new analysis operation

1. Create a new enum type that conforms to the interface [`IAnomalyType`]. Ex: [`AnomalyType`].
2. Create a new "Assumptions" class that conforms to the class [`IFMAnalysisAssumptionCreatable`].
Assumptions classes are used to generate test cases for the analysis operation. Ex: [`DeadFeatureAssumptions`].
3. Create a new "Analysis" class that extends the class [`AbstractFMAnalysis`].
Analysis classes are used to perform the analysis operation. Ex: [`DeadFeatureAnalysis`].
4. Create a new "Explanator" class that extends the class [`AbstractAnomalyExplanator`].
Explanator classes identify diagnoses for violated assumptions. Ex: [`DeadFeatureExplanator`].
5. Create a new "Builder" class that conforms to the class [`IAnalysisBuildable`].
Builder classes generate analyses. Ex: [`DeadFeatureAnalysisBuilder`].
6. Create a new "Explanation" class conforming to the class [`IAnalysisExplanation`].
Explanation classes take charge of generating explanations for the analysis results. Ex: [`CompactExplanation`].

<!-- Links -->
[`testMultiple_1`]: https://github.com/HiConfiT/hiconfit-core/blob/38f314ed632089f56b87db5870ce4c915157feb7/fma-package/src/test/java/at/tugraz/ist/ase/hiconfit/fma/FMAnalyzerTest.java#L1349

[`AutomatedAnalysisBuilder`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/builder/AutomatedAnalysisBuilder.java
[`AutomatedAnalysisExplanation`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/explanation/AutomatedAnalysisExplanation.java
[`testMultiple_0`]: https://github.com/HiConfiT/hiconfit-core/blob/38f314ed632089f56b87db5870ce4c915157feb7/fma-package/src/test/java/at/tugraz/ist/ase/hiconfit/fma/FMAnalyzerTest.java#L1309

[`DeadFeatureAnalysisBuilder`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/builder/DeadFeatureAnalysisBuilder.java
[`CompactExplanation`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/explanation/CompactExplanation.java

[`DeadFeatureAnalysis`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/analysis/DeadFeatureAnalysis.java
[`FalseOptionalAnalysis`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/analysis/FalseOptionalAnalysis.java
[`FullMandatoryAnalysis`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/analysis/FullMandatoryAnalysis.java
[`ConditionallyDeadAnalysis`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/analysis/ConditionallyDeadAnalysis.java

[testDeadFeature_0]: https://github.com/HiConfiT/hiconfit-core/blob/38f314ed632089f56b87db5870ce4c915157feb7/fma-package/src/test/java/at/tugraz/ist/ase/hiconfit/fma/FMAnalyzerTest.java#L234

[`ProgressMonitor`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/monitor/ProgressMonitor.java
[`IAnalysisMonitor`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/monitor/IAnalysisMonitor.java

[testLargeModel_2]: https://github.com/HiConfiT/hiconfit-core/blob/38f314ed632089f56b87db5870ce4c915157feb7/fma-package/src/test/java/at/tugraz/ist/ase/hiconfit/fma/FMAnalyzerTest.java#L1532

[`IAnomalyType`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/anomaly/IAnomalyType.java
[`AnomalyType`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/anomaly/AnomalyType.java
[`IFMAnalysisAssumptionCreatable`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/assumption/IFMAnalysisAssumptionCreatable.java
[`DeadFeatureAssumptions`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/assumption/DeadFeatureAssumptions.java
[`AbstractFMAnalysis`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/analysis/AbstractFMAnalysis.java
[`AbstractAnomalyExplanator`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/explanator/AbstractAnomalyExplanator.java
[`DeadFeatureExplanator`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/explanator/DeadFeatureExplanator.java
[`IAnalysisBuildable`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/builder/IAnalysisBuildable.java
[`DeadFeatureAnalysisBuilder`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/builder/DeadFeatureAnalysisBuilder.java
[`IAnalysisExplanation`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/explanation/IAnalysisExplanable.java
[`CompactExplanation`]: https://github.com/HiConfiT/hiconfit-core/blob/main/fma-package/src/main/java/at/tugraz/ist/ase/hiconfit/fma/explanation/CompactExplanation.java