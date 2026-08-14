# Single-Cell RNA-seq Technologies

## Learning Objectives

By the end of this chapter, you should be able to:
1. Explain why single-cell transcriptomics is necessary and complementary to bulk RNA-seq
2. Compare droplet-based, plate-based, and microfluidic scRNA-seq platforms
3. Understand the role of Unique Molecular Identifiers (UMIs) in quantification
4. Evaluate trade-offs between throughput, cost, and transcript detection
5. Choose appropriate platforms for different experimental designs

---

## Why Single-Cell Transcriptomics?

### The Limitation of Bulk RNA-seq

Bulk RNA-seq measures average expression across all cells in a sample:

**Example:** In a tissue sample with 1000 neurons and 9000 glial cells:
- A neuron-specific gene expressed in all neurons but no glia
- Bulk measurement: Diluted signal (10% of cells express it)
- Interpretation: Gene appears weakly expressed (or missed entirely)

**Missing information:**
- Which specific cell types express each gene?
- What is the distribution of expression within a cell type (bimodal? continuous?)?
- How do cell states transition during development or response to stimuli?

### The Single-Cell Solution

**Single-cell RNA-seq (scRNA-seq)** measures expression in individual cells:

$$\text{Transcriptome}_{\text{cell }} \to \text{Identifies cell type/state from expression profile}$$

**Advantages:**
1. **Cellular heterogeneity**: Reveal rare cell types and cell states
2. **No averaging**: Detect bimodal expression (e.g., ON/OFF switches)
3. **Developmental trajectories**: Track transcriptome changes through differentiation
4. **Disease mechanisms**: Identify which cells are affected in disease

**Trade-offs:**
- Higher per-cell cost than bulk
- Requires cell dissociation (may introduce artifacts)
- More complex computational analysis
- Sparse data (many zeros due to stochastic expression and/or low detection)

---

## Droplet-Based Methods: The 10x Revolution

### Overview

**Droplet-based platforms** capture individual cells in oil-in-water emulsions, achieving massive parallelization.

**Market leader:** 10x Genomics Chromium (dominates scRNA-seq landscape as of 2024)

**Key innovation:** Barcode-carrying beads in emulsions

### 10x Chromium Workflow

```
1. Cell suspension + barcode beads + oil/surfactant
    ↓ (Microfluidics creates emulsions)
2. Each droplet contains ~1 cell + ~1 barcode bead
    ↓ (Reverse transcription in droplet)
3. cDNA tagged with barcode + UMI + polyT
    ↓ (Emulsion broken; pool cDNA)
4. cDNA library amplified and tagmented
    ↓ (Illumina sequencing)
5. Each read tagged: [Barcode][UMI][cDNA]
```

### Key Components

#### **Barcode Design**
- **16 bp barcode**: Identifies which cell (droplet) the molecule came from
- **Barcode set**: ~4 million unique barcodes per gel bead
- **Collision rate**: ~1-2% of droplets share same barcode by chance (rare but real)
- **Resolution**: Enables >10,000 cells per channel (depending on capture efficiency)

#### **UMI (Unique Molecular Identifier)**
- **12 bp random sequence**: Marks individual RNA molecules
- **Purpose**: Distinguishes PCR duplicates from true abundance
- **Rationale**: PCR introduces exponential bias in copy number during amplification
- **Impact**: Without UMI, cannot distinguish 1 molecule amplified 100x from 100 different molecules

**Example:**
```
Original molecules:
  mRNA_1 → PCR → 50 copies of mRNA_1
  mRNA_2 → PCR → 30 copies of mRNA_2

Without UMI:
  Read count = [mRNA_1: 50, mRNA_2: 30]
  Inferred: mRNA_1 is more abundant (may be false!)

With UMI:
  Reads labeled [mRNA_1_UMI_A: 1, mRNA_1_UMI_B: 1, ..., mRNA_2_UMI_X: 1, ...]
  Collapse identical (barcode, UMI, sequence) → [mRNA_1: 1, mRNA_2: 1]
  Inferred: Both equally abundant (correct!)
```

