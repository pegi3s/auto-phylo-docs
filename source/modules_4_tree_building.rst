Tree building
*************

Fasttree
--------

This module accepts as input a single nucleotide sequence alignment FASTA file, and using the Fasttree [5] program, returns as output a tree in Newick format. A generalized time-reversible model of nucleotide evolution with a proportion of invariant sites and a gamma distribution (GTR+I+G) is used. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode="exhaustive" or "early-stop".

me_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a minimum evolution tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or "Partial Deletion" or "Pairwise Deletion". The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode="exhaustive" or "early-stop". In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

ml_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a maximum likelihood tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or "Partial Deletion" or "Use all Sites". The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode="exhaustive" or "early-stop". In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

mp_tree
-------

Tthis module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a maximum parsimony tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or "Partial Deletion" or "Use all Sites". The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode="exhaustive" or "early-stop". In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

MrBayes
-------

A single CDS alignment FASTA file must be given as input, and using the MrBayes [8] program, a tree in Newick format will be produced. A generalized time-reversible model of nucleotide evolution with a proportion of invariant sites and an independent gamma distribution for first/second and third codon sites (GTR+I+G) is implemented. The number of generations and the burnin parameters must be specified in the config file, by declaring in two different lines, mb_ngen=integer and mb_burnin=integer, respectively. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode="exhaustive" or "early-stop".

nj_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a neighbor-joining tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or "Partial Deletion" or "Pairwise Deletion". The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode="exhaustive" or "early-stop". In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

tree_colapse
------------

Accepts as input a Newick tree file and returns a collapsed Newick tree using the Phylogenetic Tree Collapse (https://hub.docker.com/r/pegi3s/phylogenetic-tree-collapser) program. The sequence header names must start with the full species name.

upgma_tree
----------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns an upgma tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: bootstrap=positive_integer and treatment="Complete Deletion" or "Partial Deletion" or "Pairwise Deletion". The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode="exhaustive" or  "early-stop". In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.
