# Chapter 3: RNA-seq: Theory and Practice

## Learning Objectives

By the end of this chapter, you should be able to:
1. Understand the read counting model and assumptions underlying RNA-seq quantification
2. Explain different normalization approaches and when each is appropriate
3. Perform differential expression analysis and interpret statistical results
4. Recognize technical biases in RNA-seq data and methods to mitigate them
5. Apply quality control best practices to RNA-seq datasets

---

## 3.1 From Reads to Counts

### The Counting Model

At its core, RNA-seq quantification rests on a simple premise:

**The number of reads mapped to a gene is proportional to the transcript abundance in the sample.**

$$\text{Count}_{gene} \propto \text{Abundance}_{gene}$$

However, this relationship is complicated by several factors:

### Factors Affecting Read Counts

#### 1. **Gene Length**
- Longer genes have more bases, hence more potential read mapping sites
- A 2 kb gene produces twice as many fragments as a 1 kb gene (all else equal)
- **Correction**: Normalize by gene length → **RPK** (Reads Per Kilobase)

#### 2. **Library Sequencing Depth**
- A sample with 100 million total reads will have higher counts than one with 50 million reads
- **Correction**: Normalize by total library size → **RPKM/FPKM** (per Million mapped reads)

#### 3. **RNA Composition**
- If one transcript is extremely abundant (e.g., hemoglobin in RBCs), it consumes sequencing capacity
- Other transcripts receive fewer reads, appearing depleted
- **Correction**: Use composition-aware methods (TMM, quantile normalization)

#### 4. **GC Content Bias**
- Illumina platforms show biased amplification for high-GC transcripts
- Low-GC and high-GC transcripts under- and over-represented
- **Correction**: GC-content normalization methods (conditional quantile normalization, loess)

#### 5. **Random Sampling Variation**
- Read counts follow approximately Poisson distribution (for low counts) or negative binomial (for high counts)
- Need statistical models to account for sampling noise

### The Count Data Model

For a given gene $g$ in sample $s$:

$$Y_{g,s} \sim \text{NegBinom}(\mu_{g,s}, \phi_g)$$

where:
- $Y_{g,s}$ = observed count
- $\mu_{g,s}$ = expected count (related to true expression)
- $\phi_g$ = dispersion parameter (variance/mean ratio)

The mean is often parameterized as:

$$\mu_{g,s} = L_s \cdot \theta_{g,s}$$

where:
- $L_s$ = library size normalization factor
- $\theta_{g,s}$ = gene expression level in sample $s$

---

## 3.2 Normalization Methods

Normalization aims to make counts comparable across samples by accounting for systematic biases.

### Library Size Normalization

#### **CPM (Counts Per Million)**
$$\text{CPM}_{g,s} = \frac{Y_{g,s}}{N_s / 10^6}$$

where $N_s$ = total reads in sample $s$.

**Advantages:** Simple, interpretable, standardized units
**Disadvantages:** Sensitive to highly expressed genes (composition bias)

#### **RPKM / FPKM (Reads/Fragments Per Kilobase per Million)**
$$\text{RPKM}_{g,s} = \frac{Y_{g,s} / L_g}{N_s / 10^6}$$

where $L_g$ = length of gene $g$ in kilobases.

**Advantages:** Accounts for gene length and library size
**Disadvantages:** Composition bias not fully addressed; difficult to compare across genes in same sample

