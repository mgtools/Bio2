# Chapter 1: Molecular Biology Fundamentals for Computational People

## Learning Objectives

By the end of this chapter, you should be able to:
1. Explain the central dogma as an information processing pipeline: DNA → RNA → Protein
2. Understand gene regulation as a computational system with inputs (signals) and outputs (expression levels)
3. Recognize that RNA is the "dataset" you're analyzing in transcriptomics; understand why it's noisy and variable
4. Know how cells transform molecular signals into data states you can measure
5. Understand why different cell types have different transcriptomes (like different software running on different machines)

---

## 1.1 Information Flow in Cells: A Computational Analogy

### The Basic Pipeline

Think of cells as computers running a genetic program:

```
┌─────────────────────────────────────────────────────┐
│         Cell as a Computer System                   │
├─────────────────────────────────────────────────────┤
│                                                     │
│  DNA = Hard drive (permanent storage)              │
│   ↓                                                 │
│  RNA = RAM (temporary working memory)              │
│   ↓                                                 │
│  Protein = Running process (executes functions)   │
│                                                     │
│  Input: Signals (hormones, growth factors, etc.)   │
│  Output: Gene expression levels (measurable data)  │
│                                                     │
└─────────────────────────────────────────────────────┘
```

**Key insight:** Transcriptomics measures RNA (the "working memory"), not DNA (permanent storage) or proteins (the running processes).

### Why RNA Instead of DNA or Proteins?

| Molecule | Stability | Information | Measurement Difficulty |
|----------|-----------|-------------|----------------------|
| **DNA** | Very stable; changes rarely | Static (same in all cells) | Hard; mostly constant |
| **RNA** | Temporary (hours); dynamic | **Varies by cell state** | **Easy to quantify** |
| **Protein** | Moderately stable | Functional output | Hard; low abundance; post-translational modifications |

**This is why we measure RNA:** It's the sweet spot—dynamic enough to reflect cellular state, but stable enough to measure reliably.

### The Central Dogma: Information Flow

```
DNA (Blueprint) → RNA (Working copy) → Protein (Function)
```

In computational terms:

### DNA Structure and Gene Organization

**DNA (deoxyribonucleic acid)** is a double-stranded molecule organized into chromosomes. Each chromosome contains:
- **Genes**: Coding sequences that specify proteins
- **Regulatory regions**: Promoters, enhancers, and silencers that control when genes are expressed
- **Non-coding DNA**: Intergenic sequences and other structural elements

A typical human gene consists of:
- **Promoter**: ~1 kb upstream of the transcription start site (TSS); contains binding sites for RNA polymerase II
- **Exons**: Protein-coding sequences (interrupted by introns)
- **Introns**: Non-coding sequences removed during RNA processing
- **Terminator**: Signals end of transcription

### RNA Synthesis: Transcription

**Transcription** is the process by which RNA polymerase reads a DNA template and synthesizes RNA in the 5' → 3' direction.

**Key Concepts:**
- **Template strand**: The DNA strand complementary to the RNA being synthesized
- **Coding strand**: The DNA strand with the same sequence as the RNA (except T instead of U)
- **Promoter binding**: RNA polymerase II (Pol II) binds to promoter regions and general transcription factors
- **Elongation**: Pol II moves along the template, incorporating ribonucleotides
- **Termination**: Specific signals (e.g., polyadenylation signals) halt transcription

**In eukaryotes**, transcription is regulated by:
- **Transcription factors (TFs)**: Proteins that bind DNA and recruit or block Pol II
- **Chromatin structure**: DNA packaging around histones affects accessibility
- **Epigenetic modifications**: DNA methylation and histone acetylation modulate gene expression

### From RNA to Protein: Translation

**Translation** converts mRNA into proteins using:
- **Ribosome**: Molecular machine that reads mRNA codons
- **tRNA**: Adapter molecules carrying amino acids
- **Codon-anticodon pairing**: Each 3-nucleotide codon on mRNA specifies an amino acid

**Key Points for Transcriptomics:**
- We measure **mRNA abundance**, which correlates (but imperfectly) with protein levels
- Protein synthesis is regulated separately from transcription (post-transcriptional control)
- Some genes produce regulatory RNAs (miRNA, lncRNA) rather than proteins

