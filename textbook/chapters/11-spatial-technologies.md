# Chapter 11: Spatial Transcriptomics: Technologies & Methods

## Learning Objectives

By the end of this chapter, you should be able to:
1. Explain why spatial context matters for interpreting transcriptomics data
2. Compare major spatial transcriptomics platforms (Visium, MERFISH, seqFISH, etc.)
3. Understand the spatial-specific preprocessing and analysis workflows
4. Recognize trade-offs between resolution, throughput, and cost
5. Evaluate spatial methods for different biological questions

---

## 11.1 Why Spatial Transcriptomics?

### The Information Loss in Single-Cell Studies

**Standard scRNA-seq workflow:**
1. Dissociate tissue into single cells
2. Measure transcriptome per cell
3. Computationally infer spatial location (e.g., via deconvolution)

**Major loss: Spatial organization is destroyed**

### Biological Examples Where Space Matters

#### **Brain Development & Architecture**
- Cortical layering: Different neuronal types in distinct layers
- Bulk/scRNA-seq → Cannot distinguish layer-specific development
- Spatial transcriptomics → Resolve layer-specific gene expression programs

#### **Tumor Microenvironment**
- Cancer cells, immune infiltrate, stromal cells
- Single-cell clustering → Mix of cell types from different regions
- Spatial transcriptomics → See immune cell gradients from tumor edge to center

#### **Embryogenesis**
- Developmental gradients: Morphogen concentrations guide cell fate
- scRNA-seq → Cannot resolve gradient structure
- Spatial → Directly measure gene expression gradients

#### **Tissue Regeneration & Wound Response**
- Spatial zones: center → transition → normal tissue
- scRNA-seq → Averaged response across zones
- Spatial → Zone-specific gene program dynamics

### Types of Biological Questions Spatial Transcriptomics Answers

1. **What genes are expressed where?** (Gene-to-region mapping)
2. **What cell types occupy which regions?** (Spatial cell-type composition)
3. **What are the local cell-cell interactions?** (Gene expression gradients near neighbor cells)
4. **How does tissue architecture change in disease?** (Spatial reorganization)

---

## 11.2 Overview of Spatial Transcriptomics Platforms

Spatial methods can be categorized by **resolution** (smallest feature size) and **throughput**:

```
                THROUGHPUT (transcripts measured)
                    ↑
                    │
     100M+  ├──────────────────────────────
             │  FFPE + seq
             │  (in situ sequencing)
             │
      10M   ├──────Visium────────────────
             │  Array spots
             │
      1M    ├──MERFISH─────seqFISH──────
             │  Multiplex FISH
             │
     100K   └────smFISH──────────────────
             │
      1K    └─────────────────────→ RESOLUTION (μm)
             1       10      100
```

---

## 11.3 Array-Based Spatial (10x Visium)

### Technology Overview

**10x Visium** uses:
- Glass slide with grid of ~5,000 capture spots (2 mm² area)
- Each spot 55 μm diameter; ~1-10 cells per spot
- Poly-A RNA from tissue section hybridizes to spot-bound oligos
- Sequencing identifies which spot & which transcript
- Output: Gene counts per spot (similar to 10x scRNA-seq)

**Workflow:**

```
1. Fresh or frozen tissue section
    ↓ (Permeabilize)
2. Transcript capture on slide
    ↓ (Reverse transcription)
3. cDNA synthesis in situ
    ↓ (Second-strand synthesis & library prep)
4. Illumina sequencing
    ↓ (Read back: spot ID + transcript sequence)
5. Maps: gene expression heatmap over tissue image
```

### Key Features

#### **Strengths:**
- Standardized protocol (easy to adopt)
- Genome-wide coverage (~20,000 genes per sample)
- Reasonable cost (~$1,000-2,000 per sample)
- Compatible with FFPE sections (archived tissue)
- Mature analysis tools (spaceranger, Seurat, Squidpy)

#### **Limitations:**
- **Spot-level only**: 55 μm resolution; cannot resolve individual cell types within spot
- **Ambiguous cell identity**: Each spot contains ~2-10 cells; cannot distinguish which cell expresses what
- **Not truly single-cell**: Lost cell-level resolution compared to scRNA-seq
- **Low throughput**: Only one slide per experiment (~5,000 spots)

### Spot Deconvolution

**Major research direction:** Computationally decompose multi-cell spots into single-cell abundance estimates.

**Methods:**
- **RCTD** (Robust Cell Type Decomposition): Uses reference scRNA-seq to deconvolve spots
- **Seurat** integration: Anchor spots to single cells; predict cell type proportions
- **MuSiC**: Weighted non-negative least squares; assumes known cell-type signatures

