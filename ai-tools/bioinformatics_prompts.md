# Bioinformatics Prompt Examples

> Curated from web and literature sources — August 2026

---

## 1. Sequence Analysis

> *"You are a bioinformatics expert. Analyze the following DNA sequence for:*
> - *Notable motifs and conserved regions*
> - *Open reading frames (ORFs) and potential coding regions*
> - *GC content percentage*
> - *Palindromic sequences or repeats*
> - *Possible origin (species or gene family)*
>
> *Explain each step, reference biological concepts, and provide interpretations."*

---

## 2. Pipeline / Workflow Generation

> *"Create a Nextflow pipeline to perform RNA-seq differential expression analysis. Include steps for quality control, alignment, quantification, and interpretation. List the commonly used tools for each step."*

> *"Act as a senior bioinformatics engineer specializing in omics data pipelines. For a single-cell RNA-seq dataset in FASTQ format, write a Nextflow pipeline that includes QC, alignment, counting (with STAR and featureCounts), and outputs a Seurat-compatible matrix. Use idiomatic code with clear comments and reproducibility best practices."*

> *"Act as an expert bioinformatician. Write a Bash script that will:*
> - *Run FastQC on all FASTQ files in a folder*
> - *Perform adapter trimming using Trimmomatic*
> - *Align reads to the hg38 reference genome using Bowtie2*
> - *Convert SAM to BAM, sort, and index*
> - *Generate a coverage track in bigWig format*
>
> *State assumptions about folder structure, reference indexing, tool versions, and CPU parallelization."*

---

## 3. GWAS / Variant Analysis

> *"List all the steps needed to perform a genome-wide association study (GWAS) using PLINK, given a VCF file and phenotype data."*

> *"Provide a Galaxy workflow for SNP identification and annotation, for a user unfamiliar with programming."*

---

## 4. Code Generation & Debugging

> *"Write a Python script to parse a FASTQ file and calculate the average quality score per read."*

> *"Act as an experienced bioinformatician proficient in R. Write code to:*
> - *Load a multiple alignment file in ClustalW format*
> - *Calculate evolutionary distance*
> - *Build a Neighbor-Joining tree*
> - *Visualize the phylogeny"*

> *"I am receiving a 'Segmentation fault' error when running BWA for read alignment. What are the possible causes and how can I fix them?"*

---

## 5. Data Standardization & Annotation

> *"Given this GFF3 file, extract all gene features and provide a table with gene names, start/end locations, and functional annotations."*

> *"How can I convert between different genomics file formats (e.g., BED to GTF) using command-line tools?"*

---

## 6. Literature Review / Systematic Screening

> *"Given the following abstract, use PICO (Population, Intervention, Comparator, Outcome) criteria to decide whether it should be included in a systematic review about CRISPR gene editing in plants."*

> *"Summarize the key findings of this paper focusing on the role of non-coding RNAs in Alzheimer's disease."*

---

## 7. Biomedical Question Answering

> *"What are the main challenges in de novo protein structure prediction using AI approaches?"*

> *"List the top 5 bioinformatics tools for metagenomic taxonomic classification, along with their key features."*

---

## 8. Report Generation

> *"Write a detailed report for an analysis of sequencing data from two samples, covering:*
> - *Data acquisition, quality control, and mapping (Bowtie2, BWA, TopHat)*
> - *Conversion, visualization in IGV, and extraction of mapping metrics*
> - *De novo assembly of reads mapped to chromosome 1*
> - *All commands, steps, troubleshooting notes, and summary plots"*

---

## Prompt Engineering Best Practices

| Strategy | Example |
|---|---|
| **Role assignment** | *"You are a senior bioinformatician…"* |
| **Chain-of-thought** | *"Think step by step through QC, alignment, and interpretation"* |
| **Structured output** | *"Return a table with gene name, position, and annotation"* |
| **Domain context** | Specify tools, file formats, organism, genome build |
| **Iterative refinement** | Paste error messages back for debugging cycles |
| **Clarifying questions** | *"Ask up to three clarifying questions before beginning"* |

---

## Key Resources

- **GitHub**: [geraldmc/bioinformatics_prompts](https://github.com/geraldmc/bioinformatics_prompts) — templates for genomics, metagenomics, NGS, precision medicine
- **GitHub**: [ai-boost/awesome-prompts](https://github.com/ai-boost/awesome-prompts/blob/main/prompts/bioinformatics_engineer.txt) — bioinformatics engineer persona prompts
- **Paper**: *"Prompt-based bioinformatic pipeline generation for a multi-step workflow"* — Bioinformatics Advances, 2025. https://academic.oup.com/bioinformaticsadvances/article/6/1/vbaf308/8346364
- **Paper**: *"From Prompt to Pipeline: Large Language Models for Scientific Workflow"* — arXiv, 2025. https://arxiv.org/pdf/2507.20122
- **Paper**: *"How to Write Effective Prompts for Screening Biomedical Literature"* — MDPI, 2025. https://www.mdpi.com/2673-7426/5/1/15
- **Blog**: [ge-lab.org — Solving bioinformatics problems with ChatGPT](https://www.ge-lab.org/2023/04/01/solving-bioinformatics-problems-with-chatgpt-example-prompts-from-three-studies/)
