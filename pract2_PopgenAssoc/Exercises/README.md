# Practical 2: Population Genetics & Association
# Objectives
We will use the Plink software (help here: www.cog-genomics.org/plink2) to:
1. Calculate some simple population genetic parameters
2. Carry out a single SNP association

# Log In
Log into bluecrystal using PuTTY.

EXTRA STEP: Run the following command to access a compute node (required for all but the smalles of tasks):

`qsub -I -q teaching -l nodes=1:ppn=1,walltime=02:00:00`


# Data
Data and scripts for this practical are available in `/panfs/panasas01/sscm/shortcourse/genetic.epidemiology/pract2_PopgenAssoc/`

For ease, make a copy of this directory in your home folder:

`cp -r /panfs/panasas01/sscm/shortcourse/genetic.epidemiology/pract2_PopgenAssoc ~/`

Now navigate to your home directory and see what is in the `pract2_PopgenAssoc/` directory.

Scripts (files containing commands) will be saved in `~/pract2_PopgenAssoc/data/scripts/`

You should save your output to `~/pract2_PopgenAssoc/output/`.

If you get really stuck, example scripts and ready-made output are available in `~/pract2_PopgenAssoc/results/` (no peaking unless you have to!)

# Loading Plink
Load Plink by typing `module load apps/plink2`

Now type `plink` and you should see something happen

# Population Genetics

We are going to estimate some population genetic parameters.

These commands are written below with the full paths, you can instead use relative paths if you know where you are (e.g. `./` is the current directory & `../` is the directory above the current directory). This can save a bit on typing.


# Exercise 1 - Estimating minor allele frequencies
Type:
`plink --bfile ~/pract2_PopgenAssoc/data/chr16 --freq --out ~/pract2_PopgenAssoc/output/chr16_maf`

Once this has run navigate to the correct directory and see what files have been created. 


**_Questions:_**
> (1) What are these files, what does each of them contain?

> (2) What is the minor allele and the minor allele frequency for rs758033? (hint: A1 is the minor allele)

# Exercise 2 - Hardy Weinberg Equilbrium
The plink command for estimating Hardy Weinberg Statistics is `--hardy`. Run a plink job for this.


**_Question:_**
> (3) Is the SNP rs758033 In HWE?

There are many other summary statistics that Plink can estimate. If you have time have a look at the Plink webpage http://pngu.mgh.harvard.edu/~purcell/plink/summary.shtml and try some others out.

# Exercise 3 - Association testing with Plink
Here we will just do a single SNP association with BMI. 

This will be a simple linear regression with BMI as the outcome (dependent variable), rs3751812 as the SNP exposure of interest (independent variable) and sex and age as covariates.  

Because our dataset contains thousands of SNPs we will use `--snp` to define the single SNP of interest. 

First use `grep` to have a look at the SNP of interest in the `.bim`, `.freq` and `.hwe` files.


**_Question:_**
> (4) What are the two alleles at this SNP? What is the minor allele frequency? Is this SNP in HWE?

Until now we have not used any phenotype data. The phenotype data is stored in `phen.txt` and the covariates in `covs.txt`


**_Question:_**
> (5) Have a look at these files and write down the column names for BMI, sex and age (case-sensitive). You will need to know these for the next command.
<br/>

Use the following command to run the association. Some parts have been left blank for you to fill in. 

Instead of typing into the command line you will find this script here: 

`~/pract2_PopgenAssoc/scripts/assoc.sh` 

Open the script in a text editor by typing `nano assoc.sh` and when you have made your changes save (by typing `ctrl-X` then `y`).
Then run the updated script by typing `./assoc.sh`

The script is reproduced here (NB - the backslash enables you to lay the command out over multiple lines):


```
plink \
--bfile ~/pract2_PopgenAssoc/data/chr16 \
--snp rs3751812 \
--linear \
–-ci 0.95 \
--pheno ~/pract2_PopgenAssoc/data/phen.txt \
--pheno-name ________ \
--covar ~/pract2_PopgenAssoc/data/covs.txt \
--covar-name _________ \
--out ~/pract2_PopgenAssoc/output/rs3751812_BMI
```


**_Questions:_**
> (6) What are the results?

>   BETA

>   95% CI

>   PVALUE

> (7) Write a sentence that fully describes this result (think about which allele is the BMI increasing allele).