#### **TPM (Transcripts Per Million)**
$$\text{TPM}_{g,s} = \frac{Y_{g,s} / L_g}{\sum_{g'} (Y_{g',s} / L_{g'})} \times 10^6$$

Conceptually: "If you sequenced 1 million transcripts in this sample, how many would be this gene?"

**Advantages:** 
- Accounts for gene length and library composition
- Sums to 1 million across a sample (interpretable)
- Better for cross-sample comparisons
**Disadvantages:** log-scale analysis requires pseudocounts

---

### Composition-Aware Normalization

These methods account for the fact that highly expressed genes monopolize sequencing capacity.

#### **TMM (Trimmed Mean of M-values)**

Core idea: Most genes are not differentially expressed. Use stable genes as reference to estimate library composition differences.

**Algorithm:**
1. Compute log-ratio of expression (M-value) for each gene compared to reference sample
2. Trim extreme M-values (e.g., remove top/bottom 30%)
3. Compute weighted mean of remaining M-values
4. This weighted mean is the TMM normalization factor

**Implementation:** edgeR package (Robinson & Oshlack, 2010)

#### **Quantile Normalization**

Assumption: The distribution of expression should be similar across samples

**Algorithm:**
1. Order genes by expression in each sample
2. For each rank, set all samples to have the average expression at that rank
3. Result: All samples have identical marginal distributions

**Advantages:** Removes distributional differences
**Disadvantages:** Strong assumption (not always biologically appropriate)

#### **Variance Stabilizing Transformation (VST)**

**Goal:** Transform data so variance is independent of mean

**Problem:** Raw counts have mean-dependent variance (Poisson-like)

**Solution:** 
- Estimate mean-variance relationship from data
- Apply transformation to stabilize variance
- Output: VST-normalized counts suitable for downstream analysis (clustering, visualization)

**Implementation:** DESeq2, limma packages

---

## 3.3 Handling Technical Biases

### GC Content Bias

**Observation:** 
- High-GC content genes show systematic over/under-representation
- Particularly pronounced in Illumina sequencing

**Causes:**
- Amplification bias during library prep
- Differential binding to flow cell

**Correction methods:**
- **Loess normalization**: Fit a smooth curve relating GC content to counts; subtract predicted bias
- **Conditional quantile normalization (CQN)**: Normalize jointly by GC content and gene length
- **Alignment-free quantification**: Some tools (e.g., Salmon) model biases explicitly

### Batch Effects

**Definition:** Systematic differences in measured expression between batches (samples prepared/sequenced together) that are not biological.

**Sources:**
- Different RNA extraction protocols
- Library prep batch (reagent lot changes)
- Sequencing run/flow cell
- Lane within flow cell
- PCR amplification differences

**Detection:**
- PCA: Batch should dominate the first PCs if large
- Heatmap of sample-sample correlations: Batch artifacts cluster samples together
- ComBat or removeBatchEffect (limma) to visualize

**Correction:**
- **ComBat** (Leek et al.): Empirical Bayes to remove batch effects
- **SVA (Surrogate Variable Analysis)**: Identify hidden batch-like variables; include as covariates
- **Remove Batch Effects (limma)**: Simple location/scale shift correction
- **Batch-aware downstream analysis**: Some methods (e.g., mixed models) can include batch as a covariate

**Caution:** Over-correction can remove real biology if confounded with batch

### Strand Specificity

**Directional library prep:** Records which strand transcripts came from

**Advantages:**
- Resolves ambiguous reads on overlapping genes
- Detects antisense transcription
- Reduces background from genomic DNA contamination

**Biases:**
- Different libraries have different strand biases
- Some genes inherently have strand bias (e.g., long non-coding RNAs)

---

## 3.4 Differential Expression Analysis

### The Research Question

**Standard goal:** Compare expression between conditions (e.g., treated vs. control)

$$H_0: \text{Expression is unchanged between conditions}$$
$$H_A: \text{Expression differs between conditions}$$

### Statistical Model for DE

Most methods use negative binomial GLM:

$$\log \mathbb{E}[Y_{g,s}] = \alpha_g + \beta_g x_s + \text{batch effects}$$

where:
- $\alpha_g$ = baseline expression for gene $g$
- $\beta_g$ = log-fold-change (LFC) for gene $g$
- $x_s$ = condition indicator (0 or 1)
- **Test:** Is $\beta_g$ significantly different from 0?

### Multiple Testing Correction

With ~20,000 genes tested, we expect many false positives by chance:

$$\text{Expected false positives at } \alpha=0.05: 20,000 \times 0.05 = 1,000$$

**Corrections:**

#### **Bonferroni**
- Adjust significance threshold: $\alpha' = \alpha / m$ (where $m$ = number of tests)
- Pros: Simple, controls family-wise error rate (FWER)
- Cons: Very conservative; many true discoveries missed

#### **Benjamini-Hochberg (FDR)**
- Order p-values; find largest $i$ where $p_{(i)} \le \frac{i \cdot \alpha}{m}$
- Pros: Controls false discovery rate (proportion of false positives among discoveries)
- Cons: Less stringent than FWER; may tolerate some false positives
- **Standard choice** in genomics (FDR < 0.05)

#### **q-values**
- Convert p-values to q-values (posterior probability of being false discovery)
- Interpretation: "At a q-value cutoff of 0.05, 5% of my hits are likely false positives"
- Implementation: qvalue package (Storey & Tibshirani)

### Effect Size (Fold-Change)

P-value alone is insufficient; also examine effect size:

$$\text{Log Fold-Change (LFC)} = \log_2 \left( \frac{\text{Abundance}_{\text{treated}}}{\text{Abundance}_{\text{control}}} \right)$$

**Interpretation:**
- LFC = 1 → 2-fold increase
- LFC = -1 → 2-fold decrease (0.5x)
- LFC = 0 → no change

**Practical significance:** 
- LFC > 1 (or < -1) often considered meaningful
- Combines with p-value for filtering: |LFC| > 1 AND adj. p-value < 0.05

---

## 3.5 Key Tools for RNA-seq Analysis

### Pseudoalignment & Quantification

- **Kallisto** (Bray et al., 2016): Fast, accurate quantification; outputs estimated counts and TPM
- **Salmon** (Patro et al., 2017): Improved over Kallisto; models sequence-specific biases
- **RSEM** (Li & Dewey, 2011): Full probabilistic model; handles isoform-level quantification

### Differential Expression

#### **edgeR** (Robinson et al., 2009)
- Negative binomial GLM framework
- TMM normalization
- Handles small sample sizes well
- Excellent for paired/complex designs

#### **DESeq2** (Love et al., 2014)
- Negative binomial GLM; VST normalization
- Robust to outliers
- lfcShrink: Shrinks log-fold-changes toward zero (reduces false positives from low-count genes)
- Very popular; extensive documentation

#### **Limma-Voom** (Law et al., 2014)
- Linear models framework
- Transforms counts to approximate normality
- Flexible for complex designs (paired samples, multiple factors)
- Fast; computationally efficient

### Visualization & QC

- **MultiQC** (Ewels et al., 2016): Aggregate FastQC and other QC reports
- **DESeq2 vst/rlog**: Stabilizing transformations for visualization
- **ggplot2** / **seaborn**: Publication-quality figures

---

## 3.6 Experimental Design Best Practices

### Biological Replication

**Why replicates matter:**
- Accounts for biological variability (cells are not clones)
- Enables statistical inference about population-level effects
- Pseudoreplicates (multiple measurements of same sample) insufficient

**Recommendation:** ≥ 3 biological replicates per condition

**Trade-off:** 
- More replicates → more robust conclusions
- More replicates → higher cost
- Balance depends on phenotype variability and effect sizes expected

### Confounding Variables

**Critical:** Don't confound biological variable with technical variables

❌ **BAD:**
- All treated samples from one person, control samples from another (confounded with individual genetics)
- All treated samples sequenced on one lane, controls on another (confounded with sequencing batch)

✅ **GOOD:**
- Randomize samples across lanes/batches
- Balance biological and technical factors

### Biological Relevant Controls

Choose appropriate controls:
- **Negative control:** Same cell type, baseline condition (e.g., untreated)
- **Positive control:** Expected to show similar response (e.g., known pathway component)
- **Technical control:** Spike-in standards (ERCC RNA) to assess quantification accuracy

---

## 3.7 Interpreting DE Results

### Common Pitfalls

**1. P-value doesn't mean fold-change**
- Small p-value = reliable estimate, not necessarily large effect
- Always examine LFC distribution, not just p-values

**2. Absence of evidence ≠ evidence of absence**
- Non-significant gene may still be meaningfully expressed
- Power depends on replication and variance

**3. Confounding with outliers**
- Single extreme replicate can inflate variance and reduce power
- Check for outliers; consider robust methods

**4. Multiple hypotheses**
- If testing many comparisons (e.g., all pairwise combinations), FDR correction becomes more stringent
- Consider pre-registered hypotheses

### Validation

**Always validate key findings:**
- **qPCR**: Gold standard for selected genes
- **Northern blot** or **in situ hybridization**: Confirms localization
- **Protein-level validation**: Western blot, immunofluorescence (confirms translation)

**Why needed:** 
- RNA-seq artifacts (e.g., mapping ambiguities) can create false signals
- Validation builds confidence in results

---

## 3.8 Case Study: Comparing Sample Types

**Scenario:** RNA-seq in two cell types (A and B), 3 replicates each, exploring transcriptome differences.

**Workflow:**
1. **QC**: FastQC on raw reads; assess adapter content, quality scores
2. **Mapping**: Align to reference genome using STAR or bowtie2
3. **Quantification**: Count reads per gene (featureCounts) → count matrix
4. **Normalization**: Explore different methods (CPM, TMM, VST)
5. **Batch inspection**: PCA; assess if any technical batch emerges
6. **DE analysis**: Use DESeq2 or edgeR; output LFC, p-values, adjusted p-values
7. **Filtering**: Keep genes with adj. p-value < 0.05 and |LFC| > 1
8. **Visualization**: Heatmaps, volcano plots, MA plots
9. **Functional analysis**: GSEA or pathway enrichment (topics for later chapters)
10. **Validation**: qPCR on selected DE genes

**Expected outcome:** Ranked list of significant DE genes with estimates of effect size and uncertainty.

---

## Key Takeaways

1. **Read counts are proxies for transcript abundance**, not direct measurements; multiple normalization methods exist
2. **Normalization methods** (CPM, RPKM, TPM, TMM) each have assumptions and appropriate use cases
3. **Technical biases** (GC content, batch effects, strand bias) must be identified and corrected
4. **Differential expression testing** combines statistical significance with effect size (LFC)
5. **Multiple testing correction** (FDR) is essential when testing thousands of genes
6. **Experimental design** (replication, randomization, avoiding confounds) is critical for valid inference
7. **Validation** of key findings builds confidence in results

---

## Exercises

### Beginner

1. **Normalization Types**: Briefly define RPKM, TPM, and CPM. When would you use each?

2. **Composition Bias**: Why does adding a single highly-expressed gene (e.g., hemoglobin) to the transcriptome affect CPM values of other genes?

3. **Multiple Testing**: You identify 500 significantly DE genes at p-value < 0.05 (unadjusted) from 20,000 genes tested. Approximately how many are expected to be false positives? How many would you expect at FDR < 0.05?

### Intermediate

4. **Negative Binomial Distribution**: RNA-seq counts often follow a negative binomial distribution. Why is this better than assuming a Poisson distribution (which has mean = variance)?

5. **Batch Correction Strategy**: You discover that your batch of samples has high PC1 values that separate from other batches in PCA. Should you use ComBat to remove this batch effect before downstream analysis? What risks does batch correction introduce?

6. **Fold-Change Interpretation**: Gene A has LFC = 0.5 and adj. p-value = 0.001. Gene B has LFC = 2.0 and adj. p-value = 0.1. Which gene would you prioritize for validation? Why?

### Advanced

7. **Variance Stabilization**: Describe how variance-stabilizing transformation (VST) works. Why is this useful for visualization but problematic for downstream statistical testing?

8. **Power Calculation**: You want to detect a 1.5-fold change (LFC ≈ 0.58) at α = 0.05 (FDR). A pilot study with n=2 replicates per condition found gene variance estimate of 2.0. Use the formula below to estimate required sample size (assuming NB distribution):

$$n = \frac{2(z_\alpha + z_\beta)^2 (\phi + 1/\mu)}{\mu^2 \cdot \text{LFC}^2}$$

where $\phi$ = dispersion, $\mu$ = mean count, $z_\alpha$ = 1.96 for α=0.05.

9. **Confounder Analysis**: In your experiment, samples from Patient 1 are all treated; samples from Patient 2 are all control. Design a statistical model to de-confound patient effects from treatment. How would you test whether patient is a confounder?

---

## Further Reading

### Foundational RNA-seq Papers

- Wang, Z., Gerstein, M., & Snyder, M. (2009). "RNA-Seq: A revolutionary tool for transcriptomics." *Nature Reviews Genetics*, 10(1), 57-63.
- Mortazavi, A., et al. (2008). "Mapping and quantifying mammalian transcriptomes by RNA-Seq." *Nature Methods*, 5(7), 621-628.

### Normalization & Statistical Methods

- Robinson, M. D., & Oshlack, A. (2010). "A scaling normalization method for differential expression analysis of RNA-seq data." *Genome Biology*, 11(3), R25.
- Love, M. I., Huber, W., & Anders, S. (2014). "Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2." *Genome Biology*, 15(12), 550.
- Law, C. W., Chen, Y., Shi, W., & Smyth, G. K. (2014). "voom: precision weights unlock linear model analysis tools for RNA-seq read counts." *Genome Biology*, 15(2), R29.

### Bias Correction

- Hansen, K. D., Irizarry, R. A., & Wu, Z. (2012). "Removing technical variability in RNA-seq data using conditional quantile normalization." *Biostatistics*, 13(2), 204-216.
- Leek, J. T., Johnson, W. E., Parker, H. S., Jaffe, A. E., & Storey, J. D. (2012). "The sva package for removing batch effects and other unwanted variation in high-throughput experiments." *Bioinformatics*, 28(6), 882-883.

### Design & Validation

- Schurch, N. J., et al. (2016). "How many biological replicates are needed in an RNA-seq experiment and which tools should you use?" *RNA*, 22(6), 839-851.

---

**Navigation**: [← Previous: Sequencing Overview](./02-sequencing-overview.md) | [Next: Single-Cell RNA-seq Technologies →](./04-scrna-technologies.md)
