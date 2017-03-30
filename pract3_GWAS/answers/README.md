# Practical: Genome-wide association study of BMI in Plink
# Answers

> (1) How many individuals are there?

```
[user@newblue4 data]$ wc -l geno_unclean.fam
8237 geno_unclean.fam
```

8237 individuals

> (2) How many SNPs are there?

```
[user@newblue4 data]$ wc -l geno_unclean.bim
463080 geno_unclean.bim
```

463,080 SNPs

> (3) How can we tell there is a problem with this GWAS?

![alt text](https://github.com/epxlp/Genetics_short_course_2016/blob/master/pract3_GWAS/answers/bmi_unclean_qqplot.png)

The QQ plot looks inflated and the lambda (genomic inflation) is 1.09 - suggesting some population stratification problems.

![alt text](https://github.com/epxlp/Genetics_short_course_2016/blob/master/pract3_GWAS/answers/bmi_unclean_manhattan.png)

There are some suspiciously good hits on the Manhattan plot.

> (4) For each of the parameters below, which SNPs or individuals do you think should be removed?

Minor allele frequency <0.01

Hardy Weinberg p-value <1x10-6

SNP missingness >0.05

Individual missingness >0.05


> (5) How many genome-wide significant (p<5x10-8) signals do you have?

62 SNPs meet the p<5x10-8 threshold

> (6) Are these likely to all be independent?

Many are nearby SNPs and likely to be in LD, so there is probably only 6 independent associations. 
In a real GWAS you would run conditional analysis to test for secondary signals at each locus.

> (7) What is the top signal?

rs571312. On chromosome 18 at position 57839769.

> (8) How might we go about confirming this finding?

In GWAS we normally seek replication in an independent study. 
Because we only test a few SNPs in replication, a significant result is achieved with a higher p-value.
We can also use other data resources to check the plausibility of the signals (see next session)
