# Chapter 2: High-Throughput Sequencing Overview

## Learning Objectives

By the end of this chapter, you should be able to:
1. Explain the historical transition from microarray to next-generation sequencing (NGS)
2. Describe the fundamental principles of DNA sequencing technologies
3. Compare key NGS platforms (Illumina, PacBio, Oxford Nanopore, 10x)
4. Understand sequencing library preparation and quality control
5. Appreciate the advantages and trade-offs of different sequencing approaches for transcriptomics

---

## 2.1 From Microarrays to Next-Generation Sequencing

### The Pre-NGS Era: Microarrays

Before high-throughput sequencing, **microarrays** were the standard tool for genome-wide gene expression analysis.

**How microarrays work:**
- DNA probes (oligos) are bound to a glass slide or silicon chip
- Sample RNA is labeled with fluorescent dyes
- Fluorescence intensity indicates target abundance
- Requires prior knowledge of sequences to design probes

**Advantages:**
- Relatively cheap
- Fast (24-48 hours)
- Established protocols and analysis

**Limitations:**
- **Cannot discover novel transcripts** or splice variants
- Background noise from cross-hybridization
- Limited dynamic range (~4-5 orders of magnitude)
- Requires accurate probe design

### The NGS Revolution (2008 onwards)

**High-throughput sequencing** overcame microarray limitations by:
- **Sequencing actual RNA molecules** (not hybridization-based detection)
- Discovering novel transcripts and isoforms without prior knowledge
- Providing much larger dynamic range (~8 orders of magnitude)
- Generating absolute quantification (read counts)

**Cost trajectory**: 
- ~$100K per human genome (2008)
- ~$1K per human genome (2015)
- ~$100-300 per genome (2024)
- Enabling large-scale projects (GTEx, TCGA, HCA, etc.)

---

## 2.2 Fundamentals of DNA Sequencing

### The Sequencing Workflow: Overview

All modern sequencing technologies follow a similar workflow:

```
1. Sample Preparation → 2. Library Construction → 3. Cluster Generation → 
4. Sequencing → 5. Base Calling → 6. Quality Assessment
```

### 1. Sample Preparation

**Starting Material:**
- Tissue or cultured cells
- Extract total RNA or select specific RNA types (poly-A+, ribosomal RNA-depleted)

**Key decisions:**
- **Single-cell or bulk?** Single-cell captures cell-type heterogeneity; bulk averages over many cells
- **Preservation of UMI (Unique Molecular Identifiers)?** For absolute quantification and error detection

### 2. Library Construction

**Process:**
1. **Reverse transcription**: Convert RNA → cDNA using reverse transcriptase (RT)
2. **2nd strand synthesis** (optional, depending on method)
3. **Fragmentation**: Break cDNA into manageable pieces (~200-600 bp for Illumina, up to 30+ kb for long-read)
4. **Adapter ligation**: Add platform-specific sequences to fragment ends
5. **cDNA enrichment and amplification**: PCR or in vitro amplification

**Adapter sequences:**
- Contain binding sites for cluster generation and sequencing primers
- Platform-specific (Illumina, PacBio, Oxford Nanopore, 10x)
- May include barcodes for sample multiplexing or cell identification

**Key consideration: Strand bias**
- RT bias: Random priming may preferentially amplify certain sequences
- dUTP vs. dTTP incorporation: Affects strand specificity

### 3. Cluster Generation

#### **Short-Read Sequencing (Illumina)**

**Cluster generation (bridge amplification):**
1. Adapters bind to lawn of oligos on the flow cell
2. Polymerase extends the cDNA fragment
3. Fragments are denatured; single strand refolds to form bridge
4. Polymerase copies the bridge, creating a cluster
5. Repeat ~35 cycles → 1000-2000 identical copies per cluster

**Result:** Millions to billions of clusters per flow cell

#### **Long-Read Sequencing (PacBio, Oxford Nanopore)**

**Different approach:**
- PacBio: Single molecules are captured in nano-wells; sequenced multiple times (polymerase activity)
- Nanopore: Single molecule passes through nanopore; electrical current detected

**Trade-off:** Lower throughput but longer reads (>10 kb to >100 kb)

### 4. Sequencing by Synthesis (Illumina)

**Reversible terminator chemistry:**

```
Cycle (repeated 50-300 times):
1. Add one labeled dNTP (dATP, dGTP, dCTP, or dTTP)
   - Each base has unique fluorophore
   - 3' terminator (ddNTP) blocks polymerase
2. Imaging: Camera captures fluorescence for each cluster
3. Remove terminator and fluorophore → cycle repeats
```

**Output per cycle:**
- Position 1, 2, 3, ..., read length
- Cluster ID and base called
- Quality score (Phred score, Q)

