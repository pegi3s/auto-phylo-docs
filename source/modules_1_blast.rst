BLAST
*****

tblastx
-------
This module accepts as input one or multiple FASTA files, and returns (if there is at least one significant hit) a
FASTA file for each input file, containing all sequences showing a significant tblastx
(https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) hit. The query and expect parameters must be
specified in two separate lines, in the config file. SEDA-CLI operations ([1]; https://hub.docker.com/r/pegi3s/seda/)
are performed to remove line breaks from sequences.