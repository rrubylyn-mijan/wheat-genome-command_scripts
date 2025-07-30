\# Wheat Genome Assembly Utilities



This repository documents useful command-line operations used during genome assembly and analysis of two wheat cultivars. These commands assist in identifying unanchored contigs after scaffolding, which are important for assembly quality metrics and manuscript reporting.



---



\## Bash Commands for Counting Unanchored Contigs



Use these commands to count how many contigs in your final assembly FASTA file are \*\*unanchored\*\*, assuming you have \*\*21 chromosome pseudomolecules\*\* (1A–7D).



```bash

\# Count total number of sequences (pseudomolecules + unanchored)

grep -c '^>' wheat+unanchored\_contigs.fasta



\# Subtract 21 chromosomes to get number of unanchored contigs

expr $(grep -c '^>' wheat+unanchored\_contigs.fasta) - 21



\# Show the first 10 contig names in the FASTA

grep '^>' wheat+unanchored\_contigs.fasta | head -n 10



