
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ILS: An R package for statistical analysis in Interlaboratory Studies

<!-- badges: start -->
<!-- badges: end -->

## Overview

The main objective of the ILS package is to detect laboratories that
provide not consistent results, working simultaneously with different
test materials, from the perspective of the Univariate Data Analysis and
the Functional Data Analysis (FDA).

The ILS package can identify laboratories that provide significantly
different results through the estimation the Mandel’s h and k scalar
statistics, based on the ASTM E691 and ISO 5725-2 standards.
Additionally, the package has implemented tools to assess the presence
of outliers using the Cochran and Grubbs tests.

Furthermore, Analysis of Variance (ANOVA) techniques are provided, both
for the cases of fixed and random effects, including confidence
intervals for the principles parameters.

Moreover, one of the novelties of this package is the incorporation of
tools to perform an ILS from a functional data analysis approach.
Accordingly, the functional nature of the data obtained by experimental
techniques corresponding to analytical chemistry, applied physics and
engineering applications (spectra, thermograms, and sensor signals,
among others) is taking into account by implementing the functional
extensions of Mandel’s h and k statistics.

<br>

## Installation

You can install the development version of ILSR6V1 from
[GitHub](https://github.com/) with:

``` r
# install.packages("ILSR6V1")
library("ILSR6V1")
```

<br>

## Concepts across the board

**ILS package** addresses several concepts and approaches which will be
discussed in detail in the later sections of this article. The most
relevant concepts can be found below:

-   **Interlaboratory Study (ILS)**:

    This concept can be defined as a control procedure to evaluate the
    performance of a group of laboratories through a collaborative
    trials. In an Interlaboratory Study, an adequate number of
    laboratories are chosen to participate in the experiment with the
    aim of analyzing the samples and obtain results.

    Participating laboratories receive samples (previously homogenized
    or to be homogenized by the laboratories) for analysis, then, the
    measurements results of the laboratories are evaluated according to
    the degree of data variability. Some of the most common factors that
    may be a cause of variability are: the equipment of laboratories,
    operators, materials, temperature and humidity, among others.

-   **Repeatability and Reproducibility studies (R&R)**:

    Repeatability and reproducibility (R&R) studies are a relevant
    methodology in quality control that assess the accuracy of a
    measurement system. In addition, R&R studies allow the
    identification of errors and sources of variation in the measurement
    process, and are essential to ensure the reliability and accuracy of
    the results.

    This tool of quality control focuses on two key aspects of
    measurement:

    **Repeatability:** Repeatability is the variation between successive
    measurements of the same part or trait by the same person using the
    same gage. In other words, how much variation do we see in
    measurements taken by the same person, on the same part, using the
    same tool.

    **Reproducibility:** Reproducibility is the difference in the
    average of the measurements made by different people using the same
    instrument when measuring the identical characteristics on the same
    part. In other words, how much variation do we see in measurements
    taken by different people on the same part using the same too.

-   **Consistency tests**:

    Several scalar statistical techniques are frequently applied to
    study the consistency of test results from the different
    laboratories that participate in an ILS. Standard ASTM E-691
    (Standard Practice for Conducting an Interlaboratory Study to
    Determine the Precision of a Test Method) recommends applying only
    one graphical technique from Mandel’s k and h statistics \[2\],
    while ISO 5725-2 (Accuracy – trueness and precision – of measurement
    methods and results) recommends, in addition to the graphic
    technique, to use the Cochran and Grubbs.

    The 2 standards mentioned can be consulted in the following
    accesses:

    [ASTM E-691](https://www.astm.org/e0691-21.html)

    [ISO
    5725-2](https://es.scribd.com/document/745647300/NTP-ISO-5725-2-2021-Antecedente-2019)

-   **ANOVA tests**:

    The technique of Analysis of Variance (ANOVA), the effect of the
    laboratory factor over the response can be studied. The variance of
    repeatability and reproducibility can be also estimated when an
    ANOVA random effects model is considered, as shown in ISO 5725-2
    \[1\]. On the other hand, if a fixed effect model is fitted, in
    addition to the F test, multiple comparisons of means can be
    performed with the Tukey Honest Significant Difference (HSD) method.

-   **Functional Data Analysis (FDA)**:

    Functional Data Analysis is a relatively new branch of statistics
    that takes curves as unit of analysis, also surfaces, and volumes
    defined in a continuum (such as time, or frequency’s domain).
    Considering the recent advances in computing science, and the
    increasing amount of data generated by experimental techniques and
    sensors, the FDA has had a great development in recent years. In
    fact, we have many statistical methodologies that have been
    developed and extended to the functional case, such as exploratory
    analysis, regression, classification, analysis of variance, and time
    series.

    In the specific case of ILS, FDA extensions for Mandels’s h and k
    have been proposed and described by Flores, in addition to other
    works where the FDA descriptive analysis had been introduced for ILS
    studies.

<br>

## The R Package ILS

The present ILS library implements and calls some of their routines in
order to perform outlier detection in the framework of the
Interlaboratory Studies. Thus, regarding to ILS with scalar response,
there are some interesting and useful computational tools in R software.

Particularly, the metRology package estimates the uncertainty of the
measurement, and performs the required statistical calculations for
Interlaboratory Studies, whereas multcomp performs analysis of variance
(ANOVA) through F and Tuckey tests.

On the other hand, due to the exponential increasing of FDA available
techniques, there are also a continuously increasing number of R
libraries devoted to this branch of statistics. Among all of them, the
most important and used packages (on which the present proposal is
based) are fda.usc, that implements outlier detection techniques and
functional ANOVA, among other tools for FDA, and the fda. The present
ILS package uses the applications of the before mentioned multcomp and
fda.usc

In summary, the functions incorporated to the ILS package to perform
Interlaboratory Studies are classified under the following scheme:

<br>

## Interlaboratory Studies: Standard Approach

The ILS package provides two groups of functions made to detect outlying
individual results (outlying replicates) and outlying laboratories; for
this purpose, the package offers graphical and analytical procedures
(statistical hypothesis test).

As mentioned in the previous section, among the methodologies used to
evaluate the consistency of laboratory results, we must highlight the
r&R studies, which quantify the variability between laboratories
(reproducibility) and variability between results (repeatability).

-   **Mandel’s h and k statistic**:

    Accordingly with the repeatability and reproducibility concepts,
    this statistics are used in ILS to detect laboratories that provide
    inconsistent results. The h statistic explains the variability
    between the laboratories, that is, estimates the bias, which is the
    difference of the means of each laboratory with respect to the
    global mean, while the k statistic estimates the variability within
    the laboratories, comparing the repeatability corresponding to each
    laboratory.

    The decision rule for detecting whether a laboratory is inconsistent
    is based on the comparison between the value of the h or k statistic
    and the critical value, which is normally calculated with a
    significance level of 0.5% (as recommended by ASTM E-691).

-   **Cochran and Grubbs test**:

    The aim oh these tests is to examine the consistency within a
    laboratory, whereas the Grubbs test is commonly used to examine
    consistency between laboratories. The Grubbs test can also be used
    as a consistency test for the results obtained in a laboratory using
    identical materials. These tests are recommended by ISO 5725-2.

Accordingly, consistency tests and identification of atypical results
must be performed previously to ANOVA analysis. There are two possible
scenarios in which the presence of outliers can be evaluated: the first
is that the results of one laboratory deviates from the others in terms
of precision, that is, when the measurements made by a laboratory
significantly differ with respect to the measurements obtained by other
laboratories. The second scenario is related with the identification of
outliers in a laboratory for a certain level. The statistics and tests
recommended by ISO 5725-2 and ASTM E-691 are described below.

-   **Mandel’s h statistic and Grubbs test**:

If a laboratory is identified as an outlier, after applying the h
statistic and the Grubbs test to different levels within a laboratory,
this is an evidence of the presence of a laboratory high bias (due to a
high systematic error in calibration, or errors in the equations used to
compute the results).

-   **Mandel’s k statistic and Cochran test**:

The Cochran test only evaluates the highest value in a series of
variances. If a laboratory is detected as an outlier, using the k
statistic or with the Cochran test, this indicates that the variance
within the laboratory is high (due to lack of familiarity with the
analytical method, differences of appreciation among operators,
inadequate equipment, equipment in poor state, or careless execution),
in which case the total of results collected by this laboratory should
be rejected and taken out of the study.

The detection of inconsistent laboratories must be repeated until it
stops reporting outliers. However, the consistency tests should be used
with caution, because if this process is carried out in excess, could
lead to false outlier identification.

<br> <br> <br>

This is a basic example which shows you how to solve a common problem:

``` r
library(ILSR6V1)
## basic example code
```

What is special about using `README.Rmd` instead of just `README.md`?
You can include R chunks like so:

``` r
summary(cars)
#>      speed           dist       
#>  Min.   : 4.0   Min.   :  2.00  
#>  1st Qu.:12.0   1st Qu.: 26.00  
#>  Median :15.0   Median : 36.00  
#>  Mean   :15.4   Mean   : 42.98  
#>  3rd Qu.:19.0   3rd Qu.: 56.00  
#>  Max.   :25.0   Max.   :120.00
```

You’ll still need to render `README.Rmd` regularly, to keep `README.md`
up-to-date. `devtools::build_readme()` is handy for this.

You can also embed plots, for example:

<img src="man/figures/README-pressure-1.png" width="100%" />

In that case, don’t forget to commit and push the resulting figure
files, so they display on GitHub and CRAN.
