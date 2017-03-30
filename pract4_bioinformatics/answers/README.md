# Practical 4: Bioinformatic follow-up of GWAS hits
# Answers

# Exercise 1 - Locuszoom

> (1) Is there much resolution for the signal (many or few SNPs, small or large region)?

There are several SNPs highly associated spanning about 100kb.

> (2) Are all associated SNPs in high LD?

No, some SNPs in low LD (r2<0.2) are also associated (dark blue points). <br>
This might be a second independent signal or might indicate that rs8050136 is not the causal SNP.

> (3) What genes are nearby? (You might also want to look these up on genecards)

The signal falls within FTO. There are other genes in the region.


# Exercise 2 - GWAS catalog

> (4) Is this association with BMI known or novel?

This association is known. This SNP has been associated with BMI/adiposity in a number of GWAS studies. <br>
It has also been associated with other traits: menarche and Type 2 Diabetes.

# Exercise 3 - Investigating your signal in Haploreg

> (5) Are any SNPs coding SNPs? (see last column)

No, all are intronic.

> (6) Are any SNPs known eQTLs? If so for what gene? In what tissue?

No

> (7) Could you say with any confidence which is the causal variant?

No - Some SNPs are annotated as potential promoters/enhancers or in regions of open chromatin in various tissue types. 
But none are annotated as eQTLs.
No SNPs stand out as having more evidence than others for being causal.

> (8) Could you say with any confidence which is the causal gene?

The signal falls in anintron of FTO, but there is no evidence that this gene is the causal gene.
The best evidence for this is either a coding or eQTL SNP.

> (9) Could you say with any confidence which is the tissue of interest?

No - SNPs are in open chromatin or enhancer regions for a range of tissues including blood, fat, lung. 
But until the causal variant and/or gene is identified the relevance of these annotations is not known.

> (10) There is some evidence that rs1421085 is the causal variant (Claussnitzer et al, 2015, NEJM). Look in more detail at this SNP. Is there anything that stands out for this SNP?

Not really. Though you could weave an interesting story if you wished.

> (11) In the NEJM paper this SNP is described as disrupting ARID5B repressor binding and influencing IRX3 and IRX5 expression. Why is that not seen here?

Haploreg only catalogues certain experiments in certain tissue types. It probably misses a lot of important data and so should be used bearing this in mind.


# Exercise 5 - Mouse knockouts

> (13) Can you think what problems there might be with using mouse knockout evidence to determine the causal gene?

Mouse and human genomes are different, so we can't be sure that a mouse knockout is equivalent to a human knockout.<br>
The other problem with knocking out an entire gene, is that it likely removes not only the gene but lots of important regulatory DNA for other nearby genes. So a knockout showing a certain phenotype is no guarentee that the protein product of that gene is the causal effect.

