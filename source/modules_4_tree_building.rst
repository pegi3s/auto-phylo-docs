Tree building
*************

get_phylo_taxa
--------------

This module is used to extract from a Newick file all taxa located in a given clade that is defined by two user specified sequence names (``get_phylo_taxa_name1=``; ``get_phylo_taxa_name2=``). Then, it produces an unaligned FASTA file containing the corresponding nucleotide sequences. Because it needs two inputs, both the nucleotide alignment file and the tree file must be in the same folder. The nucleotide alignment file must have the .nuc_aligned extension (the one attached by every alignment module to FASTA files). The tree file must have the .nwk extension (the one attached to the tree file by all tree producing modules). SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to reformat files.

Fasttree
--------

This module accepts as input a single nucleotide sequence alignment FASTA file, and using the Fasttree [5] program, returns as output a tree in Newick format. A generalized time-reversible model of nucleotide evolution with a proportion of invariant sites and a gamma distribution (GTR+I+G) is used. The resulting tree can be rooted using the Root Digger [6] program, by declaring in the config file in two different lines: root=yes and mode="exhaustive" or "early-stop". Please note that Root Digger does not allow white spaces or special characters other than underscores in sequence header names.

FastRoot
--------

This module accepts as input one Newick tree file, and using the FastRoot (https://github.com/uym2/MinVar-Rooting) program, returns as output a rooted tree also in Newick format. The rooting method to be used by this module must be specified in the config file (``fastroot_rooting_method=``). The values for this parameter can be either “MV" (Minimum Variance Rooting), “MP" (Midpoint Rooting), or “OG" (Outgroup Rooting). In the latter case, the parameter ``fastroot_outgroup=""`` must be defined in the config file (if present, the value attributed to this parameter is ignored when choosing ``fastroot_rooting_method=MV or MP``). If multiple outgroups are to be chosen, names should be separated by spaces. For instance, ``fastroot_outgroup="Name1 Name2"``.

Mafft
-----

This module accepts as input a single nucleotide FASTA file, and using the MAFFT (https://mafft.cbrc.jp/alignment/software/) program, returns as output a single sequence alignment FASTA file. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed in order to remove line breaks from the resulting alignment.

Mafft_codons
------------

This module accepts as input a single CDS FASTA file (sequences must not have stop codons), and returns as output a single sequence alignment FASTA file. The provided nucleotide sequences are first translated into amino acid sequences using the EMBOSS transeq feature [3], and an amino acid alignment is obtained using MAFFT (https://mafft.cbrc.jp/alignment/software/). Then, the corresponding nucleotide alignment is obtained using TranslatorX [4]. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed in order to remove line breaks from the resulting alignments. This option is only suitable for FASTA files containing CDS, as indicated by the “codons" suffix.

me_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a minimum evolution tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: ``me_tree_bootstrap=positive_integer`` and ``me_tree_treatment="Complete Deletion" or “Partial Deletion" or “Pairwise Deletion"``. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

ml_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a maximum likelihood tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: ``ml_tree_bootstrap=positive_integer`` and ``ml_tree_treatment="Complete Deletion" or “Partial Deletion" or “Use all Sites"``. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

mp_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a maximum parsimony tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: ``mp_tree_bootstrap=positive_integer`` and ``mp_tree_treatment="Complete Deletion" or “Partial Deletion" or “Use all Sites"``. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

MrBayes
-------

A single CDS alignment FASTA file must be given as input, and using the MrBayes [8] program, a tree in Newick format will be produced. A generalized time-reversible model of nucleotide evolution with a proportion of invariant sites and an independent gamma distribution for first/second and third codon sites (GTR+I+G) is implemented. The number of generations and the burnin parameters must be specified in the config file, by declaring in two different lines, ``mb_ngen=integer`` and ``mb_burnin=integer``, respectively.

nj_tree
-------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns a neighbor-joining tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: ``nj_tree_bootstrap=positive_integer`` and ``nj_tree_treatment="Complete Deletion" or “Partial Deletion" or “Pairwise Deletion"``. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.

Probcons
--------

This module accepts as input a single nucleotide FASTA file, and using the PROBCONS (http://probcons.stanford.edu/manual.pdf) program, returns as output a single sequence alignment FASTA file. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to reformat files.

Probcons_codons
---------------

This module accepts as input a single CDS FASTA file (sequences must not have stop codons), and returns as output a single sequence alignment FASTA file. The provided nucleotide sequences are first translated into amino acid sequences using the EMBOSS transeq feature [3], and an amino acid alignment is obtained using PROBCONS [http://probcons.stanford.edu/manual.pdf]. Then, the corresponding nucleotide alignment is obtained using TranslatorX [4]. Therefore, this option is only suitable for FASTA files containing CDS, which is indicated by the “codons" suffix. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/) are performed to reformat files.

Probcons_refinement
-------------------

This module accepts as input a single FASTA file containing aligned sequences, and using the PROBCONS (http://probcons.stanford.edu/manual.pdf) program refinement option, returns a refined FASTA file. The number of iterations (``probcons_refin_iterations=``) to be executed in the refinement must be specified in the config file.

Rootdigger
----------

This module accepts a nucleotide alignment file in FASTA format, as well as a Newick tree file with the corresponding tree. Using Root Digger [6] program the tree is then rooted. Because it needs two inputs, both the nucleotide alignment file and the tree file must be in the same folder. The nucleotide alignment file must have the .nuc_aligned extension (the one attached by every alignment module to FASTA files). The tree file must have the .nwk extension (the one attached to the tree file by all tree producing modules). The Root Digger mode must be declared in the config file (``rootdigger_mode="exhaustive" or “early-stop"``). Please note that Root Digger does not allow white spaces or special characters other than underscores in sequence header names.

tree_collapser
--------------

Accepts as input a Newick tree file and returns a collapsed Newick tree using the Phylogenetic Tree Collapse (https://hub.docker.com/r/pegi3s/phylogenetic-tree-collapser) program. The sequence header names must start with the full species name. If ``tc_taxonomy=""``, tree_collapse runs with default parameters, otherwise, the following parameters must be declared in the config file: the name of the file with the taxonomy to be used (``tc_taxonomy=``) and the name of the sequence mapping file (``tc_stsm=``).

upgma_tree
----------

This module accepts as input a single nucleotide alignment in FASTA format, and using the Mega_CC [9] program, returns an upgma tree, in Newick format. The number of bootstraps to be executed, and how sites with alignment gaps should be treated, can be specified by declaring in the config file in two separate lines: ``upgma_tree_bootstrap=positive_integer`` and ``upgma_tree_treatment="Complete Deletion" or “Partial Deletion" or “Pairwise Deletion"``. In the mao file that is used to build the tree, and that is saved together with the intermediate files that are produced, the user can find all the settings that are being used.