### 5. Base Calling and Data Output

**Base calling:**
- Image intensities → base identity and confidence
- Produced by real-time instruments (HiSeq, MiSeq) or post-run (NovaSeq)

**Quality metrics:**

**Phred Quality Score (Q):**
$$Q = -10 \log_{10}(P_e)$$

where $P_e$ is the error probability.

| Q Score | Error Rate | Accuracy |
|---------|-----------|----------|
| Q30 | 1 in 1000 | 99.9% |
| Q40 | 1 in 10,000 | 99.99% |
| Q50 | 1 in 100,000 | 99.999% |

**Output format:**
- **FASTQ files**: Read sequences + quality scores
- Millions to billions of reads per sample

---

## 2.3 Major Sequencing Platforms

### Illumina (Short-Read, High Throughput)

**Characteristics:**
- **Read length**: 50-300 bp (paired-end common)
- **Throughput**: 10-600 billion reads per instrument
- **Accuracy**: Q30-Q40 bases (99.9-99.99%)
- **Cost per base**: Lowest among current platforms
- **Platforms**: MiSeq, NextSeq, NovaSeq, iSeq

**Advantages:**
- Mature, well-established protocol
- Highest throughput and lowest cost per base
- Excellent for genome-wide surveys
- Extensive software ecosystem

**Limitations:**
- Short reads difficult to resolve complex isoforms
- Repetitive regions challenging
- Standard protocol requires significant cDNA input (mitigated by 10x/Takara)

**Best for:** Bulk RNA-seq, single-cell RNA-seq (with barcoding), high-resolution exon-level quantification

---

### PacBio (Long-Read, Accurate)

**Characteristics:**
- **Read length**: 10-30 kb median; >100 kb possible
- **Throughput**: 5-15 million reads per instrument
- **Accuracy**: Q20-Q30 (with circular consensus sequencing, Q30+)
- **Cost**: Higher per read than Illumina; competitive per base for long reads
- **Latest**: Revio, Sequel II

**Chemistry:**
- Single molecule, real-time (SMRT) sequencing
- Polymerase tethered in nano-well; watches single molecule synthesized
- Multiple passes through template (polymerase processivity → circular consensus)

**Advantages:**
- **Full-length transcript sequencing** (capture entire mRNA isoforms)
- Long reads resolve repetitive regions better
- Native detection of DNA modifications (methylation)

**Limitations:**
- High cost per base
- Smaller insert size than older platforms (though latest revisions improve this)
- Requires higher RNA quality initially

**Best for:** Isoform discovery, full-length transcript characterization, detecting splice variants

---

### Oxford Nanopore Technologies (Long-Read, Ultra-Long)

**Characteristics:**
- **Read length**: 10-50 kb median; >300 kb possible (!!)
- **Throughput**: Variable; high-throughput GridION has 48 channels
- **Accuracy**: Q10-Q20 without polishing; Q20+ with 5mc/6mA detection
- **Cost**: Competitive; scalable with flow cells
- **Platforms**: MinION, GridION, PromethION

**Physics:**
- Single molecule passes through engineered protein pore in lipid bilayer
- Different nucleotides have characteristic electrical signals
- No amplification or fluorescence needed

**Advantages:**
- **Extremely long reads** (>100 kb common)
- Real-time sequencing (data streaming)
- Direct detection of RNA modifications
- Lower cost per base for deep coverage
- Portable (MinION) and high-throughput (PromethION)

**Limitations:**
- Higher error rate without consensus/polishing (~5-10%)
- Requires good RNA quality and intact molecules
- Biases in base composition (homopolymers)

**Best for:** Ultra-long transcripts, isoform discovery at scale, detecting structural variants and modifications

---

### 10x Genomics Chromium (Single-Cell Barcoding)

**Characteristics:**
- **Application**: Single-cell RNA-seq (scRNA-seq)
- **Barcode strategy**: Oil-in-water emulsions with barcode-carrying beads
- **Throughput**: 500-10,000 cells per run (depending on kit)
- **Read length**: 28bp (barcode + UMI) + 91bp (cDNA)
- **Accuracy**: Q30+ for most bases

**Workflow:**
1. Cell suspension + capture beads in oil emulsion
2. Each droplet captures ~1 cell + 1 bead
3. Reverse transcription occurs inside droplet
4. cDNA tagged with barcode (cell ID) + UMI (molecule ID)
5. Pooled libraries sequenced on Illumina (usually paired-end)

**Advantages:**
- **Unbiased cell capture** (random)
- Enables massively parallel single-cell profiling
- Standard for many single-cell studies

