# Practical 4: Bioinformatic follow-up of GWAS hits
# Objective
Do some bioinformatic follow-up investigation of a GWAS hits using a range of online tools

1. Generate a locuszoom plot to visualise the association signal
2. See if the association is known or novel 
3. Identify interesting annotations using Haploreg
4. Use the ensembl genome browser to explore the region and visualise annotations

# Data
This practical uses results generated in the GWAS session. We will focus on the Chr 16 locus.

Regional association results files have already been extracted and saved here: `E:/Genetic Epidemiology/GWAS/practical/.....`

We will access external resources through websites


# Exercise 1 - Generate locuszoom plots
Go to locuszoom website (http://locuszoom.sph.umich.edu) and click 'Plot Using Your data'

Upload the regional association results (for the relevant chromosome) already prepared for you, e.g. `bmi_clean16.assoc.linear.add`

select `Plink data` format

Specify SNP `rs8050136`

Now, create your plot!<br>
Save this plot to your USB stick as you will need to look at this again during the imputation session.

**_Questions:_**
> (1) Is there much resolution for the signal (many or few SNPs tested/associated, small or large region)?

> (2) Are all associated SNPs in high LD?

> (3) What genes are nearby?


# Exercise 2 - GWAS catalog
See if the association with your SNP (gene or region) is novel or known

Go to the EBI GWAS catalog website: https://www.ebi.ac.uk/gwas/

**_Question:_**
> (4) Is this association with BMI known or novel?


# Exercise 3 - Investigating your signal in Haploreg
We will now test if our signal overlaps with any interesting annotations:

- coding variant
- eQTL results
- functional annotations in ENCODE/RoadMap Epigenomics

Open the Haploreg website: http://www.broadinstitute.org/mammals/haploreg

There are different ways to select your 'credible SNP set'. Here we will just look up everything with r<sup>2</sup>>0.8 with top SNP.

`Enter the SNP name into the box and click submit`

**_Questions:_**
> (5) Are any SNPs coding SNPs? (see last column)

> (6) Are any SNPs known eQTLs? If so for what gene? In what tissue?

> (7) Could you say with any confidence which is the causal variant?

> (8) Could you say with any confidence what the causal gene is?

> (9) Could you say with any confidence which is the tissue of interest?

> (10) There is some evidence that rs1421085 is the causal variant (Claussnitzer et al, 2015, NEJM). Look in more detail at this SNP. Is there anything that stands out for this SNP?

> (11) In the NEJM paper this SNP is described as disrupting ARID5B repressor binding and influencing IRX3 and IRX5 expression. Why is that not seen here? 
<br>
<br>
<br>

# Exercise 4 - Chromatin interaction

Go to http://www.yuelab.org

Navigate to 3D genome browser, click on the Hi-C tab.<br>
Select IMR90 as the tissue type and search by RSID: `rs8050136`. <br>
Zoom out once and examine the region that is observed to have chromatin interaction with the region containing the SNP. This was how the Claussnitzer paper selected which genes to follow-up in an eQTL experiment.

# Exercise 5 - Mouse knockouts
When you have a gene of interest you can look to see if this gene has been knocked out in mice, and what phenotypes these mice have.

Go to http://www.informatics.jax.org

Search for `FTO` and `IRX5` mouse knockouts.<br>
What phenotypes do these mice display?

**_Questions:_**
> (13) Can you think what problems there might be with using mouse knockout evidence to determine the causal gene?









