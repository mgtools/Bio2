# Computational Biology: A Primer on Molecular Biology & Transcriptomics

**A graduate-level digital textbook covering molecular biology fundamentals, single-cell transcriptomics, and spatial transcriptomics with recent experimental advances (2023-2026).**

---

## Textbook Overview

This textbook is designed for graduate-level students and researchers entering computational biology with prior bioinformatics training. It bridges molecular biology theory with cutting-edge computational methods for analyzing transcriptomic data.

### Key Topics
- **Molecular Biology Fundamentals**: Gene expression, transcription, RNA processing
- **High-Throughput Sequencing**: RNA-seq, bulk and single-cell approaches
- **Single-Cell Transcriptomics (scRNA-seq)**: Droplet-based methods, UMIs, data preprocessing, clustering, annotation
- **Trajectory Inference**: Pseudotime analysis, developmental trajectories
- **Spatial Transcriptomics**: Imaging-based and array-based methods (Visium, MERFISH, seqFISH)
- **Integration & Analysis**: Cross-modality data integration, case studies, best practices

### Target Audience
- Graduate students in computational biology, bioinformatics, or biomedical sciences
- Researchers transitioning to transcriptomic data analysis
- Those with prior programming and basic bioinformatics knowledge

---

## Table of Contents

### **Part I: Foundations** (Chapters 1-3)
Establish fundamental concepts in molecular biology and genomic sequencing.

1. [Molecular Biology Fundamentals](./chapters/01-molecular-biology-fundamentals.md)
2. [High-Throughput Sequencing Overview](./chapters/02-sequencing-overview.md)
3. [RNA-seq: Theory and Practice](./chapters/03-bulk-rnaseq-basics.md)

### **Part II: Single-Cell Transcriptomics** (Chapters 4-10)
Deep dive into scRNA-seq methods, analysis workflows, and recent advances.

4. [Single-Cell RNA-seq Technologies](./chapters/04-scrna-technologies.md)
5. [Quality Control & Data Preprocessing](./chapters/05-qc-preprocessing.md)
6. [Normalization, Scaling & Batch Correction](./chapters/06-normalization-batch.md)
7. [Dimensionality Reduction](./chapters/07-dimensionality-reduction.md)
8. [Clustering & Cell-Type Annotation](./chapters/08-clustering-annotation.md)
9. [Trajectory Inference & Pseudotime](./chapters/09-trajectory-inference.md)
10. [Gene Regulatory Networks & Co-expression](./chapters/10-gene-networks.md)

### **Part III: Spatial Transcriptomics** (Chapters 11-14)
Modern techniques for measuring gene expression while preserving spatial context.

11. [Spatial Transcriptomics: Technologies & Methods](./chapters/11-spatial-technologies.md)
12. [Image Processing & Spot/Cell Detection](./chapters/12-image-processing.md)
13. [Spatial Analysis & Visualization](./chapters/13-spatial-analysis.md)
14. [Integrating scRNA-seq with Spatial Data](./chapters/14-scRNA-spatial-integration.md)

### **Part IV: Advanced Topics** (Chapters 15-17)
Current cutting-edge methods and practical applications.

15. [Multimodal Integration & Joint Analysis](./chapters/15-multimodal-integration.md)
16. [Scalability & Large-Scale Analysis](./chapters/16-scalability.md)
17. [Case Studies & Research Applications](./chapters/17-case-studies.md)

---

## Learning Path

### For Beginners (No scRNA-seq background)
1. Start with **Part I** (Chapters 1-3) to build foundational knowledge
2. Progress through **Part II** (Chapters 4-8) sequentially
3. Explore **Part III** independently or in parallel with Part II

### For Intermediate Users (Familiar with bulk RNA-seq)
1. Skim **Chapter 1-3** for refresher
2. Focus on **Part II** (Chapters 4-10) for comprehensive scRNA-seq coverage
3. Combine with **Part III** for spatial analysis

### For Advanced Users (Experienced with scRNA-seq)
- Jump to relevant chapters in **Part II** for specific topics
- Explore **Part III** and **Part IV** for spatial and multimodal methods
- Use case studies (**Chapter 17**) to apply knowledge

---

## Pedagogical Features

Each chapter includes:
- **Learning Objectives**: Clear goals for the chapter
- **Conceptual Overview**: High-level explanation of key ideas
- **Methods & Algorithms**: Detailed technical descriptions with pseudo-code
- **Code Examples**: Python/R notebooks demonstrating workflows
- **Exercises**: Progressive difficulty (Beginner → Intermediate → Advanced)
- **Key Takeaways**: Summary of critical concepts
- **Further Reading**: Links to papers, tutorials, and resources
- **Figures & Diagrams**: Flowcharts, conceptual illustrations, and data visualizations

---

## Associated Resources

- **Jupyter Notebooks**: Runnable code examples for each chapter (see `./notebooks/`)
- **Assignments**: Problem sets and coding exercises (see `./assignments/`)
- **Datasets**: Public datasets used in examples (see `./datasets/`)
- **Code Utilities**: Helper functions and data processing scripts (see `./utils/`)

---

## Software & Prerequisites

### Required
- **Python 3.9+** or **R 4.0+**
- Jupyter Notebook / JupyterLab
- Git

### Common Libraries
- **Python**: pandas, numpy, scikit-learn, scanpy, seaborn, matplotlib
- **R**: Seurat, SingleCellExperiment, ggplot2, ComplexHeatmap

See [`setup/requirements.txt`](../setup/requirements.txt) for complete dependencies.

---

## How to Use This Textbook

1. **Read the Chapter**: Start with the markdown chapter file to understand concepts
2. **Run Code Examples**: Follow along with associated Jupyter notebooks
3. **Complete Exercises**: Work through exercises at your own pace
4. **Review Further Reading**: Explore linked papers and resources for deeper understanding
5. **Implement Workflows**: Apply learned methods to your own datasets

---

## Citation

If you use this textbook or code examples in your research, please cite:

```
[To be added upon publication]
```

---

## Contributing & Feedback

We welcome suggestions, corrections, and contributions! Please:
- Report errors via [GitHub Issues](https://github.com/mgtools/CB2/issues)
- Suggest improvements via [Pull Requests](https://github.com/mgtools/CB2/pulls)
- Contact the authors with major feedback

---

## License

[To be determined]

---

## Acknowledgments

This textbook incorporates methods and insights from:
- Leading single-cell genomics researchers
- Open-source tools like Scanpy, Seurat, and Bioconductor
- Community feedback and contributions

---

**Last Updated**: August 2026

For the latest version, visit: [GitHub Repository](https://github.com/mgtools/CB2)
