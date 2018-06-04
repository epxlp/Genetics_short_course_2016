# Practical 2: Population Genetics & Association
# Answers

# Exercise 1 - Estimating minor allele frequencies

> (1) What are these files, what does each of them contain?

```
user@newblue4 data]$ less ~/pract2_PopgenAssoc/output/chr16_maf.log
```

chr16_maf.log - A Plink log file describing what was done

```
user@newblue4 data]$ less ~/pract2_PopgenAssoc/output/chr16_maf.frq
```

chr16_maf.frq - A results file containing the Minor Allele Frquencies, one line per SNP.


> (2) What is the minor allele and the minor allele frequency for rs758033? (hint: A1 is the minor allele)

```
user@newblue4 data]$ head -1 ~/pract2_PopgenAssoc/output/chr16_maf.frq
 CHR         SNP   A1   A2          MAF  NCHROBS
```
```
user@newblue4 data]$ grep rs758033 ~/pract2_PopgenAssoc/output/chr16_maf.frq
  16    rs758033    T    G       0.2463    16474
```

T 0.25

# Exercise 2 - Hardy Weinberg Equilbrium

```
[user@newblue4 data]$ plink --bfile ~/pract2_PopgenAssoc/data/chr16 --hardy --out ~/pract2_PopgenAssoc/output/chr16_hardy
```

> (3) Is the SNP rs758033 In HWE?

```
user@newblue4 data]$ head -1 ~/pract2_PopgenAssoc/output/chr16_hardy.hwe
 CHR         SNP     TEST   A1   A2                 GENO   O(HET)   E(HET)            P
```
```
user@newblue4 data]$ grep rs758033 ~/pract2_PopgenAssoc/output/chr16_hardy.hwe
 16    rs758033  ALL(NP)    T    G        536/2985/4716   0.3624   0.3712      0.03256
```

The p-value for the test in 0.03256. This is below 0.05, but given the number of tests this is not significant.

The null hypothesis is no difference between observed and expected (under HWE). We cannot reject the null hypothesis, so there is no evidence that rs758033 is not in HWE.

# Exercise 3 - Association testing with Plink
```
[user@newblue4 data]$ grep rs3751812 chr16.bim
16      rs3751812       0       53818460        T       G
```

```
[user@newblue4 data]$ grep rs3751812 ~/pract2_PopgenAssoc/output/chr16_maf.frq
  16   rs3751812    T    G       0.3937    16474
```

```
[user@newblue4 data]$ grep rs3751812 ~/pract2_PopgenAssoc/output/chr16_hardy.hwe
  16   rs3751812  ALL(NP)    T    G       1268/3949/3020   0.4794   0.4774       0.7119
```

> (4) What are the two alleles at this SNP? What is the minor allele frequency? Is this SNP in HWE?

T/G MAF(T)=0.39 HWE(P)=0.71 - The SNP is in HWE.

> (5) Have a look at these files and write down the column names for BMI, sex and age (case-sensitive). You will need to know these for the next command.

```
[epxlp@newblue4 data]$ head phen.txt
FID IID BMI DBP SBP CRP HT
id1 id1 31.8664742886873 87.2331807479429 152.290193244483 1.44468000003555 2
id2 id2 35.4253325607032 86.059532896277 143.082692573686 3.75456412209453 2
....
```

```
[epxlp@newblue4 data]$ head covs.txt
FID IID PC1 PC2 PC3 PC4 PC5 PC6 PC7 PC8 PC9 PC10 age sex smoking
id1 id1 0.0155804 -0.00641899 0.00453887 0.00694199 -0.000623769 0.0108906 -0.0129265 -0.0120965 0.0176676 -0.0026872 14.6667 2 1
id2 id2 0.0126108 -0.0042825 0.00125359 0.00983088 0.0286569 0.000137101 -0.012276 -0.0104017 0.00382211 0.00892457 15 2 0
....
```

phen.txt: BMI

covs.txt: sex, age

Run the analysis:
```
plink \
--bfile \
~/pract2_PopgenAssoc/data/chr16 \
--snp rs3751812 \
--linear \
–-ci 0.95 \
--pheno ~/pract2_PopgenAssoc/data/phen.txt \
--pheno-name BMI \
--covar ~/pract2_PopgenAssoc/data/covs.txt \
--covar-name sex,age \
--out ~/pract2_PopgenAssoc/output/rs3751812_BMI
```

```
./assoc.sh
```


> (6) What are the results?

```
less ~/pract2_PopgenAssoc/output/rs3751812_BMI.assoc.linear
CHR         SNP         BP   A1       TEST    NMISS       BETA       SE      L95      U95         STAT            P
  16   rs3751812   53818460    T        ADD     8237     0.6503  0.08928   0.4753   0.8253        7.284    3.545e-13
  16   rs3751812   53818460    T        age     8237  -0.007949  0.02049 -0.04812  0.03222      -0.3879       0.6981
  16   rs3751812   53818460    T        sex     8237      1.377   0.1232    1.136    1.618        11.18    8.122e-29
```

BETA = 0.6503

95% CI = 0.4753 - 0.8253

PVALUE = 3.5x10-13

> (7) Write a sentence that fully describes this result (think about which allele is the BMI increasing allele).

rs3751812 is associated with BMI (p=3.5x10-13), with a 0.65kg/m2 increase in BMI per T allele.
