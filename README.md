checkVCF.py
===========

checkVCF.py is a small tool written in [Python](http://www.python.org/) to check input [VCF](http://www.1000genomes.org/wiki/Analysis/Variant%20Call%20Format/vcf-variant-call-format-version-41) files before association tests. 
It can report monomorphic sites, sites with reference alleles inconsistent with the reference genome, sites with invalid genotypes, non-SNP site (e.g. indels), and all sites with allele frequencies greater than ''0.5''.
After you passed the checking, you can go on to run [rvtests](https://github.com/zhanxw/rvtests) - rare-variant test software.

Download
--------

Download from [this bundle (839 Mb)](http://qbrc.swmed.edu/zhanxw/software/checkVCF/checkVCF-20140116.tar.gz) and unzip the downloaded file.
This includes [checkVCF.py](https://github.com/zhanxw/checkVCF/blob/master/checkVCF.py) script, reference genome (hs37d5.fa) in FASTA format and its index file (hs37d5.fa.fai).

Example
-------

    python checkVCF.py -r hs37d5.fa -o test $your_VCF

Outputs
-------

### Console output and .log file
Upon successfully running checkVCF.py on the example file, you will see following outputs:

    checkVCF.py -- check validity of VCF file for meta-analysis
    version 1.3 (20130223)
    contact zhanxw@umich.edu or dajiang@umich.edu for problems.
    Python version is [ 2.7.3.final.0 ] 
    Begin checking vcfFile [ example.vcf.gz ]
    ---------------     REPORT     ---------------
    Total [ 18 ] lines processed
    Examine [ 7 ] VCF header lines, [ 11 ] variant sites, [ 6 ] samples
    [ 0 ] duplicated sites
    [ 0 ] NonSNP site are outputted to [ tmp.check.nonSnp ]
    [ 10 ] Inconsistent reference sites are outputted to [ tmp.check.ref ]
    [ 0 ] Variant sites with invalid genotypes are outputted to [ tmp.check.geno ]
    [ 1 ] Alternative allele frequency > 0.5 sites are outputted to [ tmp.check.af ]
    [ 1 ] Monomorphic sites are outputted to [ tmp.check.mono ]
    ---------------     ACTION ITEM     ---------------
    * Read tmp.check.ref, for autosomal sites, make sure the you are using the forward strand
    * Upload these files to the ftp: tmp.check.log tmp.check.dup tmp.check.noSnp tmp.check.ref tmp.check.geno tmp.check.af tmp.check.mono

### .check.nonSnp file

This file includes all non-SNP sites. These sites can be detected when the length of the reference allele or alternative allele is larger than one. For example, reference allele is AT. Non-SNP sites also include reference alleles that are not composited of 'A', 'C', 'G', 'T' alleles or alternative alleles that are not composited of 'A', 'T', 'G', 'C', '.' alleles.

### .check.ref file

This file includes the variant sites that do not match reference alleles.
That can happen when: (1) variant chromosome names do not appear in the reference genome file. You will see a line with "FailedGetBase" and chromosome:position from the input VCF file; (2) reference alleles do not match. You will see "MismatchRefBase" and chromosome:position:trueReferenceAllele-referenceAlleleInVCF:referenceAlleleInVCF. For example:

    MismatchRefBase 19:50578409:G-C/T
    FailedGetBase   23:208316
	
### .check.geno file

This file contains line numbers in which genotypes are not found or not formatted correctly.
You will get either "IndividualMissingGTField" warning or "IndividualHasInvalidGT" warnings.

### .check.af file

This file contains the sites where alternative allele frequencies are larger than 0.5 . 
It is normal that this file contains a number of lines. 
For human exome chip, you are likely to have ~10k lines in this file. 
That means out of total ~250k variants, around 10k SNP variants have allele frequencies larger than 0.5.

### .check.mono file

This file contains the monomorphic sites.
It is normal that this file contains a number of lines.
In the ideal case, VCF files should only contain variant sites.
However, it is practical or convenient to keep some monomorhipc sites in the VCF file.
This file records these monomorphic sites.

Contact
-------

Questions or comments can be sent to [Xiaowei Zhan](mailto:zhanxw@umich.edu)  or [Dajiang Liu](mailto:dajiang@umich.edu).


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/zhanxw/checkvcf/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

