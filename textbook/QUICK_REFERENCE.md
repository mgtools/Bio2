# Quick Reference Guide: Computational Biology Textbook

## 🚀 Getting Started

### For Students: Which Chapter Should I Read?

**New to molecular biology?**
→ Start with Chapter 1 (Molecular Biology Fundamentals)

**Familiar with bulk RNA-seq?**
→ Start with Chapter 4 (scRNA-seq Technologies)

**Want to analyze your own data?**
→ Go to Notebook 1 immediately; return to chapters for theory

**Interested in spatial transcriptomics?**
→ Skim Chapters 1-3 and Chapter 4, then jump to Chapter 11

---

## 📚 Chapter Quick Links

### Part I: Foundations
| Chapter | Duration | Difficulty | Key Question |
|---------|----------|-----------|--------------|
| [1. Molecular Biology](./chapters/01-molecular-biology-fundamentals.md) | 3 hours | Easy | What is gene expression at the molecular level? |
| [2. Sequencing Overview](./chapters/02-sequencing-overview.md) | 3 hours | Easy-Med | How do we measure RNA at scale? |
| [3. RNA-seq Methods](./chapters/03-bulk-rnaseq-basics.md) | 3 hours | Medium | How do we quantify and compare genes across samples? |

### Part II: Single-Cell Transcriptomics (Ready)
| Chapter | Duration | Difficulty | Key Question |
|---------|----------|-----------|--------------|
| [4. scRNA Technologies](./chapters/04-scrna-technologies.md) | 3 hours | Easy-Med | How do we measure transcriptomes of individual cells? |
| 5. QC & Preprocessing | *Coming* | Medium | How do we filter and process single-cell data? |
| 6. Normalization & Batch | *Coming* | Medium | How do we correct for technical variations? |
| 7. Dimensionality Reduction | *Coming* | Medium | How do we visualize high-dimensional data? |
| 8. Clustering & Annotation | *Coming* | Hard | How do we identify and label cell types? |
| 9. Trajectory Inference | *Coming* | Hard | How do cells change state over time? |
| 10. Gene Networks | *Coming* | Hard | Which genes regulate which other genes? |

### Part III: Spatial Transcriptomics (Ready)
| Chapter | Duration | Difficulty | Key Question |
|---------|----------|-----------|--------------|
| [11. Spatial Technologies](./chapters/11-spatial-technologies.md) | 3 hours | Easy-Med | How do we measure transcriptomes while preserving space? |
| 12. Image Processing | *Coming* | Medium | How do we process spatial imaging data? |
| 13. Spatial Analysis | *Coming* | Medium | How do we analyze spatial patterns? |
| 14. scRNA-Spatial Integration | *Coming* | Hard | How do we combine single-cell and spatial data? |

### Part IV: Advanced Topics (Coming)
| Chapter | Duration | Difficulty | Key Question |
|---------|----------|-----------|--------------|
| 15. Multimodal Integration | *Coming* | Hard | How do we combine mRNA + protein + other modalities? |
| 16. Scalability | *Coming* | Hard | How do we handle large-scale datasets? |
| 17. Case Studies | *Coming* | Variable | What real problems can we solve? |

---

## 💻 Practical Resources

### Notebooks
- **[Notebook 1: scRNA Basics & Analysis](./notebooks/01-scrna-basics-analysis.ipynb)**
  - 10 self-contained Python sections
  - Data loading → QC → normalization → clustering
  - ~1-2 hours to run and understand
  - Requires: Python 3.9+, Scanpy, Pandas, NumPy

### Setup
```bash
# Install dependencies
pip install scanpy pandas numpy matplotlib seaborn jupyter

# Launch Jupyter
jupyter notebook notebooks/01-scrna-basics-analysis.ipynb
```

