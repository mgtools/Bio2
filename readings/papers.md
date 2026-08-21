# Readings

This folder contains reading materials, references, and supplementary documentation for the Introduction to Bioinformatics course.

## Scientific papers and articles (recent breakthroughs) -- for literature presentation by students
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

**What to learn?** How models are evaluated (the metrics)? What are the protein understanding benchmarks?

#### Paper 9: Protein embedding based alignment (BMC Bioinformatics)

**Link:** [BMC Bioinformatics paper](https://doi.org/10.1186/s12859-024-05699-5)

**Why pick the paper?** Protein sequence alignment becomes especially difficult when sequences have less than 20–35% pairwise identity, the so-called "twilight zone." This paper introduces PEbA, which uses similarities between protein-language-model embeddings as dynamic-programming match scores instead of traditional substitution matrices. It shows how contextual representations from models such as ProtT5 can improve alignment quality for highly divergent proteins, outperforming BLOSUM-based alignment and other embedding-based methods.

#### Paper 10: AlphaFold accelerates artificial intelligence powered drug discovery: efficient discovery of a novel CDK20 small molecule inhibitor (Chemical Science)

**Link:** [Chemical Science paper](https://pubs.rsc.org/sc/article/14/6/1443/786890/AlphaFold-accelerates-artificial-intelligence)

**Why pick the paper?** An example of AI in/for heathcare. This makes an excellent follow-up to AlphaFold because it moves from predicting structures toward actually discovering molecules. The researchers used an AlphaFold-predicted structure of CDK20 together with an AI-powered drug-discovery platform to identify novel small-molecule inhibitors. Note the two platforms that are used in this project: PandaOmics and Chemistry42 are commercial.

#### Paper 11: A machine learning model using clinical notes to identify physician fatigue (Nature Communications, 2025)

**Link:** [Nature Communications paper](https://doi.org/10.1038/s41467-025-60865-4)

**Why pick the paper?** This paper is a useful example of applying machine learning to real-world clinical text and to an important human-factors problem. The authors trained a model on clinical notes from 129,228 emergency-department visits to identify notes written in high-fatigue settings, using recent shift patterns as a proxy for physician fatigue. Higher predicted fatigue was associated with differences in clinical decision-making, including a lower yield of diagnostic testing for heart attacks. It provides a concrete case for discussing proxy labels, clinical text representation, confounding, privacy, and the difference between detecting a pattern and proving causation.

#### Paper 12: Clinicians vs. artificial intelligence in patient outcome prediction in the intensive care unit (npj Digital Medicine, 2026)

**Link:** [npj Digital Medicine paper](https://doi.org/10.1038/s41746-026-03132-0)

**Why pick the paper?** This study directly compares clinicians with artificial intelligence algorithms for predicting patient outcomes in the intensive care unit. It combines retrospective and prospective evaluations across 15 adult ICUs in Alberta, Canada, allowing students to consider both benchmark performance and prediction in a live clinical setting. The paper is a strong starting point for discussing calibration, generalizability, human-AI comparison, prospective validation, and whether predictive accuracy alone is enough to improve patient care.

**Last Updated**: 2026-08-13