**Limitations:**
- Fixed barcode set (can lead to collisions in large pools)
- 3' bias (captures transcript ends for UMI methods)
- Requires suspension of individual cells

**Best for:** Single-cell transcriptomics; immune profiling; tissue dissociation studies

---

## 2.4 Library Preparation for Transcriptomics

### Bulk RNA-seq Library Prep

**Standard workflow (e.g., TruSeq):**

1. **poly-A enrichment or rRNA depletion**
   - Most experiments enrich for poly(A)+ transcripts
   - Alternative: Deplete rRNA to capture all transcripts
2. **Fragmentation**: Break RNA into smaller pieces
3. **Reverse transcription**: Create first-strand cDNA (often with random hexamers)
4. **Second-strand synthesis**: Create dsDNA library
5. **Adapter ligation**: Add platform-specific sequences
6. **PCR amplification**: Enrich for full-length molecules
7. **Quality control**: Verify library size and purity

**Key parameters:**
- **Insert size**: Affects read mapping and isoform resolution
- **Amount of starting RNA**: Affects sensitivity
- **PCR cycles**: Balance amplification efficiency vs. bias

### Single-Cell RNA-seq (scRNA-seq)

**10x Chromium specific:**

1. **Cell capture in emulsion**: Each droplet contains one cell + barcode bead
2. **Reverse transcription**: Occurs within droplet
3. **cDNA synthesis**: First-strand cDNA tagged with:
   - Cell barcode (16 bp; identifies droplet/cell)
   - UMI (12 bp; identifies individual molecule)
   - poly-T stretch (anchors to poly-A tail)
4. **Emulsion breaking**: Combine all cDNA
5. **Library amplification**: Tagmentation (Nextera) adds platform adapters
6. **Sequencing library**: Ready for Illumina sequencing

**Result:** Millions of reads, each tagged with (cell_barcode, UMI, sequence_read)

---

## 2.5 Data Quality Control

### Pre-Sequencing QC

Before loading on sequencer:

| Metric | Target |
|--------|--------|
| **RNA integrity** | RIN > 7 (or DIN for long-read) |
| **Library size** | 200-600 bp for Illumina (Bioanalyzer) |
| **cDNA quantification** | Sufficient for desired throughput |
| **cDNA concentration** | Usually 1-10 nM |
| **Library purity** | No visible adapters or contamination |

### Post-Sequencing QC

Assess sequencing quality:

**Quality metrics (from FASTQ):**
- **Per-base quality**: Phred score distribution (Q30+ desired)
- **GC content**: Should reflect genomic/transcriptomic background
- **Sequence duplication**: Low duplication expected (high = over-amplification)
- **Adapter contamination**: Should be minimal after trimming

**Tools:** FastQC, MultiQC

**Example: Sample FASTQ file:**
```
@SEQ_ID_1
ACGTACGTACGTACGTACGTACGTACGT...
+
IIIIIIIIIIIIIIIIIIIIIIIIIIII...

@SEQ_ID_2
TGCATGCATGCATGCATGCATGCATGCA...
+
HHHHGHHHIHIHGHIGHIHIHIGHIGHI...
```

- Header line: Sequence ID
- Sequence: Actual bases
- Plus line: Separator
- Quality: Phred scores (ASCII characters)

---

## 2.6 Mapping and Quantification Workflow

After sequencing, raw reads must be:

1. **Quality trimming**: Remove low-quality bases and adapters
2. **Mapping**: Align reads to reference genome or transcriptome
3. **Quantification**: Count reads per gene/transcript

### Quantification Approaches

#### **Alignment-Based:**
- Map reads to genome or transcriptome using bowtie2, HISAT2, STAR
- Count overlapping reads per gene (HTSeq, featureCounts)
- Capture splice junction reads for isoform awareness

#### **Alignment-Free (Pseudoalignment):**
- Avoid full alignment; match k-mers to transcriptome (kallisto, salmon)
- Much faster; still accurate for abundance estimation
- Cannot directly detect novel junctions

#### **Comparison:**

| Aspect | Alignment-Based | Pseudoalignment |
|--------|-----------------|-----------------|
| **Speed** | Slower | Faster |
| **Sensitivity** | High | High (similar) |
| **Splice junctions** | Direct detection | Implicit |
| **Novel transcripts** | Can detect | Limited |
| **Repeated regions** | Challenging | Also challenging |

---

## 2.7 Experimental Design Considerations

### Choice of Sequencing Technology

**Decision tree:**

