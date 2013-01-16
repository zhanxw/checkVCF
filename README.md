checkVCF.py
===========

A tools to check input VCFs before running rvtests. The code checks for the monomorphic sites, sites with reference alleles inconsistent with the reference genome, sites with invalid genotypes, non-snp site (e.g. indels), and suspicious sites with allele frequencies greater >0.5  .
After you passed the checking, you can go on to run [rvtests](https://github.com/zhanxw/rvtests) - rare-variant test software.
Example
-------
    python checkVCF.py -r hs37d5.fa -o test $your_VCF

Outputs
-------
    checkVCF.py -- check validity of VCF file for meta-analysis
    version 1.0 (20130115)
    contact zhanxw@umich.edu or dajiang@umich.edu for problems.
    ---------------     REPORT     ---------------
    Total [ 1000 ] lines processed
    [ 0 ] duplicated sites
    [ 0 ] NonSNP site are outputted to [ test.check.nonSnp ]
    [ 0 ] Inconsistent reference sites are outputted to [ test.check.ref ]
    [ 0 ] Variant sites with invalid genotypes are outputted to [ test.check.geno ]
    [ 546 ] Alternative allele frequency > 0.5 sites are outputted to [ test.check.af ]
    [ 582 ] Monomorphic sites are outputted to [ test.check.mono ]
    ---------------     ACTION ITEM     ---------------
    * No error found by checkVCF.py, thank you for cleanning VCF.
    * Upload these files to the ftp: test.check.log test.check.dup test.check.noSnp test.check.ref test.check.geno test.check.af test.check.mono


NOTE: hs37d5.fa need to be indexed by 'samtools faidx hs37d5.fa' command.

