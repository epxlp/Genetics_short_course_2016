# Practical: Genome-wide association study of BMI in Plink
# Objectives
1. Clean a dataset
2. Conduct a GWAS analysis
3. Produce Manhattan & QQ plots
4. Interpret GWAS results

This practical uses simulated data. But the scenario is as follows:

Data has been collected as part of a local population cohort, Bristol Obesity Population Study (BOPS), which recruited secondary school children (aged between 11 and 18) from around Bristol. Questionnaires were completed and several measures (including BMI) were taken from participants. Blood was taken and DNA extracted for genotyping using the custom 'NiftyBOPs' array. Individuals were followed up to see if they suffered from certain medical conditions (including hypertension), later in life.

(Some names may have been invented)


#Log In
Log into bluecrystal using PuTTY.

Run the following command to access a compute node:
`qsub -I -q teaching -l nodes=1:ppn=1,walltime=02:00:00`

#Data
Data for this practical is available in `pract3_GWAS/data`

Scripts (files containing commands) should be saved in `pract3_GWAS/scripts`

You should save your output to `pract3_GWAS/output`

If you get really stuck, example scripts and ready-made output are available in `pract3_GWAS/results` (no peaking unless you have to!)

#Loading Plink
If you are starting a new PuTTY session you may need reload plink.
`module load apps/plink2`

#Exercise 1 - Unclean GWAS
First, we will run a GWAS without doing any cleaning to the dataset.

Take a look at the data `data/geno_unclean.bim` & `.fam`

**_Questions:_**
> (1) How many individuals are there?

> (2) How many SNPs are there?

Run the GWAS (without QC) `./unclean_gwas.sh` – results are in the `output/` directory

Run the script to generate the plots using R `./unclean_gwas_graphs.sh`

Open WINSCP (in windows) and open the graphs you’ve just created.

**_Question:_**
> (3) How can we tell there is a problem with this GWAS?

#Exercise 2 - Cleaning the GWAS data
There are many steps to a good QC procedure (see Weale 2010. Quality control for genome-wide association studies. Methods in Molecular Biology 628:341-372). Here we assume that related individuals and non-white Europeans have already been removed and proceed with the final steps of the QC.

**_Question:_**
> (4) For each of the parameters below, which SNPs or individuals do you think should be removed?

>     Minor allele frequency?

>     Hardy Weinberg p-value?

>     SNP missingness?

>     Individual missingness?

Now look at the `qc.sh` script to see the suggested exclusions for this dataset. Run the `qc.sh` script to generate new ‘cleaned’ data files `geno_qc.bed` `.bim` `.fam`


#Exercise 3 - Running the clean GWAS
We will now run the final ‘clean’ GWAS for BMI.

To do this, copy the `unclean_gwas.sh` to a new script using `cp unclean_gwas.sh {newfilename}`

Edit the file to use the new ‘clean’ GWAS data, remove the covar-name option so it includes all principle component covariates in the model and output to a new file named `bmi_clean`

Run the script. 

You’ll notice at this point that the script is going to take a long time to run! So once you get bored waiting, hit `ctrl-c` to cancel and go to the `results/` directory where you can see the pre-made results file.

Go back to `./scripts`

Copy the `unclean_gwas_graphs.sh` file to a new file named `clean_gwas_graphs.sh`. Edit to use the new clean results and output to new files. Run this new script with `./clean_gwas_graphs.sh`

Open WINSCP (in windows) and open the graphs you’ve just created.

Look at the results file using the following commands:

`head bmi_clean.assoc.linear.add`

`awk '$9<0.00000005' bmi_clean.assoc.linear.add | wc -l`

`awk '{if(NR==1 || $9<0.00000005) print $0}' bmi_clean.assoc.linear.add` - save the output of this command for the next practical

`grep -v NA bmi_clean.assoc.linear.add | sort -g -k 9 | head`

**_Questions:_**
> (5) How many individuals in the final analysis?

> (6) How many genome-wide significant (p<5x10-8) signals do you have?

> (7) Are these likely to all be independent?

> (8) What is the top signal?

> (9) How might we go about confirming this finding?