#### **Capture Efficiency**
- **Design goal:** Each droplet captures ~1 cell
- **Poisson process**: Droplets follow Poisson distribution of cell numbers
- **In practice:** ~50-80% of droplets capture single cells; remainder empty or doublets
- **Doublet detection:** Computational methods to identify and flag dual-cell droplets

---

### Advantages of Droplet-Based Methods

| Advantage | Impact |
|-----------|--------|
| **High throughput** | 1000s-100,000s cells per run |
| **Cost-effective** | ~$1-5 per cell (all-in) |
| **Unbiased capture** | Random cell loading (no sorting bias) |
| **Standardized protocol** | Enables comparison across studies |
| **Mature ecosystem** | Extensive software for analysis |

### Limitations of Droplet-Based Methods

| Limitation | Consequence |
|-----------|-------------|
| **3' bias** | Captures poly-A tail; misses 5' regions (UMI-based) |
| **Shallow coverage per cell** | ~50K-500K reads total; sparse gene detection |
| **Doublets** | ~1-5% false positives (two cells in one droplet) |
| **Cell dissociation** | Stress response; rare cells may be lost |
| **Fixed barcode set** | Cannot design custom barcodes |
| **No transcript length** | Cannot resolve full-length isoforms (separate poly-A bias) |

---

## Other Major Platforms

### Plate-Based Methods

**Approach:** Isolate single cells into individual wells of a multi-well plate; reverse transcription occurs in parallel