**Input:**
- Spot-level gene expression (Visium)
- Single-cell reference transcriptome (from same tissue)

**Output:**
- Estimated fractional abundance of each cell type per spot
- Can then map back to estimate "pseudo" single-cell types

---

## 11.4 High-Resolution Fluorescence In Situ Hybridization (FISH)

### smFISH (Single Molecule FISH)

**Technology:** Fluorescent probes target individual RNA molecules

**Key specifications:**
- Resolution: ~200-500 nm (subcellular)
- Throughput: 10-100 genes per cell
- Cells per image: 100s-1000s
- Cost: Moderate (per probe set)

**Workflow:**
1. Design fluorescent probes (typically 20-50 oligos per RNA target)
2. Hybridize to fixed/permeabilized cells/tissue
3. Wash to remove unbound probes
4. Image via fluorescence microscopy
5. Count individual RNA molecules (bright spots)

**Output:** 
- Precise localization within cell (e.g., nuclear vs. cytoplasmic)
- Single-molecule sensitivity
- Limited gene throughput

**Best for:** Validating specific genes; studying subcellular localization

---

### MERFISH (Multiplexed Error-Robust FISH)

**Technology:** Sequential rounds of FISH with ~10-100 genes per round

**Key innovations:**
- **Round multiplexing**: Multiple sequential FISH rounds
- **Error correction**: Combinatorial barcode design (each gene has unique binary barcode across rounds)
- **Throughput**: ~100-500 genes detected simultaneously (after combining all rounds)
- **Resolution**: ~200-500 nm subcellular
- **Cells per experiment**: Thousands

**Workflow:**
1. Round 1: Hybridize multiplexed FISH probes (~20 genes; each with distinct fluorophore)
2. Image: Detect molecules; register coordinates
3. Wash/destain probes
4. Round 2: New set of probes (~20 genes)
5. Repeat ~5-25 times
6. Computational decoding: Assign each barcode to gene identity
7. Map all genes in single coordinate space

**Output:** 
- 100s of genes measured
- Subcellular resolution
- Thousands of cells per tissue section
- 3D stacks possible (for volumetric imaging)

**Advantages over Visium:**
- Higher resolution (subcellular)
- Unambiguous cell identity (know exactly which cell expresses gene)
- Many more genes detected per cell

**Disadvantages:**
- More expensive per sample
- Longer experimental timeline (multiple imaging rounds)
- Requires high-end microscopy equipment

**Major studies using MERFISH:**
- Brain cell-type mapping (Chen et al., 2015)
- Tumor microenvironment (Jackson et al., 2020)
- Developmental atlases

---

### seqFISH & seqFISH+ (Spatial Expression Quantified by Sequential FISH)

**Similar concept to MERFISH but with variations:**

**seqFISH:**
- Sequential FISH rounds
- ~250 genes typically
- Resolution: Subcellular
- Implementation: Can use polyA probe + readout (simpler than smFISH-based MERFISH)

**seqFISH+:**
- Integrates with scRNA-seq reference
- Can impute unmeasured genes
- ~15,000 gene expressions (original + imputed)
- Higher complexity; combines imaging + computational inference

**Use case:** Full transcriptome-scale spatial analysis at subcellular resolution (but with imputation uncertainty)

---

## 11.5 In Situ Sequencing (ISS)

**Alternative to FISH: Directly sequence RNA molecules in their location**

### Technology

**Process:**
1. Denature DNA (from cDNA)
2. Single-strand synthesis (anchored to tissue)
3. Sequencing-by-synthesis cycles (iterative nucleotide addition + imaging)
4. Each pixel in image = one RNA molecule; sequence read from fluorescence pattern

**Advantages:**
- No probe design needed (any sequence can be detected)
- Unbiased (no probe hybridization bias)
- Very high resolution (optical diffraction limit)

**Disadvantages:**
- Technically demanding (optical precision, many imaging rounds)
- Lower throughput per sample
- Higher cost per transcript
- Not yet as mature as Visium or MERFISH

---

## 11.6 Spatial Analysis Workflows

### Step 1: Image Registration & Spot Identification

**For Visium:**
- Automatic: Capture barcode locations pre-defined by 10x
- Register histology image to barcode array

**For MERFISH/seqFISH:**
- Detect puncta (spots = individual RNA molecules)
- Segment cells (nuclear/cytoplasmic boundaries)
- Assign molecules to cells (each puncta → nearest cell nucleus)

### Step 2: Quality Control

**Spatial-specific QC:**

