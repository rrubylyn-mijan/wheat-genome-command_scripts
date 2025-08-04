# Wheat Genome Assembly Utilities

This repository documents useful command-line operations used during genome assembly and analysis of wheat cultivars. These commands assist in identifying unanchored contigs after scaffolding, which are important for assembly quality metrics and manuscript reporting.

---

## Bash Commands for Counting Unanchored Contigs

Use these commands to count how many contigs in your final assembly FASTA file are **unanchored**, assuming you have **21 chromosome pseudomolecules** (1A–7D).

```bash
# Count total number of sequences (pseudomolecules + unanchored)
grep -c '^>' wheat+unanchored_contigs.fasta

# Subtract 21 chromosomes to get number of unanchored contigs
expr $(grep -c '^>' wheat+unanchored_contigs.fasta) - 21

# Preview first 10 contigs in the FASTA file
grep '^>' wheat+unanchored_contigs.fasta | head -n 10
```

## Command to count the total number of base pairs in subgenomes A, B, and D in wheat.fasta

```bash
awk '
  BEGIN {A=0; B=0; D=0; chr=""}
  /^>/ {
    chr = $0
    next
  }
  {
    gsub(/\s+/, "", $0)
    if (chr ~ />chr[1-7]A/) A += length($0)
    else if (chr ~ />chr[1-7]B/) B += length($0)
    else if (chr ~ />chr[1-7]D/) D += length($0)
  }
  END {
    printf "Subgenome A: %'\''d bp\n", A
    printf "Subgenome B: %'\''d bp\n", B
    printf "Subgenome D: %'\''d bp\n", D
    printf "Total:       %'\''d bp\n", A + B + D
  }
' wheat.fasta
```