---

## 1.2 RNA Processing and Modifications

In eukaryotes, nascent RNA (pre-mRNA) undergoes extensive processing before becoming mature mRNA:

### 5' Capping

Immediately after transcription initiation:
- A **7-methylguanosine cap** is added to the 5' end of the pre-mRNA
- Function: Protects mRNA from degradation, aids in ribosome binding, facilitates splicing

**Impact on Transcriptomics:**
- Most sequencing methods target polyadenylated transcripts; alternative 5' modifications may be missed
- Cap-switching and other methods can detect 5' UTR variants

### 3' Polyadenylation (Poly-A Tailing)

At the 3' end:
- A consensus sequence (typically AAUAAA) signals the cleavage and polyadenylation machinery
- ~200 adenine nucleotides are added (**poly(A) tail**)
- Function: Protects mRNA from degradation and aids in export from the nucleus

**Impact on Transcriptomics:**
- Poly(A) enrichment is standard in most RNA-seq protocols
- Non-polyadenylated transcripts may be underrepresented
- Poly(A) tail length affects mRNA stability and translation efficiency (can vary by cell type and condition)

### Splicing

**Pre-mRNA contains introns (non-coding) and exons (coding).** During splicing:
- The spliceosome (a large ribonucleoprotein complex) recognizes intron-exon boundaries
- Introns are removed; exons are joined together
- Produces mature mRNA

**Alternative splicing:**
- Multiple exons can be included or excluded from the final transcript
- Results in **protein isoforms** from a single gene
- Highly regulated and tissue/condition-specific

**Genetic Code for Splice Sites:**
- **5' splice site**: GT (donor site)
- **3' splice site**: AG (acceptor site)
- **Branch point**: Intronic sequence 20-50 nt upstream of 3' splice site

**Impact on Transcriptomics:**
- Short-read sequencing may not resolve full isoform structure
- Long-read technologies (PacBio, Oxford Nanopore) can capture full-length transcripts
- Exon-exon junction quantification reveals isoform-specific expression

### Other RNA Modifications

Beyond the major processing events:
- **Internal modifications**: m6A, pseudouridine, inosine (detected by specialized methods)
- **UTR modifications**: Alternative promoters and polyadenylation create transcript diversity
- **Circular RNAs (circRNAs)**: Rare in standard RNA-seq but increasingly recognized

---

## 1.3 Gene Expression: Regulation

### Transcriptional Regulation

Gene expression is controlled at multiple levels:

#### 1. **Chromatin Accessibility**
- **Heterochromatin**: Tightly packed DNA; generally transcriptionally silent
- **Euchromatin**: Open DNA; accessible to transcription machinery
- **Histone modifications**: H3K4me3 (active), H3K27me3 (repressed), etc.
- **Tools to measure**: ATAC-seq, ChIP-seq, DNase-seq

#### 2. **Transcription Factor Binding**
- **Promoter-proximal TFs**: Bind within ~1 kb of TSS
- **Enhancer elements**: Bind tissue- or condition-specific TFs; can be far from gene (>100 kb away)
- **TF networks**: Multiple TFs work together to regulate genes
- **Tools to measure**: ChIP-seq, ATAC-seq, in situ hybridization

#### 3. **RNA Polymerase Recruitment and Initiation**
- Mediator complex bridges TFs and Pol II
- Paused Pol II: Many genes have Pol II at the TSS but don't actively elongate
- P-TEFb complex: Promotes productive elongation

#### 4. **Elongation Control**
- Pausing factors (DSIF, NELF) and elongation factors (P-TEFb, FACT) regulate Pol II speed
- Affects total transcript output

### Post-Transcriptional Regulation

After transcription, gene expression is further regulated by:

#### 1. **mRNA Stability**
- **5' and 3' UTRs** contain regulatory sequences
- **RNA-binding proteins (RBPs)** stabilize or destabilize transcripts
- **microRNAs (miRNAs)** can trigger deadenylation and decay
- **Nonsense-mediated decay (NMD)**: Quality control mechanism targeting truncated transcripts
- **Half-life**: Varies from minutes to hours; affects steady-state mRNA levels