| Metric | Target |
|--------|--------|
| **Spots with >0 counts** | >80% for Visium |
| **Median genes per spot** | >500 (Visium) or >1000 (MERFISH) |
| **Median UMI per spot** | >5,000 (Visium) |
| **Image quality** | No obvious damage, artifacts |
| **Alignment quality** | Good registration between image & barcode array |

### Step 3: Normalization & Transformation

**Similar to scRNA-seq but spatial-aware:**

- **Library size normalization** (CPM, RPKM, or similar)
- **Log transformation**
- **Batch correction** (if multiple slides/rounds)

**Spatial-specific consideration:** Account for spatial autocorrelation (neighboring spots are more similar than distant spots; violates independence assumption)

### Step 4: Spatial Variable Gene Selection

**Challenge:** Identify genes that vary significantly across space (not just randomly)

**Methods:**
- **Moran's I**: Measures spatial autocorrelation; genes with significant autocorrelation are spatially variable
- **Getis-Ord Gi**: Identifies hot spots (regions of high expression)
- **Autocorrelation-adjusted p-values**: Account for spatial dependence in multiple testing

**Tools:** SpatialDE, MERINGUE, Squidpy

### Step 5: Dimensionality Reduction & Visualization

**Standard approaches (adapted for space):**

- **PCA → UMAP**: On log-normalized expression
- **Direct spatial visualization**: Heatmap-style display on original tissue coordinates

**Unique opportunity:** Color each spot/cell by gene expression; overlay on histology image

```
Example output:
  ┌─────────────────────────┐
  │   Tissue Image          │
  │ ──  ▓▓▓▓▓  ──────       │
  │ │   ▓▓▓▓▓   ─────       │
  │ ▄   ▓▓▓▓▓  ─────▄       │
  │                         │
  │ Colored: Gene X expr    │
  │ (Red=high, Blue=low)    │
  └─────────────────────────┘
```

### Step 6: Cell-Type Annotation

**For spotted data (Visium):**
- Deconvolve using scRNA-seq reference (RCTD, MuSiC)
- Infer cell-type composition per spot

**For single-cell resolution (MERFISH):**
- Cluster cells by expression (standard scRNA-seq methods)
- Annotate clusters (marker genes or reference-based)

### Step 7: Spatial Statistics & Inference

**Spatial-specific analyses:**

#### **Neighborhood Analysis**
- Which cell types are neighbors? (hotspot detection)
- Do certain pairs of cell types co-localize? (or avoid each other?)
- Statistical test: Permutation test or Ripley's K

#### **Spatial Domain Detection**
- Identify contiguous regions of similar expression
- Methods: Leiden clustering on spatial graphs, spatial Moran's I + unsupervised clustering

#### **Transcriptional Gradients**
- Are there genes with expression gradients? (e.g., morphogen-like)
- Fit spatial trend models
- Identify genes with significant spatial trends

---

## 11.7 Integration: scRNA-seq + Spatial

### Why Integrate?

**Complementary information:**
- **scRNA-seq**: Cell-type resolution but spatial information lost
- **Spatial**: Preserve location but cell-type ambiguity in multi-cell spots

**Integrated approach:**
- Use scRNA-seq as reference (known cell types)
- Map spatial data to reference → Deconvolve spots into cell types
- Gain spatial insight into scRNA-seq-defined cell types

### Workflow

```
1. scRNA-seq: Identify cell types (Seurat clustering → marker genes → annotation)
2. Generate reference: Expression signature per cell type
3. Spatial data: Load (Visium, MERFISH, etc.)
4. Deconvolve: Use reference to map spatial -> cell type
5. Analyze: Spatially-resolved cell-type composition, interactions
```

**Tools:**
- **Seurat**: Integration workflow; anchor-based
- **RCTD**: Explicit deconvolution model
- **Tangram**: Aligned neural network mapping
- **Stereo-seq** integration: Handle cross-platform integration

---

## 11.8 Case Study: Spatial Analysis of a Tumor Section

**Scenario:** 
- Visium data from breast cancer section
- scRNA-seq reference from same tumor (dissociated)
- Goal: Map immune infiltration and stromal composition

**Workflow:**

1. **Load data:**
   - Visium counts + histology image
   - scRNA-seq reference with cell-type labels

2. **Preprocessing:**
   - QC filtering (Visium spots with >500 genes)
   - Normalization (CPM + log)
   - scRNA-seq: Ensure high-quality reference

3. **Deconvolution:**
   - RCTD or Seurat integration
   - Output: Estimated cell-type proportions per spot

