# Computational Biology Textbook: Creation Status & Guide

**Status as of August 13, 2026**

---

## ✅ Completed Sections

### **Part I: Foundations**
Complete foundational knowledge for understanding transcriptomics.

#### Chapter 1: Molecular Biology Fundamentals ✅
**Topics:**
- Central dogma (DNA → RNA → Protein)
- Gene structure and regulation
- RNA processing (5' capping, splicing, 3' polyadenylation)
- Different RNA types (mRNA, rRNA, tRNA, ncRNA, miRNA, lncRNA)
- Post-transcriptional regulation
- Gene expression variation across cell types
- Connection to transcriptomics experiments

**Pedagogical features:**
- Learning objectives, overview, detailed mechanisms
- Case studies linking molecular biology to transcriptomics
- 9 exercises (Beginner, Intermediate, Advanced)
- Further reading with 5+ key papers

---

#### Chapter 2: High-Throughput Sequencing Overview ✅
**Topics:**
- Microarray → NGS transition
- DNA sequencing fundamentals (cluster generation, base calling, quality scores)
- Major platforms:
  - Illumina (short-read, high throughput)
  - PacBio (long-read, accurate)
  - Oxford Nanopore (ultra-long reads)
  - 10x Chromium (single-cell barcoding)
- Library preparation for transcriptomics
- Quality control (pre- and post-sequencing)
- Mapping and quantification workflow
- Experimental design considerations

**Pedagogical features:**
- Detailed workflow diagrams
- Platform comparison tables
- Decision trees for technology selection
- 9 exercises covering theory to practical design
- Recent literature (2023-2026 advances)

---

#### Chapter 3: RNA-seq: Theory and Practice ✅
**Topics:**
- Read counting model (normalization factors)
- Factors affecting read counts (gene length, library depth, composition, GC bias)
- Normalization methods (CPM, RPKM, TPM, TMM, quantile, VST)
- Technical bias handling (GC content, batch effects, strand specificity)
- Differential expression analysis:
  - Negative binomial model
  - Multiple testing correction (Bonferroni, FDR, q-values)
  - Effect size (log fold-change)
- Key tools (Kallisto, Salmon, edgeR, DESeq2, Limma-Voom)
- Best practices in experimental design
- Validation strategies

**Pedagogical features:**
- Mathematical models with clear notation
- Normalization method comparison matrix
- Case study: comparing sample types
- 9 exercises from basic concepts to advanced analysis
- Practical software recommendations

---

### **Part II: Single-Cell Transcriptomics** (Partial)

#### Chapter 4: Single-Cell RNA-seq Technologies ✅
**Topics:**
- Why single-cell transcriptomics is necessary
- Limitations of bulk RNA-seq
- Droplet-based methods (10x Chromium):
  - Barcode design (16 bp cell ID)
  - UMI (Unique Molecular Identifiers)
  - Capture efficiency and doublets
- Plate-based methods (SMART-seq, CEL-seq)
  - Full-length transcript capture
- Emerging long-read single-cell (PacBio, Nanopore)
- Platform comparison matrix
- Batch effects and integration
- QC at platform level

**Pedagogical features:**
- Workflow diagrams for droplet and plate methods
- Platform decision tree
- Technology comparison table
- 9 exercises covering all technical aspects
- Recent advances (2023-2026)

---

### **Part III: Spatial Transcriptomics** (Partial)

#### Chapter 11: Spatial Transcriptomics: Technologies & Methods ✅
**Topics:**
- Biological motivation for spatial analysis
- Array-based methods (10x Visium):
  - 55 μm resolution, genome-wide coverage
  - Spot deconvolution strategies
- High-resolution FISH methods:
  - smFISH (single molecule)
  - MERFISH (100-500 genes, multiplexed)
  - seqFISH+ (imputation to 15K genes)
