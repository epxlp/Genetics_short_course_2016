# Practical: Bioinformatic follow-up of GWAS hits
# Answers

Here I give answers only for the rs571312 locus. 

> (1) Is there much resolution for the signal (many or few SNPs, small or large region)?

There is a clump of SNPs highly associated spanning about 200kb. This includes 9 SNPs very strongly associated.

> (2) Are all associated SNPs in high LD?

No, there seems to be a second clump of SNPs with p~10-10 in low LD (r2<0.2) flanking the MC4R gene. 
This might be a second independent signal and this would need testing formally using conditional analysis.

> (3) What genes are nearby? (You might also want to look these up on genecards)

MC4R and PMAIP1 flank the association signal.


#Exercise 2 - GWAS catalog

> (4) Is this association with BMI known or novel?

This association is known. This SNP has been associated with BMI in a number of GWAS studies. 

#Exercise 3 - Investigating your signal in Haploreg

> (5) Are any SNPs coding SNPs? (see last column)

No

> (6) Are any SNPs known eQTLs? If so for what gene? In what tissue?

No

> (7) Could you say with any confidence which is the causal variant?

No - Some SNPs are annotated as potential enhancers or in regions of open chromatin in various tissue types. 
But none are annotated as eQTLs.
No SNPs stand out as having more evidence than others for being causal.

> (8) Could you say with any confidence which is the causal gene?

Though MC4R is the closeest gene, there is no evidence that this gene is the causal gene.
The best evidence for this is either a coding or eQTL SNP.

> (9) Could you say with any confidence which is the tissue of interest?

No - SNPs are in open chromatin or enhancer regions for a range of tissues including blood, skin, ESCs. 
But until the causal variant and/or gene is identified the relevance of these annotations is not known.


> (10) How many have histone marks indicative of a promoter? an enhancer? In a region of open chromatin? Have proteins bound?

None are annotated as promoters, 8 are annotated as enhancers, 6 are in regions of open chromatin, 1 has GATA2 protein bound. 

> (11) Which SNP alters the most motifs? Which motif is most affected?

rs523288 alters 11 motifs. Nkx6-1_1 has a large difference in LOD for binding affinity between reference (13.2) and alternative (1.2).


#Summary
For your region:

> Is the association novel?

No

> What are the nearby genes?

MC4R and PMAIP1

> Is there any evidence for a particular .....

> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; causal variant?

No

>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; causal gene?

No

> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; affected tissue?

No

> What additional investigations/validation might you want to do?

There's lots of things you could do:

Test for enrichment of annotations in particular tissue types over all hits.

Do pathway analysis

Look at more specific eQTL databases

Look up genes in mouse knockout databases

Do laboratory over- and under-expression experiments.

See DOI: 10.1056/NEJMoa1502214 for a thorough investigation of the FTO association signal.
