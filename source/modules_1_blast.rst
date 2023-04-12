BLAST
*****

tblastx
-------
This module accepts as input one or multiple FASTA files, and returns (if there is at least one significant hit) a FASTA file for each input file, containing all sequences showing a significant tblastx (https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) hit. The query and expect parameters must be specified in two separate lines, in the config file.