checkVCF.py
===========

checkVCF.py is a small tools written in Python script to check input [VCF](http://www.1000genomes.org/wiki/Analysis/Variant%20Call%20Format/vcf-variant-call-format-version-41) files before association tests. 
It will report monomorphic sites, sites with reference alleles inconsistent with the reference genome, sites with invalid genotypes, non-snp site (e.g. indels), and all sites with allele frequencies greater than ''0.5''.
After you passed the checking, you can go on to run [rvtests](https://github.com/zhanxw/rvtests) - rare-variant test software.

Download
--------

Download from [this]() and unzip downloaded file.
This includes checkVCF.py script, reference genome in FASTA format and its index file.

Example
-------

    python checkVCF.py -r hs37d5.fa -o test $your_VCF

Outputs
-------

### Console output and .log file
Upon successfully running checkVCF.py on the example file, you will obtain following information:

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


### .check.nonSnp file

This file includes all non-SNP sites. These can be detected when the length of your reference allele or alternative allele is larger than one. For example, reference allele is AT. Non-SNP sites also includes reference alleles that are not composited from 'A', 'C', 'G', 'T' alleles or alternative alleles that are not composited from 'A', 'T', 'G', 'C', '.' alleles.

### .check.ref file

This file includes the variant sites that do not match reference alleles.
That can happen when: (1) variant chromosome names do not appear in the reference genome file. You will see a line with "FailedGetBase" and chromosome:position from the input VCF file; (2) reference alleles do not match. You will see "MismatchRefBase" and chromosome:position:trueReferenceAllele-referenceAlleleInVCF:referenceAlleleInVCF. For example:

    MismatchRefBase 19:50578409:G-C/T
    FailedGetBase   23:208316
	
### .check.geno file

This file contains the line number in which genotypes are not found or not formatted correctly.
You will get "IndividualMissingGTField" and "IndividualHasInvalidGT" warnings.

### .check.af file

This file contains the sites where alternative allele frequency larger than 0.5 . 
It is normal that this files contains a number of lines. 
For human exome chip, you are like to see 10k lines in this file. 
That means out of total 250k variants, around 10k SNP variants have allele frequency larger than 0.5.

### .check.mono file

This file contains the monomorphic sites.
It is normal that this files contains a number of lines.
In the ideal case, VCF files should only contain variant sites.
However, it is practical or convenient to keep some monomorhipc sites in the VCF file.
This file records the number of monomorphic sites.

Contact
-------

Questions or comments can be sent to [Xiaowei Zhan](mailto:zhanxw@umich.edu)  or [Dajiang Liu](mailto:dajiang@umich.edu).
