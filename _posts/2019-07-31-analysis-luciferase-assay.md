---
layout: single
title:  "Statistical analysis of Luciferase Assays"
date:   2019-07-31
desc: "Simple guide for the analysis of the statistical analysis of Luciferase reporter assays"
keywords: "statistics,analysis,diy,code,test,statistical,simple,reporter"
categories: [biology,statistics]
tags: [biology]
icon: icon-dna
---

# Motivation

The Luciferase reporter assay is used to measure the repressional influence of a regulatory element. A common example is the assessment of microRNA-mediated post-transcriptional regulation of 3'untranslated regions (3'UTRs). It works by transfecting a prepared luciferase plasmid, containing the coding sequence for a luciferase protein followed by the to be tested 3'UTR, along with a to be tested miRNA, into a suitable cell line. After some time, the cells are harvested and lysed in order to assess the amount of produced luciferase using a luminescence detector.
In order to normalize for minor pipetting mistakes and other potential per-well deviations, dual luciferase reporter assays can be used, which enable the measurement of two distinct luciferase proteins, one of them without a regulatory element to be used as a normalizer. 

Although analysis of the data, produced in such an experiment, is fairly simple, I failed in finding easily accessible resources on the web on this matter, which is what motivated me to share my current approach. 

This being said, please note, that my statistical knowledge is limited, so take this guide with a grain of salt. I have to rely on the information I got from the references I was using and appreciate any comment on the matter. 

The calculations here are simple enough to perform them in a spreadsheet (e.g. Excel), or in the programming language/notebook of your choice.

# The data

As a rule of thumb, at least a biological triplicate is required in order to gain enough statistical power. Furthermore, each biological replicate is performed in three technical replicates. For a single tested combination (miRNA and regulatory sequence (e.g. 3'UTR)), this results in 9 measurements. Of note, clear single outliers in a given triplicate can be deleted.

## Normalization

Dual reporter assays require an initial normalization step, which is skipped for single reporter assays.

In order to perform normalization the reporter fluorophore intensity is simply divided by the normalizing fluorophore. To provide an exmaple, for the psiCHECK(TM) 2 vector this would be:

$$I_normalized = \frac{I_Renilla}{I_Firefly}$$

## Averaging technical replicates

Following [^1], technical replicates can be simply averaged into a single data point, while treating the mean as a single biological replicate.

It is important however to always make manually sure that the variation is not too high between single data points. In case of one deviating data point it may be feasible to drop a single technical replicate and continue with the other two. Generally high variation should motivate to redo the experiment.

# Statistical testing

A bunch of statistical tests exist and have been discussed in [blogs](https://blog.minitab.com/blog/adventures-in-statistics-2/choosing-between-a-nonparametric-test-and-a-parametric-test) and the scientific literature[^1].

In our case, as each of our sample measurements represents an average of a high number of cells, it is fair to say that our three biological replicates come from a normal distribution, which enables us to do a two sample unpaired t-test [^1][^2]. In a simple experiment, where we test a number of microRNAs on a 3'UTR, we can compare pairs of microRNAs (as for example a negative control microRNA and a to be tested microRNA) as follows

$$t_{statistics}, p_{two-tailed} = t_{unpaired}([c_1, c_2, c_3], [x_1, x_2, x_3])$$

Given the means $$c_1, c_2, c_3, x_1, x_2, x_3$$ calculated from the technical replicates for independent experiments. $$c\_i$$ corresponds to the negative control microRNA, $$x\_i$$ to the tested microRNA. If the retrieved p-value is small, the null hypothesis (which in this case states that the two microRNAs have different potential to repress the tested 3'UTR) can be rejected. Usually, a p-value of 0.05 is taken, however the use of p-values to accept or reject hypothesis is [under debate](https://www.nature.com/news/scientific-method-statistical-errors-1.14700). Furthermore, it might be necessary to account for multiple testing, if the number of tests becomes large [^3].

When comparing more than 2 groups (e.g. to test whether a set of distinct microRNAs all exhibit the same repression or whether their observed repressional effects are different), it is advisable to use an ANOVA test, which accounts for the multiple testing issue [^4].

# References

[^1]: Fay D.S. and Gerow K. A biologist's guide to statistical thinking and analysis (July 9, 2013), WormBook, ed. The C. elegans Research Community, WormBook, doi/10.1895/wormbook.1.159.1, http://www.wormbook.org
[^2]: Student. “The Probable Error of a Mean.” Biometrika, vol. 6, no. 1, 1908, pp. 1–25. JSTOR, www.jstor.org/stable/2331554. Accessed 22 Feb. 2020.
[^3]: Noble, William S. How does multiple testing correction work?. Nature biotechnology 27.12 (2009): 1135-1137.
[^4]: Kim, Hae-Young. Analysis of variance (ANOVA) comparing means of more than two groups. Restorative dentistry & endodontics 39.1 (2014): 74-77.

