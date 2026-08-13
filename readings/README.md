# Readings

This folder contains reading materials, references, and supplementary documentation for the CB2 course.

# Bioinformatics Fundamentals
- a free molecular primer biology textbook (for students who need a bit catch up with biology)

# Scientific papers and articles (foundational)

### Scientific papers and articles (recent breakthroughs) -- for literature presentation by students
#### Paper 1: Protein-templated synthesis of dinucleotide repeat DNA by an antiphage reverse transcriptase

**Link:** [Science paper](https://www.science.org/doi/10.1126/science.aed1656); [commentary](https://www.science.org/content/article/scientists-stunned-fundamentally-new-way-life-produces-dna)

**Why pick the paper?** Traditionally, biology taught that genetic information flows only from nucleic acids (DNA/RNA) to proteins. However, researchers discovered a bacterial defense system called DRT3 where a specialized enzyme uses a physical protein structure as a template to build DNA without a nucleic acid guide.

#### Paper 2: Accurate structure prediction of biomolecular interactions with AlphaFold 3
**Link:** [Nature paper](https://www.nature.com/articles/s41586-024-07487-w)

**Why pick the paper?** AlphaFold is a major breakthrough because it showed that **AI can solve a fundamental biological problem that had challenged scientists for decades: predicting a protein’s 3D structure from its amino acid sequence**. It can produce highly accurate structures in minutes or hours, compared with months or years using experimental methods. More broadly, AlphaFold demonstrated a new paradigm for computational biology: **AI models can learn complex biological principles directly from large datasets**, rather than relying primarily on explicitly programmed rules. Its success has inspired AI models across proteins, DNA, RNA, and other areas of biology.

#### Paper 3: Telomere-to-telomere assembly using HERRO-corrected Nanopore Simplex reads
**Link:** [Nature paper](https://www.nature.com/articles/s41586-026-10563-y)

**Why pick the paper?** For decades, scientists couldn't fully sequence human DNA because regions near chromosome ends (telomeres) were too difficult to read. This breakthrough uses advanced sequencing technology to complete the entire human genome, including these previously "missing" regions. It's important because **complete genome sequences reveal genetic variations and structures that were previously invisible**, which has implications for understanding genetic diseases, evolution, and personalized medicine. This paper demonstrates how modern sequencing technologies continue to push the boundaries of what we can learn about the human genome.

#### Paper 4: A complete diploid human genome benchmark for personalized genomics
**Link:** [Cell paper](https://www.cell.com/cell/fulltext/S0092-8674(26)00703-8)

**Why pick the paper?** This paper creates a "gold standard" reference genome for personalized medicine by sequencing complete diploid genomes (both copies of each chromosome) and providing highly accurate benchmarks for identifying genetic variations. It's important because **accurate variant calling is essential for diagnosing genetic diseases and understanding individual differences in disease risk and drug response**. As genomic medicine becomes more common, we need reliable ways to distinguish real genetic variations from sequencing errors. This work enables better precision medicine by providing tools and standards for accurately interpreting individual genome sequences.

#### Paper 5: xTrimoPGLM: unified 100-billion-parameter pretrained transformer for deciphering the language of proteins (Nature Methods, 2025)
**Link:** [Nature Methods paper](https://doi.org/10.1038/s41592-025-02636-z?utm_source=chatgpt.com)

**Why pick the paper?** An excellent example of **scaling foundation models for proteins** to an extremely large model.

xTrimoPGLM is a **100-billion-parameter protein language model** designed to support both protein understanding and protein generation. It illustrates how the foundation-model paradigm from natural language processing can be transferred to protein sequences: pretrain a very large model on protein sequence data and then adapt or use it for many downstream biological tasks. It is particularly useful for illustrating the idea that scaling can improve general-purpose representations of proteins. ([Nature][1])

#### Paper 6: Simulating 500 million years of evolution with a language model (Science, 2025)

**Link:** [Science paper](https://doi.org/10.1126/science.ads0018)

**Why pick the paper?** It goes beyond predicting properties of existing proteins to demonstrate **generative protein design**.

ESM-3 is particularly significant because it jointly reasons about **protein sequence, structure, and function** and can generate proteins conditioned on these different modalities. The authors used the model to generate a functional fluorescent protein substantially different from known fluorescent proteins, presenting a compelling example of foundation models moving from *understanding biology* toward *designing new biology*. The paper is highlighted alongside other major protein foundation-model advances in Nature Methods. 

#### Paper 7: Genome modelling and design across all domains of life with Evo 2 (Nature, 2026)
**Link:** [Nature paper](https://www.nature.com/articles/s41586-026-10176-5)

**Why pick the paper?** Probably the strongest current example of a **general-purpose genome foundation model**.

Evo 2 was trained on approximately **9 trillion DNA base pairs across all domains of life**, with up to a **1-million-token context window at single-nucleotide resolution**. Remarkably, the model can predict effects of genetic variants without task-specific fine-tuning, learns representations corresponding to biological features such as exon–intron boundaries and transcription-factor binding sites, and can generate DNA at genomic scales. It extends the foundation-model concept from individual proteins to entire genomes and biological systems.

#### Paper 8: scGPT: toward building a foundation model for single-cell multi-omics using generative AI (Nature Methods, 2024)
**Link:** [Nature Methods paper](https://www.nature.com/articles/s41592-024-02201-0)
**Why pick the paper?** One of the most recognizable examples of applying the **GPT/foundation-model concept to single-cell biology**.

scGPT treats genes and their expression measurements somewhat analogously to tokens and their associated information in language models. Pretraining on very large collections of single-cell data enables the model to be transferred to tasks including cell-type annotation, batch integration, perturbation prediction and multi-omics analysis. It provides an intuitive example for students of how the same **pretraining → representation learning → downstream adaptation** paradigm can be applied to cellular rather than sequence data.

#### Paper 9: Protein embedding based alignment (BMC Bioinformatics)

**Link:** To be added

**Why pick the paper?** To be added

**Last Updated**: 2026-08-13