- In situ sequencing (ISS)
- Spatial analysis workflows:
  - Image registration
  - QC metrics
  - Spatial statistics (Moran's I, hotspots)
  - Dimensionality reduction for spatial data
- Integration with scRNA-seq
- Case study: tumor microenvironment

**Pedagogical features:**
- Throughput vs. resolution comparison plot
- Detailed workflow descriptions for each platform
- Spatial statistics explanation
- 9 exercises from basic concepts to analysis design
- Recent methods (2023-2026)

---

## 📊 Notebooks & Practical Examples

#### Notebook 1: scRNA-seq Data Loading, QC, and Initial Analysis ✅
**Location:** `/textbook/notebooks/01-scrna-basics-analysis.ipynb`

**Topics covered:**
1. Loading count matrices (AnnData format)
2. Quality control (library size, gene detection)
3. Cell filtering (low-quality cell removal)
4. Gene filtering (rare gene filtering)
5. Normalization (library size, log transformation)
6. Highly variable gene selection
7. Dimensionality reduction (PCA, UMAP)
8. Gene expression visualization
9. Leiden clustering
10. Results saving

**Features:**
- Runnable Python code with Scanpy library
- Uses synthetic data for demonstration
- Commented code explaining each step
- 10 self-contained sections
- Ready for adaptation with real data

---

## 🔄 In Progress / Planned

### Part II: Single-Cell Transcriptomics (Chapters 5-10)
- Chapter 5: Quality Control & Data Preprocessing
- Chapter 6: Normalization, Scaling & Batch Correction
- Chapter 7: Dimensionality Reduction
- Chapter 8: Clustering & Cell-Type Annotation
- Chapter 9: Trajectory Inference & Pseudotime
- Chapter 10: Gene Regulatory Networks & Co-expression

### Part III: Spatial Transcriptomics (Chapters 12-14)
- Chapter 12: Image Processing & Spot Detection
- Chapter 13: Spatial Analysis & Visualization
- Chapter 14: Integrating scRNA-seq with Spatial Data

### Part IV: Advanced Topics (Chapters 15-17)
- Chapter 15: Multimodal Integration & Joint Analysis
- Chapter 16: Scalability & Large-Scale Analysis
- Chapter 17: Case Studies & Research Applications

### Additional Resources
- Assignments (problem sets and coding exercises)
- Interactive tutorials (converting notebooks to lesson format)
- Further code examples for each chapter

---

## 📚 How to Use This Textbook

### For Students (Learning Path)

#### **Beginner Path (No RNA-seq background)**
1. Read Chapters 1-3 (Fundamentals)
2. Work through Notebook 1
3. Read Chapters 4-5 (scRNA-seq basics)
4. Complete associated exercises
5. Progress through rest of Part II sequentially

#### **Intermediate Path (Familiar with bulk RNA-seq)**
1. Skim Chapters 1-3 for refresher
2. Focus intensively on Chapters 4-8 (scRNA-seq)
3. Work through practical notebooks
4. Explore Part III (Spatial) in parallel or later

#### **Advanced Path (Experienced with scRNA-seq)**
1. Jump to specific chapters of interest
2. Skip to Part III (Spatial) and Part IV (Advanced)
3. Use case studies (Chapter 17) to apply knowledge

### For Instructors (Teaching Guide)

#### **Week-by-week suggestions:**

**Week 1-2:** Molecular biology fundamentals + sequencing overview
- Chapters 1-2
- Exercises (Beginner + Intermediate tier)

**Week 3-4:** Bulk RNA-seq methods
- Chapter 3
- Real data analysis problem set

**Week 5-6:** Single-cell technologies + QC
- Chapters 4-5
- Notebook 1 (hands-on)

**Week 7-8:** Normalization + Dimensionality reduction
- Chapters 6-7
- Code-along sessions

**Week 9-10:** Clustering + cell-type annotation
- Chapter 8
- Student project: Annotate their own dataset

**Week 11-12:** Spatial transcriptomics
- Chapters 11-14
- Integration lab combining scRNA-seq + spatial

**Week 13-14:** Advanced topics
- Chapters 15-17
- Student presentations on applications

---

## 🎯 Key Features of This Textbook

### 1. **Comprehensive Coverage (Recent Advances)**
- Single-cell RNA-seq methods (2020-2026)
- Spatial transcriptomics platforms (Visium, MERFISH, seqFISH+)
- Long-read technologies (PacBio, Nanopore)
- Emerging multimodal methods

### 2. **Pedagogical Design**
- Every chapter includes:
  - Clear learning objectives
  - Conceptual overview before deep dive
  - Real-world examples and case studies
  - Tiered exercises (Beginner → Intermediate → Advanced)
  - Key takeaways and summary
  - Curated further reading (~5-10 papers per chapter)

### 3. **Practical, Runnable Code**
- Jupyter notebooks with real analysis workflows
- Scanpy-based examples (Python standard)
- Reproducible and adaptable to user data
- Comments and explanations throughout

### 4. **Cross-Platform Perspective**
- Compares multiple technological approaches
- Discusses trade-offs (throughput vs. resolution, cost vs. depth)
- Decision trees for choosing appropriate methods

### 5. **Graduate-Level Rigor**
- Assumes prior bioinformatics training
- Mathematical models explained clearly
- Statistical testing and multiple correction
- Deep mechanistic understanding

---

## 📖 Chapter Overview Table

| Part | Chapter | Status | Pages* | Main Topics |
|------|---------|--------|--------|------------|
| I | 1. Molecular Biology | ✅ | 25 | Gene expression, regulation, RNA processing |
| I | 2. Sequencing Overview | ✅ | 30 | NGS fundamentals, platforms, library prep |
| I | 3. RNA-seq Methods | ✅ | 35 | Normalization, DE analysis, QC |
| II | 4. scRNA Technologies | ✅ | 28 | Droplet & plate methods, UMIs, platforms |
| II | 5. QC & Preprocessing | ⏳ | ~25 | Cell filtering, gene filtering, metric calculation |
| II | 6. Normalization & Batch | ⏳ | ~30 | Normalization methods, batch correction strategies |
| II | 7. Dimensionality Reduction | ⏳ | ~25 | PCA, UMAP, t-SNE, visualization |
| II | 8. Clustering & Annotation | ⏳ | ~30 | Clustering algorithms, cell-type assignment |
| II | 9. Trajectory Inference | ⏳ | ~25 | Pseudotime, developmental paths |
| II | 10. Gene Networks | ⏳ | ~25 | Co-expression, GRNs, regulatory logic |
| III | 11. Spatial Technologies | ✅ | 32 | Visium, MERFISH, seqFISH+, ISS |
| III | 12. Image Processing | ⏳ | ~20 | Spot detection, segmentation, registration |
| III | 13. Spatial Analysis | ⏳ | ~25 | Statistics, visualization, hotspots |
| III | 14. scRNA-Spatial Integration | ⏳ | ~20 | Deconvolution, combined analysis |
| IV | 15. Multimodal Integration | ⏳ | ~25 | Integrating mRNA + protein + other modalities |
| IV | 16. Scalability | ⏳ | ~20 | Large-scale analysis, cloud computing |
| IV | 17. Case Studies | ⏳ | ~30 | Real research applications across domains |
| - | **Total** | **~43%** | **~400+** | Comprehensive graduate-level curriculum |

*Estimated page count (formatted as publication)

---

## 🛠️ How to Contribute

### Adding New Chapters
1. Use `CHAPTER_TEMPLATE.md` as starting point
2. Follow pedagogical format:
   - Learning objectives
   - Conceptual overview
   - Detailed methods/theory
   - Real examples
   - Exercises (3 tiers)
   - Key takeaways
   - Further reading
3. Include at least one figure description or flowchart
4. Ensure mathematical notation is clear (KaTeX compatible)

### Creating Assignments
1. Use `ASSIGNMENT_TEMPLATE.md`
2. Design multi-part problems
3. Include solution sketches (for instructors)
4. Provide real or synthetic datasets

### Contributing Code Examples
1. Create Jupyter notebooks in `/textbook/notebooks/`
2. Use standard libraries (Scanpy, Seurat equivalent in Python, etc.)
3. Include documentation and comments
4. Make reproducible with example data

---

## 📝 Citation & License

**When to cite this textbook:**

```bibtex
@book{CB2_Textbook,
  title={Computational Biology: A Primer on Molecular Biology \& Transcriptomics},
  author={[Contributors]},
  year={2026},
  url={https://github.com/mgtools/CB2}
}
```

**License:** [To be determined upon publication]

---

## 🎓 Learning Outcomes by End of Textbook

### Students will be able to:

**Conceptual Knowledge**
- Explain molecular mechanisms underlying transcriptomics
- Describe different transcriptomics platforms and their trade-offs
- Interpret statistical tests in RNA-seq analysis
- Design experiments using appropriate technologies

**Practical Skills**
- Process raw sequencing data (FASTQ → counts)
- Perform quality control on transcriptomics datasets
- Conduct differential expression analysis
- Perform unsupervised analysis (clustering, dimensionality reduction)
- Interpret spatial transcriptomics data
- Integrate multiple data types (scRNA + spatial + protein)

**Research Competency**
- Read and critically evaluate published transcriptomics papers
- Design novel transcriptomics experiments
- Troubleshoot common analysis problems
- Apply methods to their own research questions

---

## 📊 Dataset Resources

**Public datasets available for practice:**

1. **10x Genomics Datasets**
   - PBMC (peripheral blood mononuclear cells)
   - Brain cell atlas
   - Tumor atlas
   - Available: https://www.10xgenomics.com/resources/datasets

2. **Single Cell Transcriptomics Portal**
   - 800+ studies
   - https://www.singlecelltranscriptomics.org/

3. **Human Cell Atlas**
   - Large-scale tissue-specific atlases
   - https://www.humancellatlas.org/

4. **GEO/NCBI**
   - Any publicly available RNA-seq data
   - https://www.ncbi.nlm.nih.gov/geo/

**For Spatial:**
1. **10x Visium datasets** (Brain, FFPE tissues)
2. **Published MERFISH & seqFISH datasets**
3. **ISS datasets** from published papers

---

## 🔗 Related Resources

**Recommended External Tutorials:**
- Scanpy: https://scanpy.readthedocs.io/
- Seurat: https://satijalab.org/seurat/
- Bioconductor (R-based): https://bioconductor.org/
- Galaxy Training: https://training.galaxyproject.org/

**Key Journals for staying current:**
- *Nature Biotechnology* (methods)
- *Genome Biology* (open access, comprehensive)
- *Nucleic Acids Research* (annual software database)
- *Cell Reports Methods* (open access, methods-focused)
- *Briefings in Bioinformatics* (reviews and tutorials)

---

## ✉️ Contact & Feedback

We welcome feedback, corrections, and suggestions!

- **Report errors:** [GitHub Issues](https://github.com/mgtools/CB2/issues)
- **Suggest improvements:** [GitHub Discussions](https://github.com/mgtools/CB2/discussions)
- **Contribute:** [Pull Requests](https://github.com/mgtools/CB2/pulls)

---

**Last updated:** August 13, 2026

**Next milestone:** Complete Part II chapters (5-10) with associated notebooks and assignments.