#### 2. **RNA Localization**
- Some mRNAs are localized to specific cellular regions
- Affects local protein synthesis

#### 3. **Translation Control**
- **Codon usage bias**: Optimal codons → faster translation
- **uORFs (upstream ORFs)**: Can inhibit main protein synthesis
- **IRES (internal ribosome entry sites)**: Permit cap-independent translation
- **miRNAs**: Can block ribosome access

**Key insight for transcriptomics:**
Measuring mRNA abundance gives an incomplete picture of gene expression; protein levels may differ substantially.

---

## 1.4 Types of RNA Molecules

Not all transcribed RNA is messenger RNA (mRNA). A cell produces multiple RNA species:

### 1. **Messenger RNA (mRNA)**
- Encode proteins
- Typically 0.5–5 kb (eukaryotic mRNAs)
- ~3-5% of total cellular RNA

### 2. **Ribosomal RNA (rRNA)**
- Components of the ribosome
- Highly abundant (~50-80% of total RNA)
- Generally not analyzed in standard RNA-seq (removed by rRNA depletion)

### 3. **Transfer RNA (tRNA)**
- Adapter molecules in protein synthesis
- Highly abundant (~10% of total RNA)
- Variable in standard RNA-seq (depends on poly-A tail)

### 4. **Non-Coding RNAs (ncRNAs)**

**MicroRNAs (miRNAs):**
- 18-25 nucleotides
- Regulate gene expression by binding to mRNA 3' UTRs
- Typically ~300 human miRNAs; each targets hundreds of mRNAs

**Long Non-Coding RNAs (lncRNAs):**
- >200 nucleotides
- Diverse functions: scaffold TFs, sponge miRNAs, regulate chromatin
- Thousands in the human genome; many tissue-specific

**Circular RNAs (circRNAs):**
- Formed by backsplicing (exon 2 spliced to exon 1)
- Can act as miRNA sponges or protein scaffolds
- Enriched in some tissues (e.g., neurons)

**Small nucleolar RNAs (snoRNAs):**
- Guide chemical modifications of rRNA
- Part of snoRNPs (small nucleolar ribonucleoproteins)

**Piwi-interacting RNAs (piRNAs):**
- Silence transposable elements in germline cells
- 24-31 nucleotides

---

## 1.5 Gene Expression Variation Across Cell Types

A central principle in modern biology: **cells in the same organism have different transcriptomes**.

### Cell-Type-Specific Expression

Different cell types maintain distinct transcriptional profiles:
- **Neuron**: High expression of neurotransmitter genes, ion channels
- **Muscle**: High myosin, actin, metabolic genes
- **Immune cell**: High expression of cytokines, antigen presentation genes

This variation arises from:
- **Differential TF activity**: Different cells activate different TFs during development
- **Stable epigenetic marks**: Maintained through cell division
- **Environmental signals**: Cytokines, growth factors, cell-cell contacts

### Developmental Transitions

Cells change transcriptional state during development:
- **Lineage commitment**: Progressive restriction of cell fate options
- **Differentiation**: Cell acquires specialized properties (e.g., fibroblast → osteoblast)
- **Transdifferentiation**: Direct conversion without intermediate state (rare)

---

## 1.6 Connecting Molecular Biology to Transcriptomics Experiments

### Why Measure RNA?

RNA abundance reflects:
- Active genes in a given cell type or condition
- Regulatory responses to stimuli
- Developmental state and lineage commitment
- Disease perturbations

### Limitations of RNA-Based Measures

**Important caveat**: mRNA abundance ≠ protein abundance

**Reasons:**
- Different mRNA half-lives
- Variable translation efficiency
- Post-translational modifications and protein stability
- Subcellular localization

**Consequence**: 
- Protein measurements (immunofluorescence, Western blot, flow cytometry, mass spectrometry) are often needed to validate transcriptomic findings

### Experimental Readouts in Transcriptomics

Different experiments capture different aspects of gene regulation:

