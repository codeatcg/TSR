# TSR: Selection of Trait Specific and Representative markers

## Description:

With the development of resequencing and genotype imputation methods large amounts of SNPs are available. Many of the SNPs are thought to be redundant. TSR was developed mainly to select appropriate SNPs to improve the genome prediction and both genotype and dosage are supported. Several methods can be chose: minimal allele frequency, linkage disequilibrium, cluster, average distance and p-value from genome wide association studies. The program also has other functions. It can be used to estimate the linkage disequilibrium decay. It can also be use to estimate the variance of SNP effects and build weighted genome relationship.

## Version:

The program was written by C++ and compiled using gcc 4.4.7 on a 64-bit Linux version. 
Current version: TSR_float_v0.1.0 (genotypes are stored in a float and compatible with software MGP_float)

## Command and options:

**vcf2tag**         &ensp; &ensp; &ensp; &ensp; TSR vcf2tag [options]

Convert genotypes in VCF format to binary format. Binary genotypes are used to build genome relationship and get appropriate SNPs to improve the genome prediction and genome wide association.

\//Convert Vcf to Binary Genotype:	

    --vcf       <FILE>   input vcf file
    --gType     <STR>    **genotype or dosage
    --outGen    <FILE>   output binary genotype
    --outPos    <FILE>   **output coordinate file
	
\//Prune SNPs:

    --inHeader  <FILE>   **vcf file or vcf header file
    --inGen     <FILE>   **input binary genotype
    --inPos     <FILE>   input coordinate file		
    --outGen    <FILE>   output binary genotype
    --outPos    <FILE>   **output coordinate file		
    --win       <INT>    window size, by default:50000
    --overlap   <INT>    overlap size, by default:5000
    --value     <FLOAT>  relation between SNPs,by default:0.9		
    --verbose            output detailed information for each window
    --cluster            SNPs pruned by cluster
    --ldprune            SNPs will be removed if they are in tight linkage with any others, similar to plink
    --unif               SNPs pruned by average distance
    --mafwin             SNPs pruned by minimal allele frequency in a window
		
\//Build Relationship:

     --inHeader  <FILE>   **vcf file or vcf header file
     --inGen     <FILE>   **input binary genotype
     --gType     <STR>    **genotype or dosage
     --addMethod <INT>    1 (formula according to Vanraden) or 2 (similar to GCTA)
     --bin2kin            build genome relationship
     --outKin    <FILE>   output binary kinship
     --outTxt    <FILE>   output kinship in text
     --part               genotype file is partial and the output kinship file need to be merged


**ld**         &ensp; &ensp; &ensp; &ensp; TSR ld [options]

Linkage disequilibrium decay was estimated by the correlation coefficients between markers, which was thought to be comparable with the method based on linkage phase. All SNP pairs are evaluated, but it’s optional that just using part of pairs if maker densities are high.

    --pos        <FILE>   position file
    --genotype   <FILE>   input binary genotype file
    --inHeader   <FILE>   vcf file or vcf header file
    --out        <FILE>   output file
    --win        <INT>    window size, by default: 500000
    --thin                chromosome segments are independent, without this parameter all SNP pairs with distance less than the window will be considered



**wkin**         &ensp; &ensp; &ensp; &ensp; TSR wkin [options]

Estimated breeding value (EBV), relationship and binary genotype are needed to build weighted genome relationship. It’s similar to iteration ssGBLUP but the analysis can be parallelized by chromosomes or chromosome segments.

    --inKin        <FILE>   input binary kinship
    --inEbv        <FILE>   input ebv file
    --inGeno       <FILE>   input binary genotype file
    --posFile      <FILE>   input position file (match the binary genotype file)
    --outKbin      <FILE>   output weighted binary kinship
    --outKtxt      <FILE>   output weighted kinship in text

    --varSnp       <FILE>   output variance of SNPs effects
    --varWin       <FILE>   output genetic variance explained by SNPs in a window
    --winMet       <INT>    method to calculate variance explained by SNPs in a window (1,2,3), by default: 1, method 1- similar to ssGWAS, method 2- sum the effect variances of SNPs in a window, method 3- similar to method 2 but using sliding window
    --winSize      <INT>    number of SNPs in a window, by default: 20
    --overlap      <INT>    number of SNPs in an overlap region, by default: 5
		
    --varLimit     <FLOAT>  threshold to remove SNPs with small effect variances, by default: 0
    --part                  genotype file is partial and the output kinship file needs to be merged


**qtn**         &ensp; &ensp; &ensp; &ensp; TSR qtn [options]

Trait specific markers were selected by p value from genome wide association studies.

    --pFile     <FILE>   p-value file
    --pvalue    <FLOAT>  threshold to select trait specific SNPs,range (0,1],by default 0.01

    --allGen    <FILE>   input binary genotype (all genotype)	
    --allPos    <FILE>   input coordinate file, all locis
		
    --qtnGen    <FILE>   output triat specific SNPs (binary genotype)	
    --qtnPos    <FILE>   output positions of trait specific SNPs	

    --cor       <FLOAT>  threshold to select independent SNPs,range [0,1],by default 0.9
    --pruneGen  <FILE>   input binary genotype (pruned genotype)
    --prunePos  <FILE>   input coordinate file, pruned locis
		
    --indepGen  <FILE>   output independent SNPs (binary genotype)	
    --indepPos  <FILE>   output positions of independent SNPs
    --sel       <CHAR>   select QTNs and locis independent of them, values can be 'qtn', 'indep' or 'both', by default 'both'
    --rSnp      <INT>    number of SNPs kept in memory at a time,by default 1000
    --inHeader  <FILE>   vcf file or vcf header file



## Formats:
EBV, p value, kinship and genotype formats are compatible with software MGP_float and the output files can be used by TSR, directly.

## Contact

If you find bugs please email me.  
Email:  miaozepu@genomics.cn  
Institute: Applied agriculture of BGI  


## Licence

Free for research. For commercial use please contact P_agro_pmo@genomics.cn
