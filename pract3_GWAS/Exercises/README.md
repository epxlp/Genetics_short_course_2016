# Practical 3: Genome-wide association study of BMI in Plink
# Objectives
1. Clean a dataset
2. Conduct a GWAS analysis
3. Produce Manhattan & QQ plots
4. Interpret GWAS results

This practical uses simulated data. But the scenario is as follows:

Data has been collected as part of a local population cohort, Bristol Obesity Population Study (BOPS), which recruited secondary school children (aged between 11 and 18) from around Bristol. Questionnaires were completed and several measures (including BMI) were taken by a nurse during a school health checkup. Blood was taken and DNA extracted for genotyping using the custom 'NiftyBOPs' array. Individuals of non-European ancestry were excluded and principal components were calcuated to estimate any remaining population structure.

(Some names may have been invented)


# Log In
Log into bluecrystal using PuTTY.

Run the following command to access a compute node:<br>
`qsub -I -q teaching -l nodes=1:ppn=1,walltime=02:00:00`

# Data
Data and scripts for this practical are available in
`/panfs/panasas01/sscm/shortcourse/genetic.epidemiology/pract3_GWAS/`

For ease, make a copy of this directory in your home folder (this may take a few minutes):

`cp -r /panfs/panasas01/sscm/shortcourse/genetic.epidemiology/pract3_GWAS ~/`

Scripts (files containing commands) should be saved in `~/pract3_GWAS/scripts/`

You should save your output to `~/pract3_GWAS/output/`

If you get really stuck, example scripts and ready-made output are available in `~/pract3_GWAS/results/` (no peaking unless you have to!)

# Loading Plink
Load Plink
`module load apps/plink2`

# Exercise 1 - Unclean GWAS
First, we will run a GWAS of BMI without doing any cleaning to the dataset.

Take a look at the genetic data `data/geno_unclean.bim` & `.fam`<br>
Take a look at the phenotype data `data/phen.txt`

**_Questions:_**
> (1) How many individuals are there?

> (2) How many SNPs are there?

We will run the first GWAS using a provided script `~/pract3_GWAS/scripts/unclean_gwas.sh`. You should look at this script to see what it contains, so you understand how to make your own.<br>
Run the GWAS of BMI (without QC) using `./unclean_gwas.sh` or `~/pract3_GWAS/scripts/unclean_gwas.sh`<br>
Results will be in the `output/` directory

Run the script to generate the plots using R `./unclean_gwas_graphs.sh`

Open WINSCP (in windows) and open the graphs you’ve just created (you might need to right click to open)

**_Question:_**
> (3) How can we tell there is a problem with this GWAS?

# Exercise 2 - Cleaning the GWAS data
There are many steps to a good QC procedure (see Weale 2010. Quality control for genome-wide association studies. Methods in Molecular Biology 628:341-372). Here we assume that related individuals and non-white Europeans have already been removed and proceed with the final steps of the QC.

**_Question:_**
> (4) For each of the parameters below, which SNPs or individuals do you think should be removed?

>     Minor allele frequency?
>     Hardy Weinberg p-value?
>     SNP missingness?
>     Individual missingness?

Now look at the `qc.sh` script to see the suggested exclusions for this dataset. Run the `qc.sh` script to generate new ‘cleaned’ data files `geno_qc.bed` `.bim` `.fam`


# Exercise 3 - Running the clean GWAS
We will now run the final ‘clean’ GWAS for BMI. This requires you to edit some scripts.

To do this, copy the `unclean_gwas.sh` to a new script using `cp unclean_gwas.sh {newfilename}`

Edit the file (using pico) to use the new ‘clean’ GWAS data, remove the covar-name option so it includes all principle component covariates in the model and output to a new file named `bmi_clean`

Run the script ---- This should now be running the clean GWAS

You’ll notice at this point that the script is going to take a long time to run! So once you get bored waiting, hit `ctrl-c` to cancel and go to the `results/` directory where you can see the pre-made results file `bmi_clean.assoc.linear.add`.

Now we will make some plots......

Go back to `./scripts`

Copy the `unclean_gwas_graphs.sh` file to a new file named `clean_gwas_graphs.sh`. <br>
Edit (using pico) to use the new clean results and output to new files. Run this new script with `./clean_gwas_graphs.sh`

Open WINSCP (in windows) and open the graphs you’ve just created.

Look at the results file using the following commands:

`head bmi_clean.assoc.linear.add`

`awk '$9<0.00000005' bmi_clean.assoc.linear.add | wc -l`

`awk '{if(NR==1 || $9<0.00000005) print $0}' bmi_clean.assoc.linear.add`

`grep -v NA bmi_clean.assoc.linear.add | sort -g -k 9 | head`

**_Questions:_**
> (5) How many individuals in the final analysis?

> (6) How many genome-wide significant (p<5x10-8) signals do you have?

> (7) Are these likely to all be independent?

> (8) What is the top signal?

> (9) How might we go about confirming this finding?

<br>
<br>

**_Task_**

Complete the results sheet on the next page. Include the top SNP at each locus. 

# Exercise 4 - Generating a Locus Zoom Plot
We will now generate a locus zoom plot of the signal on chromosome 16.
You will find the file `bmi_clean16.assoc.linear.add` on your USB stick.
This file was generated by extracting only the chr16 results from `bmi_clean.assoc.linear.add`

Go to the locuszoom website (`http://locuszoom.org/`) and click 'Plot your data' 'Single plot'.

Upload the regional association results already prepared for you, `bmi_clean16.assoc.linear.add`

Select `Plink data` format

Specify SNP `rs8050136`

Now, create your plot!

Save this plot to your USB stick as you will need to look at this again during the imputation session.

**_Questions:_**
> (10) Are all associated SNPs in high LD?

> (11) What genes are nearby?

# SNPTEST Info
```
Another commonly used GWAS softwars is SNPTEST (mathgen.stats.ox.ac.uk/genetics_software/snptest/snptest.html)

INPUT files: .gen (or .bgen)
             .sample
             
CAUTION:
There are no IDs in the file contianing the genetic data (.gen / .bgen), so the sample file must be kept in the correct order (i.e. the first row in the .sample file is the individual whose genetic data is displayed in the first three columns of the .gen file (as three probabilities). Typically to run a GWAS on your trait you would take the generic .sample file, merge in your phenotype (and covariates) keeping the same row order and output as a new .sample file for analysis.
```