```
Need isoform-level precision?
├─ YES → Long-read preferred (PacBio, Nanopore)
│         Backup: Short-read with long insert libraries
└─ NO → Short-read (Illumina) sufficient

Single-cell resolution needed?
├─ YES → 10x Chromium or similar
└─ NO → Bulk RNA-seq

Need spatial information?
├─ YES → Spatial transcriptomics methods (Visium, MERFISH, seqFISH)
└─ NO → Standard sequencing

Budget and timeline constraints?
├─ TIGHT → Illumina short-read (cost-effective)
└─ FLEXIBLE → Combine short + long-read (complementary)
```

### Biological Replication

**Critical for robust analysis:**
- Minimum 2-3 biological replicates per condition
- >3-4 replicates if asking subtle questions
- Pseudoreplicates (technical replicates) insufficient for statistical inference

### Sequencing Depth

**Depends on research question:**
- **Gene discovery**: 10-20 million reads/sample (bulk)
- **Quantification**: 30-50 million reads/sample
- **Isoform resolution**: 50-100 million reads/sample
- **Single-cell**: 50K-500K reads/cell (total)

**Saturation curve:** Sequencing more reads gives diminishing returns

---

## Key Takeaways

1. **NGS revolutionized transcriptomics** by enabling hypothesis-free discovery of novel transcripts
2. **Illumina dominates** for bulk and single-cell RNA-seq due to cost and maturity
3. **Long-read platforms** (PacBio, Nanopore) excel at full-length isoform characterization
4. **Library preparation** introduces technical biases; understanding methodology is crucial
5. **Quality control** at multiple stages ensures reliable downstream analysis
6. **Technology choice** depends on biological questions, budget, and timeline
7. **Experimental design** (replicates, depth, controls) is as important as sequencing technology

---

## Exercises

### Beginner

1. **Microarray vs. NGS**: What are two major advantages of RNA-seq over microarray gene expression profiling?

2. **Phred Scores**: A position in a read has a Q score of 30. What is the error probability at this position?

3. **Platform Comparison**: You want to fully characterize transcript isoforms in your samples. Would you choose Illumina short-read or PacBio long-read sequencing? Why?

### Intermediate

4. **Library Complexity**: Explain why PCR over-amplification during library prep can bias quantification results.

5. **Single-Cell Barcoding**: In 10x Chromium, what do the cell barcode and UMI each represent? Why do you need both?

6. **Depth vs. Replication**: Your budget allows either (a) deeply sequencing 3 replicates or (b) shallowly sequencing 6 replicates. Which is more appropriate for differential expression analysis? Why?

### Advanced

7. **Quality Score Calculation**: Derive the relationship between error probability and Phred score. If you want 99.99% accuracy (Q40), what is the tolerance for errors across a 100 bp read?

8. **Pseudoalignment vs. Alignment**: Suppose a read maps equally well to two different genes (homologous regions). How might an alignment-based approach vs. pseudoalignment approach handle this differently?

9. **Batch Effect Design**: You are preparing to sequence 100 samples across different RNA extractions, library prep batches, and sequencing runs. Design an experimental layout that allows you to estimate and correct for technical batch effects.

---

## Further Reading

### Reviews & Methodology Papers

- Stark, R., Grzelak, M., & Hadfield, J. (2019). "RNA sequencing: the teenage years." *Nature Reviews Molecular Cell Biology*, 20(11), 631-656.
- Ozsolak, F., & Milos, P. M. (2011). "RNA sequencing: advances, challenges and opportunities." *Nature Reviews Genetics*, 12(2), 87-98.
- Andrews, S. (2010). "FastQC: A quality control tool for high throughput sequence data." *Babraham Bioinformatics*, available online.

### Platform-Specific Papers

- **Illumina**: Goodwin, S., McPherson, J. D., & McCombie, W. R. (2016). "Coming of age: ten years of next-generation sequencing technologies." *Nature Reviews Genetics*, 17(6), 333-351.
- **PacBio**: Wenger, A. M., et al. (2020). "Accurate circular consensus long-read sequencing improves variant calling and assembly of a human genome." *Nature Biotechnology*, 38(10), 1155-1164.
- **Nanopore**: Jain, M., et al. (2018). "Nanopore sequencing and assembly of a human genome with ultra-long reads." *Nature Biotechnology*, 36(4), 338-345.
- **10x Chromium**: Zheng, G. X., et al. (2017). "Massively parallel digital transcriptional profiling of single cells." *Nature Communications*, 8, 14049.

### Quality Control
- Chen, S., Zhou, Y., Chen, Y., & Gu, J. (2018). "fastp: an ultra-fast all-in-one FASTQ preprocessor." *Bioinformatics*, 34(17), i884-i890.

---

**Navigation**: [← Previous: Molecular Biology Fundamentals](./01-molecular-biology-fundamentals.md) | [Next: RNA-seq Basics →](./03-bulk-rnaseq-basics.md)
