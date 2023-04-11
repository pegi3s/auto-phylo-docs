BLAST
*****

tblastx
-------
This module accepts as input one or multiple FASTA files, and returns (if there is at least one significant hit) a FASTA file for each input file, containing all sequences showing a significant tblastx (https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) hit. The query and expect parameters must be specified in two separate lines, in the config file.

FASTA file processing
*********************

add_taxonomy
------------

This module accepts as input one or multiple FASTA files downloaded from the NCBI assembly database, and adds taxonomy information to the headers of FASTA files, using the SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/), as long as the corresponding GCF or GCA accession number is part of the file name. This is achieved by querying NCBI, and thus, there is always the possibility that the internet connection will fail. In that case, the affected FASTA will be moved to the folder “2-Files_that_failed” under the corresponding block and command directory. It is advisable to check this folder. It returns as output as many FASTA files as the ones given as input.

CGF_and_CGA_CDS_processing
--------------------------

This module accepts as input one or multiple CDS FASTA files downloaded from the NCBI assembly database, and using SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/), implements the following operations:  1) sequence headers are reformatted in order to keep only the scaffold and protein accession numbers; 2) Sequences showing ambiguous nucleotides are removed; 3) only sequences showing a valid start codon, that do not have in frame stop codons, and that are multiple of three are kept; 4) stop codons are removed; 5) sequences showing a size variation (in percentage) relative to the reference sequence greater than the specified value are not kept; 6) only sequences showing the specified pattern are kept; 7) isoforms are removed.  The following parameters must be specified in the config file: start_codon (a list of valid start codons with one space between them), max_size_difference (the maximum difference (in percentage) allowed, relative to the sequence given in the reference file, to consider a given sequence as being of interest), reference_file (the name of the reference FASTA file containing a single nucleotide), pattern (regular expression), codon_table (the codon table that should be used for translation), isoform_min_word_length (the minimum identical word size for two sequences to be inferred as isoforms), and isoform_ref_size (the reference size that is used to decide which one of two isoforms should be kept. The one with the closest size will be kept). It should be noted, that if the size variation (in percentage) relative to the reference sequence is a large number (for instance, 100000), the specified pattern is “.”, or the isoform minimum word length is greater than the sequence sizes, the corresponding operations will be effectively ignored. It returns as output as many files as the ones given as input. When processing a large number of files, in order to avoid out of memory errors, it is advisable to use the split option (see below).

check_contamination
-------------------

This module accepts as input one or multiple FASTA files downloaded from the NCBI assembly database, and adds the taxonomy specified in the config file (taxonomy=) to the name of the file as a suffix, using the SEDA-cli ([1]; https://hub.docker.com/r/pegi3s/seda/) operations. The value of this suffix is then compared with the value declared for category in the config file (category=). If the there is a discrepancy, then the file is treated as being a putative contaminant. This is achieved by querying NCBI, and thus, there is always the possibility that the internet connection will fail. In that case, the affected FASTA will be moved to the folder “4-Suspicious_Files” under the corresponding block and command directory. It is advisable to always check this folder. If there are no contaminations, it returns as many FASTA files as the ones given as input.


disambiguate
------------

This module takes as input one or multiple FASTA files. Using SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/) operations, identical sequence headers are disambiguated using an incremental suffix. It returns as output as many files as the ones given as input.

merge
-----

This module merges all FASTA files in a given folder into a single one, and removes redundant identical sequences or sub-sequences, using the SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/) operations, thus allowing the user to specify modules that accept a single FASTA file in the following step.

prefix
------

This module accepts as input one or more FASTA files. It adds a prefix to the sequence headers, using the SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/)  operations. Some programs (for instance, Blast (https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) or MrBayes [8]) have a size limit for sequence headers, and thus, in the auto-phylo modules that use these programs, the headers are truncated to meet such requirements. Nevertheless, in the truncated header versions, two header names may become identical. In order to avoid such possibility, a prefix may be added to sequence names. It returns as many FASTA files as the ones given as input.

prefix_out
----------

This module accepts as input one or more FASTA files. Using the SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/)  operations, it removes the prefixes that are added by the prefix module, and returns as many FASTA files as the ones given as input.

remove_stops
------------