**Examples:**
- **SMART-seq** (Switching Mechanism At 5' end of RNA Template)
- **CEL-seq** (Cell Expression by Linear amplification and Sequencing)

**Characteristics:**
- Fewer cells (~100-1000 per batch)
- Full-length transcript capture (no 3' bias)
- Higher per-cell cost than droplets
- Enables sorting for specific cell types beforehand

**Advantages:**
- Full-length transcripts → isoform resolution
- No PCR bias (uses in vitro amplification with CEL-seq)
- Compatible with sorted/rare cells

**Disadvantages:**
- Lower throughput
- More labor-intensive
- Higher per-cell cost

---

### Commercial Hybrid Platforms (2023-2026 Advances)

#### **10x 5' + VDJ (Immune Profiling)**
- Capture cell barcodes + UMIs
- Sequence both mRNA (5' end) and V(D)J segments
- Application: Map TCR/BCR sequences to transcriptomes

#### **10x Multimodal (CITE-seq integration)**
- Simultaneous capture of mRNA + antibody-tagged proteins
- Each antibody tagged with oligo barcode
- Application: Protein surface markers + transcriptomics

#### **BD Rhapsody**
- Similar throughput to 10x
- Microwell plate format
- More compatible with cryopreserved cells

#### **Parse Biosciences**
- Splitpool barcoding (multiple rounds of partitioning)
- Claims higher capture efficiency
- Newer to market

---

## Long-Read Single-Cell Methods (Emerging)

### Why Long-Read for Single Cells?

**Motivation:** Droplet-based 3' bias misses:
- Full-length isoform structure
- 5' UTR regulatory elements
- Alternative promoters

**Challenge:** Combining single-cell resolution with long reads

### Approaches

#### **PacBio SMRT-Link + Barcoding**
- Recently developed protocols capture cell barcodes + full-length cDNA
- Throughput: 100s to 1000s of cells
- Trade-off: More expensive than Illumina but isoform-resolved

#### **Oxford Nanopore Direct Capture**
- Direct RNA sequencing (no cDNA reverse transcription)
- Preserves RNA modifications (m6A, pseudouridine)
- Inherent barcode schemes still being developed

---

## Key Metrics for Platform Comparison

### Throughput
- **Cells per run:** 100s (plate) to 100,000s (droplets)
- **Total RNA molecules detected:** Impacts downstream analysis sensitivity

### Sequencing Depth Per Cell
- **Median reads per cell:** Affects detection power
  - 10x (scRNA-seq): ~50K-500K reads per cell
  - 10x (5' antibody): Similar; more concentrated on UTR
  - Plate-based (SMART-seq): ~1-5M reads per cell

### Cost
- **Total cost per cell (all-in):**
  - Droplet-based (10x): $1-5
  - Plate-based (SMART-seq): $10-50
  - As throughput increases, per-cell cost decreases

### Detection Efficiency
- **Genes detected per cell:**
  - 10x scRNA-seq: ~3,000-5,000 median (depends on depth)
  - SMART-seq: ~8,000-12,000 median
  - Nanopore: Potentially >10,000 (if sufficient reads)

### Bias
| Bias Type | Droplet | Plate |
|-----------|---------|-------|
| **3' bias** | High | Low (full-length) |
| **GC content** | Moderate | Low (SMART-seq less biased) |
| **Length bias** | Moderate | Low |
| **Amplification** | Mitigated by UMI | In vitro amplification (CEL-seq) |

---

## Experimental Design Considerations

### Choosing a Platform

**Decision tree:**

```
Goal: Comprehensive cell-type discovery in a tissue?
├─ YES, limited budget → 10x Chromium
├─ YES, high resolution → 10x + spatial integration
└─ NO → Consider alternatives

Goal: Isoform-level resolution?
├─ YES → Plate-based or PacBio single-cell
└─ NO → Droplet-based sufficient

Goal: Sorted/rare cell types?
├─ YES → Plate-based (SMART-seq) more practical
└─ NO → Droplet-based more cost-effective

Goal: Surface protein + transcriptome?
├─ YES → 10x Multimodal (CITE-seq)
└─ NO → mRNA-only (standard scRNA-seq)
```

### Sample Preparation

**Critical for data quality:**

| Step | Best Practice | Common Problem |
|------|---------------|-----------------|
| **Dissociation** | Optimize for tissue type | Over-dissociation → cell stress |
| **Viability** | >85% live cells recommended | Dead cells leak RNA → doublets/ambient RNA |
| **Cell concentration** | ~1000 cells/μL (10x) | Too few → more empty droplets |
| **Filtering** | Remove debris/clumps | Clumps → doublets |
| **Cryopreservation** | (if needed) Use specialized media | Poor viability post-thaw |

---

## Batch Integration & Technology Transfer

### Batch Effects in scRNA-seq

scRNA-seq is highly susceptible to technical batches:
- Different dissociation protocols
- Different cell sorters/FACS gates
- Different instruments
- Different sequencing runs
- Even different days with same protocol

**Impact:** Can dominate biological signal if not addressed

### Integration Methods (Preview)

Computational methods to correct batch effects:

- **Seurat CCA/harmony**: Canonical correlation analysis or harmonic alignment
- **scVI**: Variational autoencoders
- **Liger**: Joint matrix factorization
- **FastMNN**: Mutual nearest neighbors

**Key principle:** Match cells across batches that are similar in expression; correct batch shifts

*More details in the Batch Correction section.*

---

## Quality Control at Platform Level

### Pre-Sequencing QC (Cell-Level)

**For droplet-based:**
- Cell viability (>85%)
- Cell count and concentration
- No clumps/debris
- RNA quality (optional; Nanodrop/Qubit)

**For plate-based:**
- Individual cell isolation (visual confirmation)
- Viability per well
- RNA quality per cell (harder to assess)

### Post-Sequencing QC (Dataset-Level)

*Detailed in the Quality Control section, but preview here:*

- **Sequencing metrics:**
  - Per-barcode read distribution
  - UMI saturation (% of sequencing depth remained)
  - rRNA content (should be minimal in poly-A+ selection)

- **Cell-level QC:**
  - UMI per cell (gene library complexity)
  - Genes per cell
  - Mitochondrial fraction (>20% suggests stress/dying cells)
  - Doublet score

---

## Key Takeaways

1. **Single-cell transcriptomics** reveals cellular heterogeneity missed by bulk RNA-seq
2. **Droplet-based methods** (10x Chromium) dominate due to throughput and cost
3. **UMIs enable accurate quantification** by distinguishing PCR duplicates from true molecules
4. **Cell barcodes** enable computational deconvolution of thousands of cells in parallel
5. **3' bias** in UMI-based methods limits isoform resolution; plate-based methods capture full-length
6. **Trade-offs exist:** Throughput/cost vs. transcript coverage; choose based on biological question
7. **Batch effects are prominent** in scRNA-seq; computational integration is often necessary
8. **Platform selection** depends on experimental goals, budget, and downstream questions

---

## Exercises

### Beginner

1. **Droplet vs. Plate:** What is the main advantage of plate-based scRNA-seq methods over droplet-based approaches like 10x Chromium?

2. **UMI Function:** Explain how a UMI (Unique Molecular Identifier) helps distinguish real differences in transcript abundance from PCR amplification artifacts.

3. **Cell Barcode:** In 10x Chromium, what does a 16 bp cell barcode identify?

### Intermediate

4. **Doublet Problem:** In 10x scRNA-seq, ~2% of droplets capture two cells (doublets) instead of one. Why is this a problem, and how might you detect doublets computationally?

5. **3' Bias Trade-off:** Compare the advantages and disadvantages of 10x UMI-based 3' capture versus SMART-seq full-length capture. When would you choose each?

6. **Capture Efficiency:** If a 10x run is loaded at 10,000 cells, but the actual recovery is 7,000 cells (70% efficiency), what might cause the 30% loss? How would you diagnose this?

### Advanced

7. **UMI Saturation:** In a scRNA-seq experiment, you observe that UMI saturation (% of sequencing depth wasted on duplicate UMIs) is 40%. What does this tell you? How would you address it?

8. **Batch Integration Necessity:** Propose an experiment where you sequence the same tissue on two different days. Describe what computational batch correction step you would apply and why.

9. **Cost-Benefit Analysis:** Your lab can afford either (a) 10x run with 10,000 cells at moderate depth, or (b) SMART-seq of 500 sorted cells at very high depth. What factors would determine your choice?

---

## Further Reading

### Foundational scRNA-seq Reviews
- Hwang, B., Lee, J. H., & Bang, D. (2018). "Single-cell RNA sequencing technologies and bioinformatics pipelines." *Experimental & Molecular Medicine*, 50(7), 1-14.
- Lafzi, A., Moutinho, C., Picelli, S., & Heyn, H. (2018). "Tutorial: guidelines for the experimental design and computational analysis of single-cell RNA sequencing studies." *Nature Protocols*, 13(12), 2742-2756.

### Platform-Specific Papers
- **10x Chromium**: Zheng, G. X., et al. (2017). "Massively parallel digital transcriptional profiling of single cells." *Nature Communications*, 8, 14049.
- **SMART-seq**: Picelli, S., et al. (2013). "Smart-seq2 for sensitive full-length transcriptome profiling in single cells." *Nature Methods*, 10(11), 1096-1098.
- **CEL-seq**: Hashimshony, T., et al. (2012). "CEL-Seq: single-cell RNA-seq by multiplexed linear amplification." *Cell Reports*, 2(3), 666-673.

### UMI Technology
- Islam, S., et al. (2014). "Quantitative single-cell RNA-seq with unique molecular identifiers." *Nature Methods*, 11(2), 163-166.

### Long-Read Single-Cell (Emerging)
- Lebrigand, K., et al. (2020). "High clonality of primordial germ cells and frequent later clonal expansions." *Nature*, 547(7663), 326-330. (Example of long-read application)

---

**Related**: [Bulk RNA-seq Basics](./bulk-rnaseq-basics.md)