4. **Visualization:**
   - Overlay cell-type composition on tissue image
   - Identify immune hotspots, stromal regions

5. **Spatial analysis:**
   - Immune cell composition varies by region?
   - Co-localization: Immune + cancer cells at margins?
   - Moran's I: Which genes show spatial clustering?

6. **Hypothesis generation:**
   - Immune-cold region: Design immunotherapy strategy
   - Immune-hot region: Predict response to checkpoint inhibitors

---

## Key Takeaways

1. **Spatial transcriptomics preserves tissue organization**, filling the gap between bulk and single-cell methods
2. **Array-based methods (Visium)** offer genome-wide coverage and cost-effectiveness; trade-off: limited resolution
3. **High-resolution FISH methods (MERFISH)** achieve subcellular precision; trade-off: limited gene throughput without imputation
4. **Spatial statistics** (Moran's I, hotspot detection, gradients) reveal organization principles
5. **Integration with scRNA-seq** deconvolves spot ambiguity and provides cell-type context
6. **Biological applications span** development, disease, tissue regeneration, and tumor biology
7. **Platform choice** depends on biological question: Do you need genome-wide coverage or single-cell resolution?

---

## Exercises

### Beginner

1. **Spatial vs. Single-Cell**: What key biological information is lost when tissue is dissociated for scRNA-seq? How does spatial transcriptomics preserve this?

2. **Visium Resolution**: Visium spots are 55 μm in diameter; the brain cell soma is ~10-20 μm. Why does this create ambiguity in cell-type identification?

3. **MERFISH Throughput**: MERFISH uses ~5-25 sequential FISH rounds to detect ~500 genes. If each round detects 20 genes, why are so many rounds needed?

### Intermediate

4. **Spot Deconvolution**: Explain how RCTD uses a scRNA-seq reference to deconvolve multi-cell Visium spots into single-cell abundances.

5. **Spatial Autocorrelation**: Why is Moran's I test appropriate for identifying spatially-variable genes (rather than standard variance tests)?

6. **Tissue Artifacts**: Your Visium data shows a strong "stripes" pattern in expression. What could cause this? (Hint: consider technical factors.)

### Advanced

7. **Integration Design**: You have bulk RNA-seq, scRNA-seq, and Visium data from the same tissue. Design a computational workflow to leverage all three for maximum insight into cell-type-specific spatial organization.

8. **Power Calculation for Spatial**: You want to detect a hotspot of immune cells in tissue. Given ~5,000 Visium spots and ~10% spatial heterogeneity expected, estimate required effect size for 80% power.

9. **Multiplex FISH Barcode Design**: In seqFISH, each gene is assigned a binary barcode across 10 rounds (1 = red channel, 0 = no probe). How many unique barcodes can you design? What is the error-correction capability?

---

## Further Reading

### Reviews & Methods

- **Visium:** 10x Genomics Visium White Paper: "Visium Spatial Gene Expression"
- **MERFISH:** Chen, K. H., et al. (2015). "RNA imaging. Spatially resolved, highly multiplexed RNA profiling in single cells." *Science*, 348(6233), aaa6090.
- **seqFISH+:** Eng, C. L., et al. (2019). "Transcriptome-scale super-resolved imaging in tissues by RNA seqFISH+." *Nature*, 568(7751), 235-239.
- **Integration review:** Rao, A., Barkley, D., & Franç, G. (2021). "Exploring tissue architecture using spatial transcriptomics." *Nature*, 596(7871), 211-220.

### Analysis Tools & Software

- **Seurat** (spatial integration): Hao, Y., et al. (2021). "Integrated analysis of multimodal single-cell data." *Cell*, 184(13), 3573-3587.
- **Squidpy**: Palla, G., et al. (2022). "Squidpy: a scalable framework for spatial omics analysis." *Nature Methods*, 19(2), 171-178.
- **RCTD**: Cable, D. M., et al. (2021). "Robust decomposition of cell type mixtures in spatial transcriptomics data." *Nature Methods*, 18(4), 424-430.

### Applications & Case Studies

- **Tumor microenvironment:** Jackson, H. W., et al. (2020). "The single-cell pathology of synovial inflammation in rheumatoid arthritis." *Nature Communications*, 11(1), 1676.
- **Brain architecture:** Moffitt, J. R., et al. (2018). "Molecular, spatial, and functional single-cell profiling of the hypothalamic preoptic region." *Science*, 362(6416), eaau5324.

---

**Navigation**: [← Previous: Trajectory Inference](./09-trajectory-inference.md) | [Next: Image Processing & Spot Detection →](./12-image-processing.md)