This module accepts as input one or more FASTA files. Using SEDA-CLI using the SEDA-CLI ([1]; https://hub.docker.com/r/pegi3s/seda/) operations, it removes stop codons from sequences, and returns as many FASTA files as the ones given as input. The alignment of CDS sequences using either the Clustal_Omega_codons or the T-coffee_codons modules, requires that CDS sequences do not have stop codons.

Alignment
*********

Clustal_Omega
-------------

This module accepts as input a single nucleotide FASTA file, and using the Clustal Omega [2] program, returns as output a single sequence alignment FASTA file.

Clustal_Omega_codons
--------------------

This module accepts as input a single CDS FASTA file (sequences must not have stop codons), and returns as output a single sequence alignment FASTA file. The provided nucleotide sequences are first translated into amino acid sequences using the EMBOSS transeq feature [3], and an amino acid alignment is obtained using Clustal_Omega [2]. Then, the corresponding nucleotide alignment is obtained using TranslatorX [4]. Therefore, this option is only suitable for FASTA files containing CDS, which is indicated by the “codons” suffix.  Sequences must not have stop codons.

T-coffee
--------

This module accepts as input a single FASTA file, and using the T-coffee [10] program, returns as output a single sequence alignment FASTA file.

T-coffee_codons
---------------

As indicated by the “codons” suffix, this module accepts as input a single CDS FASTA file (sequences must not have stop codons), and using the T-coffee [10] program, returns as output a single nucleotide alignment FASTA file. The provided nucleotide sequences are first translated into amino acid sequences using the EMBOSS

Tree building
*************

Fasttree
--------

This module accepts as input a single nucleotide sequence alignment FASTA file, and using the Fasttree [5] program, returns as output a tree in Newick format. A generalized time-reversible model of nucleotide evolution with a proportion of invariant sites and a gamma distribution (GTR+I+G) is used. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode=”exhaustive” or ”early-stop”.

me_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a minimum evolution tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or “Partial Deletion” or “Pairwise Deletion”. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode=”exhaustive” or ”early-stop”. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

ml_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a maximum likelihood tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or “Partial Deletion” or “Use all Sites”. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode=”exhaustive” or “early-stop”. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

mp_tree
-------

Tthis module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a maximum parsimony tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or “Partial Deletion” or “Use all Sites”. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode=”exhaustive” or “early-stop”. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

MrBayes
-------

A single CDS alignment FASTA file must be given as input, and using the MrBayes [8] program, a tree in Newick format will be produced. A generalized time-reversible model of nucleotide evolution with a proportion of invariant sites and an independent gamma distribution for first/second and third codon sites (GTR+I+G) is implemented. The number of generations and the burnin parameters must be specified in the config file, by declaring in two different lines, mb_ngen=integer and mb_burnin=integer, respectively. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode=”exhaustive” or “early-stop”.

nj_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a neighbor-joining tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or “Partial Deletion” or “Pairwise Deletion”. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode=”exhaustive” or “early-stop”. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

tree_colapse
------------

Accepts as input a Newick tree file and returns a collapsed Newick tree using the Phylogenetic Tree Collapse (https://hub.docker.com/r/pegi3s/phylogenetic-tree-collapser) program. The sequence header names must start with the full species name.

upgma_tree
----------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns an upgma tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or “Partial Deletion” or “Pairwise Deletion”. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode=”exhaustive” or  “early-stop”. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

Model checking
**************

JModel_test
-----------

This module  accepts as input a nucleotide alignment in FASTA format, and using the JModel [7] test program, produces as an output a report, that can be used to check whether the GTR+I+G model used by the Fasttree [5] and MrBayes [8] modules is appropriate. Before running JModel test, sequence headers are renamed (using SEDA-CLI operations; [1]; https://hub.docker.com/r/pegi3s/seda/), since this program does not allow special characters in sequence header names besides underscores.

Special
*******

split
-----

This is a special command, that is invoked after a regular command, and that takes as input a single argument, namely, the number of groups to consider. For instance, the instruction: “CGF_and_CGA_CDS_processing my_data_dir out_dir split 20” will split the files that are in the my_data_dir directory into 20 equal size subfolders. The data on each subfolder will be processed independently, thus avoiding out of memory errors. The output of all independent analyses will be saved in the out_dir directory.