### Datasets for Practice
See [STATUS_AND_GUIDE.md](./STATUS_AND_GUIDE.md#-dataset-resources) for public data links

---

## 🎯 Key Concepts by Chapter

### Molecular Biology (Chapter 1)
- **Central dogma**: DNA → RNA → Protein
- **Transcriptional regulation**: TFs, chromatin, enhancers
- **Post-transcriptional control**: mRNA stability, translation, localization
- **Cell type differences**: Different cells have different transcriptomes

### Sequencing Overview (Chapter 2)
- **Technology options**: Illumina, PacBio, Oxford Nanopore, 10x
- **Quality metrics**: Phred scores, library size, GC content
- **Read mapping**: Alignment vs. pseudoalignment
- **Design considerations**: Replication, depth, technology selection

### RNA-seq Methods (Chapter 3)
- **Read counting model**: Counts ∝ abundance (with caveats)
- **Normalization**: CPM, RPKM, TPM, TMM (each addresses different biases)
- **Differential expression**: Negative binomial GLM, multiple testing correction
- **Batch correction**: ComBat, SVA (if necessary)

### scRNA Technologies (Chapter 4)
- **Droplet revolution**: 10x Chromium with cell + UMI barcodes
- **UMI role**: Corrects PCR amplification bias
- **Plate-based alternative**: Full-length transcripts but lower throughput
- **Batch effects**: Prominent in scRNA; computational correction essential

### Spatial Transcriptomics (Chapter 11)
- **Why space matters**: Cell-cell interactions, gradients, organization
- **Visium**: Genome-wide, low resolution (55 μm), moderate cost
- **MERFISH**: High resolution, ~500 genes, expensive, beautiful data
- **Integration**: Combine spatial + scRNA-seq for interpretation

---

## 🧮 Mathematical Concepts Reference

### Important Equations

**Phred Quality Score:**
$$Q = -10 \log_{10}(P_e)$$
*Q30 = 99.9% accuracy*

**Negative Binomial (scRNA-seq model):**
$$Y \sim \text{NegBinom}(\mu, \phi)$$
*Variance = mean + φ × mean²*

**Log-Fold-Change (DE analysis):**
$$\text{LFC} = \log_2 \left( \frac{\text{Expr}_{\text{treatment}}}{\text{Expr}_{\text{control}}} \right)$$
*LFC=1 → 2-fold change*

**False Discovery Rate (Multiple testing):**
$$\text{FDR} = \frac{\text{False positives}}{\text{Total positives}}$$
*Adjust p-values; keep FDR < 0.05*

**UMI Deduplication:**
- Count unique (barcode, UMI, sequence) triplets
- Collapse PCR duplicates to single molecule

**Moran's I (Spatial autocorrelation):**
$$I = \frac{n \sum_i \sum_j w_{ij}(x_i - \bar{x})(x_j - \bar{x})}{\sum_i (x_i - \bar{x})^2 \sum_i \sum_j w_{ij}}$$
*Ranges -1 to 1; > 0 = positive spatial correlation*

---

## 📊 Technology Comparison Cheat Sheet

### By Analysis Question

| Question | Best Technology |
|----------|-----------------|
| **Genome-wide baseline expression** | Bulk RNA-seq or 10x Visium |
| **Identify new cell types** | 10x scRNA-seq Chromium |
| **Isoform discovery** | PacBio long-read or SMART-seq |
| **Subcellular localization** | smFISH or MERFISH |
| **Spatial organization** | 10x Visium or MERFISH |
| **Rare cell isolation** | SMART-seq after sorting |
| **Ultra-large scale** | 10x Visium (spots) or Nanopore (reads) |
| **Cost-effective screening** | Bulk RNA-seq or 10x Visium |
| **Publication-quality microscopy** | MERFISH or seqFISH+ |

### By Throughput/Cost Tradeoff

**Highest throughput, lowest cost:**
- 10x scRNA-seq (~$1-5 per cell; 10,000+ cells)

**Balanced:**
- 10x Visium (~$1,000 per slide; 5,000 spots)

**Highest resolution, highest cost:**
- MERFISH (~$10,000+ per sample; 100-500 genes, subcellular)

---

## 🎓 Exercise Difficulty Levels

### Beginner (Conceptual)
*Time: 15-30 min*
- Explain basic concepts in your own words
- Define key terms
- Answer comprehension questions
- Example: "What is a UMI and why is it needed?"

### Intermediate (Application)
*Time: 30-60 min*
- Apply concepts to new scenarios
- Interpret results from example analyses
- Design simple experiments
- Example: "Why would droplet-based scRNA-seq fail for rare cells?"

### Advanced (Analysis & Design)
*Time: 1-3 hours*
- Derive equations or proofs
- Design complex experiments
- Troubleshoot realistic problems
- Example: "Design a computational workflow to integrate scRNA-seq + Visium data. Account for batch effects."

---

## 🔍 Troubleshooting Guide

### Data Quality Issues

**Symptom:** Many zeros in count matrix
- **Cause 1**: Sparse scRNA-seq data (normal; counts reflect stochastic expression)
- **Cause 2**: Low sequencing depth (solution: sequence deeper or filter cells)
- **Cause 3**: Poor cell quality (solution: improve dissociation/sorting)
- **Fix**: Inspect QC metrics (genes per cell, UMI per cell)

**Symptom:** One sample clusters separately from replicates
- **Cause 1**: Batch effect (different prep batch, sequencing run, person)
- **Cause 2**: Real biological difference (e.g., different disease state accidentally)
- **Fix**: Inspect metadata; apply ComBat if technical batch confirmed

**Symptom:** UMAP shows no clear clusters
- **Cause 1**: Too much noise; too few cells
- **Cause 2**: Over-normalization (lost biological signal)
- **Cause 3**: Homogeneous cell type (no distinct populations)
- **Fix**: Check QC; try different HVG thresholds; verify cell dissociation quality

### Analysis Issues

**Symptom:** Differential expression p-values all ~1.0
- **Cause**: Low power (too few replicates or very high variance)
- **Fix**: Collect more replicates; increase sequencing depth

**Symptom:** FDR-corrected p-values are very stringent (all >0.05)
- **Cause**: Multiple testing penalty; real effects present but underpowered
- **Fix**: Examine unadjusted p-values and effect sizes (LFC); pre-register hypotheses to reduce multiple testing burden

**Symptom:** Cell-type annotation doesn't match tissue biology
- **Cause 1**: Bad reference data or wrong reference tissue
- **Cause 2**: Contamination or mixed cell types in clusters
- **Cause 3**: Over-fitting to reference
- **Fix**: Inspect marker genes; compare to immunofluorescence; use multiple reference sources

---

## 📖 Reading Lists by Interest

### For Epidemiologists / Clinicians
1. Chapter 1 (molecular biology essentials)
2. Chapter 3 (bulk RNA-seq → disease understanding)
3. Chapter 17 (case studies in disease)

### For Computational Biologists
1. Chapter 3 (statistical methods)
2. Chapters 4-8 (full scRNA-seq pipeline)
3. Chapters 15-16 (advanced integration & scaling)

### For Cell Biologists / Developmental Biologists
1. Chapter 4 (single-cell necessity)
2. Chapter 9 (trajectory inference)
3. Chapter 11 (spatial transcriptomics)
4. Chapter 14 (combining spatial + scRNA-seq)

### For Immunologists
1. Chapter 4 (single-cell resolution for immune profiling)
2. Chapter 11 (spatial immune landscapes)
3. Case studies in Chapter 17 (immune responses)

---

## 🛠️ Software Ecosystem Quickstart

### Python Stack (Recommended)
```python
import scanpy as sc              # Single-cell analysis
import pandas as pd              # Data manipulation
import numpy as np               # Numerics
import matplotlib.pyplot as plt  # Plotting
import seaborn as sns            # Statistical visualization
```

**Key workflows:**
- Load: `adata = sc.read_h5ad('data.h5ad')`
- QC: `sc.pp.calculate_qc_metrics(adata)`
- Normalize: `sc.pp.normalize_total(adata); sc.pp.log1p(adata)`
- HVG: `sc.pp.highly_variable_genes(adata)`
- Reduce: `sc.tl.pca(adata); sc.tl.umap(adata)`
- Cluster: `sc.tl.leiden(adata)`

### R Stack (Alternative)
- **Seurat**: Comprehensive single-cell pipeline
- **SingleCellExperiment**: Standard data format
- **Bioconductor**: Gene expression and genomics tools

### Spatial-Specific Tools
- **Squidpy** (Python): Spatial analysis, neighborhood inference
- **Seurat v5** (R): Integration of spatial + scRNA-seq
- **MERFISH-related**: nuc-vist, merfishtools (varies by paper)

---

## 📱 Study Tips

### For Each Chapter
1. **First pass (1 hour)**: Read learning objectives and conceptual overview
2. **Deep dive (2 hours)**: Study detailed sections; take notes
3. **Practice (1-2 hours)**: Work through exercises; look up unfamiliar terms
4. **Consolidate (30 min)**: Review key takeaways; create summary

### For the Notebook
1. **Read first**: Understand what each cell does
2. **Run in order**: Dependencies between cells
3. **Modify it**: Change parameters; see what breaks
4. **Adapt it**: Replace data with your own

### For Exercises
1. **Beginner**: Before diving deep into chapter
2. **Intermediate**: After reading; applies what you learned
3. **Advanced**: Treat as capstone project; discuss with peers

---

## 🎯 20-Minute Crash Courses

**RNA-seq in 20 minutes:**
- Chapter 3, sections 3.1-3.3 (read counting, normalization)
- Skip deep statistics; focus on "why normalization matters"

**scRNA-seq in 20 minutes:**
- Chapter 4, sections 4.1-4.3 (why single-cell, droplet method, UMI)
- Skim rest

**Spatial transcriptomics in 20 minutes:**
- Chapter 11, sections 11.1-11.4 (motivation, Visium, MERFISH)
- Skip detailed analysis

---

## 📞 Getting Help

**Stuck on a concept?**
- Re-read the "Conceptual Overview" section of the chapter
- Check "Further Reading" for accessible review papers
- Email or post on course forum (if in classroom setting)

**Error in your code?**
- Check Notebook 1 for working examples
- Search error message online (StackOverflow, GitHub issues)
- Refer to software documentation (Scanpy docs, Seurat vignettes)

**Want real data to practice?**
- See [STATUS_AND_GUIDE.md](./STATUS_AND_GUIDE.md#-dataset-resources)
- Download from 10x Genomics, HCA, or GEO
- Start with PBMC dataset (smallest, easiest)

**Found an error in textbook?**
- Report on GitHub Issues
- Email textbook team
- Consider pull request with correction

---

## ⏱️ Time Estimates for Full Course

- **Part I (Chapters 1-3)**: 9 hours reading + 3 hours exercises + 2 hours lab = **14 hours**
- **Part II (Chapters 4-10)**: 21 hours reading + 6 hours exercises + 4 hours lab = **31 hours**
- **Part III (Chapters 11-14)**: 10 hours reading + 3 hours exercises + 3 hours lab = **16 hours**
- **Part IV (Chapters 15-17)**: 7.5 hours reading + 2 hours exercises + 5 hours case study = **14.5 hours**
- **Total**: **~75 hours** (one semester equivalent)

*Can be compressed to 5-6 weeks intensive (two weeks part-time); or extended over full semester*

---

## 🎓 Recommended Prerequisites

**Absolute Minimum:**
- Introductory molecular biology or biochemistry
- Basic statistics (mean, standard deviation, p-values)
- Comfort with command line (bash/terminal)
- Python or R programming

**Recommended:**
- Undergraduate-level genetics and molecular biology
- Statistics course covering hypothesis testing
- Previous exposure to bioinformatics or computational biology

**Not Required (but helpful):**
- Advanced mathematics (linear algebra for PCA/UMAP)
- Machine learning background
- System biology knowledge

---

**Last Updated:** August 13, 2026

**Have feedback?** Open an issue on [GitHub](https://github.com/mgtools/CB2/issues) or contact the textbook team.