| Method | Measures | Resolution |
|--------|----------|-----------|
| **Bulk RNA-seq** | Average mRNA per sample | Per gene |
| **scRNA-seq** | mRNA per individual cell | Per cell |
| **Spatial Transcriptomics** | mRNA with spatial coordinates | Per spot or cell |
| **Single-Molecule FISH** | Individual RNA molecules | Single molecule |
| **ChIP-seq** | TF binding sites | Per genomic region |
| **ATAC-seq** | Chromatin accessibility | Per genomic region |
| **Ribosome Profiling** | Actively translated mRNAs | Per gene |

---

## Key Takeaways

1. **Gene expression flows from DNA to RNA to protein**, with RNA serving as the transient intermediate
2. **RNA processing** (capping, splicing, polyadenylation) profoundly shapes transcript diversity
3. **Transcriptional regulation** involves chromatin, transcription factors, and polymerase dynamics
4. **Post-transcriptional control** via RNA stability, localization, and translation further modulates protein synthesis
5. **Multiple RNA species** exist; mRNA represents a minority of total RNA
6. **Cell-type differences** in transcriptomics reveal developmental programs and cellular specialization
7. **RNA abundance ≠ protein abundance**; protein measurements validate transcriptomic findings

---

## Exercises

### Beginner

1. **Central Dogma**: In your own words, explain why transcriptomics captures only part of the gene expression picture (i.e., why RNA ≠ protein).

2. **RNA Processing**: List three major modifications that happen to eukaryotic pre-mRNA before it becomes mature mRNA. What is the function of each?

3. **RNA Types**: Name five types of RNA and briefly describe what each does in the cell.

### Intermediate

4. **Regulatory Variation**: A gene has a long half-life mRNA but low protein abundance. What post-transcriptional mechanisms could explain this?

5. **Alternative Splicing**: Two samples from the same tissue express different isoforms of the same gene. How might you experimentally distinguish which isoforms are present in each sample?

6. **Cell-Type Expression**: Sketch (conceptually) how the transcriptome of a neuron differs from that of a pancreatic β-cell. What categories of genes would be highly expressed vs. silent?

### Advanced

7. **Chromatin and Expression**: Describe how histone modification patterns (e.g., H3K4me3 at promoters, H3K27me3 in repressed regions) could be used to predict which genes are transcribed in a given cell type.

8. **RNA Dynamics**: mRNA production and degradation are continuous processes. Given a gene with production rate $r$ and degradation rate $\lambda$, what is the steady-state mRNA level? How would a sudden increase in $r$ (but not $\lambda$) affect dynamics?

9. **TF Circuitry**: Consider a developmental transition where TF A is downregulated and TF B is upregulated. If TF A represses TF B and TF B activates TF A, what feedback loop is this? Why might it favor robust transition?

---

## Further Reading

### Foundational Reviews
- Alberts, B., et al. (2002). *Molecular Biology of the Cell* (4th ed.). Garland Science. *(Classic textbook reference)*
- Cramer, P. (2019). "Eukaryotic transcription regulation." *Current Opinion in Genetics & Development*, 51, 126-131.

### Specific Topics
- **Transcription**: Revyakin, A., et al. (2012). "Single-molecule DNA unzipping and nanomechanical properties of DNA." *Nature Physics*, 8(9), 698-703.
- **Splicing**: Wahl, M. C., Will, C. L., & Lührmann, R. (2009). "The spliceosome: design principles of a dynamic RNP machine." *Cell*, 136(4), 701-718.
- **RNA Stability & Decay**: Søensen, V., & Holstege, F. C. P. (2018). "Global analysis of mRNA decay mechanisms." *Molecular Systems Biology*, 14(10), e8534.
- **miRNA**: Bartel, D. P. (2018). "Metazoan microRNAs." *Cell*, 173(1), 20-51.

### Recommended Review Articles
- Reddington, J. P., et al. (2015). "Non-coding RNAs and cancer." *Cell Research*, 25(3), 311-342.
- Djebali, S., et al. (2012). "Landscape of transcription in human cells." *Nature*, 489(7414), 101-108.

---

**Navigation**: [← Previous](#) | [Next: High-Throughput Sequencing Overview →](./02-sequencing-overview.md)
