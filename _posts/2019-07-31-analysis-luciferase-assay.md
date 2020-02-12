* 
---
layout: single
title:  "Statistical analysis of Luciferase Assays"
date:   2019-07-31
desc: "Simple guide for the analysis of the statistical analysis of Luciferase reporter assays"
keywords: "statistics,analysis,diy,code,test,statistical,simple,reporter"
categories: [biology,statistics]
tags: [biology]
icon: icon-default
---
# Motivation

The Luciferase reporter assay is commonly used to report 
dual reporter
Analysis of the data is fairly simple, however little support is provided only.

Please note that my statistical knowledge is limited so take this guide with a grain of salt.

The calculations here are simple enough to perform them in a spreadsheet (e.g. Excel), or in your

# The data

Usually at least a biological triplicate is required. Furthermore, each biological replicate is performed in three technical replicates....

## Normalization

In dual-reporter assays, two independent fluorophores are being expressed and their intensity is measured. One is regulated (by the regulator of interest), the other one is not and can be used as a normalizing factor to account for variances in reaction efficiencies between different wells (e.g. caused by pipetting). 

In order to perform normalization the reporter fluorophore intensity is simply divided by the normalizing fluorophore. For the psiCHECK(TM) 2 vector (just to give an example) this would be:

$$I_normalized = \frac{I_Renilla}{I_Firefly}$$

## Averaging technical replicates

"As such, technical replicates should be averaged, and this value treated as a single data point."

[@fay13_biolog_guide_to_statis_think_analy]

# Statistical testing

A bunch of statistical tests exist and have been discussed in [blogs](https://blog.minitab.com/blog/adventures-in-statistics-2/choosing-between-a-nonparametric-test-and-a-parametric-test) and the [scientific literature](http://www.wormbook.org/chapters/www_statisticalanalysis/statisticalanalysis.html) [@fay13_biolog_guide_to_statis_think_analy].

As each of our samples contains an average of a high number of cells, it is fair to say that our three technical replicates come from a normal distribution which enables us to do an (unpaired) two sample t test (logic borrowed from the wormbook).

The ANOVA test is also widely used in Biology, however it boils down to a t-test, as described by (Gosset 1908) and described on [Wikipedia/ANOVA](https://en.wikipedia.org/wiki/One-way_analysis_of_variance).

