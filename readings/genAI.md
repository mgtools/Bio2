# Generative AI for Computational Biology

Generative artificial intelligence (GenAI) systems can produce text, code, summaries, plans, and other content from a user's instructions. In computational biology, they can help us learn unfamiliar concepts, write and debug programs, explore possible explanations, and find relevant literature. They are useful assistants, but they are not substitutes for scientific judgment, primary sources, reproducible analysis, or expert review.

This reading introduces three practical roles for GenAI:

1. **Responsible use of AI** - using AI in ways that protect people, data, scientific integrity, and reproducibility.
2. **GenAI as a coding assistant** - using AI to plan, write, explain, test, and debug code.
3. **GenAI as a discovery aide** - using AI to generate questions, search strategies, hypotheses, and connections between ideas.

## Learning Objectives

After completing this reading, you should be able to:

- Write a prompt that includes context, a specific task, constraints, and a requested output format.
- Check AI-generated explanations, code, citations, and biological claims against reliable evidence.
- Use GenAI to improve a workflow without hiding its contribution or outsourcing scientific decisions.
- Identify privacy, bias, hallucination, reproducibility, and intellectual-property risks.
- Keep enough of a record that another person can understand how AI contributed to your work.

## A Useful Mental Model

Treat GenAI as a fast collaborator that proposes possibilities. It does not automatically know whether a statement is true, whether code is appropriate for your data, or whether a citation actually supports a claim.

Use the following loop:

```text
Ask -> Inspect -> Verify -> Adapt -> Document
```

- **Ask:** State the goal, context, assumptions, and desired format.
- **Inspect:** Read the entire response. Look for missing cases, invented details, and hidden assumptions.
- **Verify:** Run code, check calculations, consult primary sources, and compare with expected biology.
- **Adapt:** Revise the prompt or response based on what you learned.
- **Document:** Record the tool, date, relevant prompt, changes you made, and validation steps.

## Responsible Use of AI

### Protect data and people

Do not paste identifiable patient information, private research data, unpublished sequences, credentials, or access tokens into a public AI service. De-identification is not always enough: genomic data can remain identifying because it is inherently linked to individuals and families. Follow your institution's policies, data-use agreements, and the terms of the service you are using.

Before using a dataset with an AI tool, ask:

- Is the data public, or do I have permission to share it?
- Could the input identify a person, laboratory, participant, or confidential project?
- Will the service retain or use the input for training?
- Can I use a local or institution-approved model instead?

### Protect scientific integrity

AI output is a draft, not evidence. Verify:

- **Facts:** Check biological definitions, units, assumptions, and reported results.
- **Citations:** Open each source and confirm that it exists and supports the exact claim. Models can invent plausible-looking references.
- **Code:** Run tests, inspect edge cases, and review dependencies before trusting results.
- **Statistics:** Recalculate important values and check whether the method matches the study design.
- **Interpretations:** Distinguish correlation from causation and predictions from experimentally demonstrated findings.

Do not use AI to fabricate data, results, citations, or experimental observations. Disclose meaningful AI assistance according to the requirements of your course, institution, journal, or funder.

### Watch for bias and overconfidence

AI systems can reproduce biases in their training data and can state uncertain answers confidently. Be especially careful with clinical recommendations, population-level claims, underrepresented organisms, and conclusions drawn from small or uneven datasets. Ask the model to state assumptions and uncertainty, then evaluate those statements yourself.

### Keep work reproducible

Save the inputs and outputs that materially affect your work. Record the model or service, date, relevant settings, and the final human-edited result. A prompt alone is not a reproducible scientific method: include the data version, software environment, code, and validation procedure as well.

## GenAI as a Coding Assistant

GenAI is most useful when you remain the programmer and reviewer. Give it a small, testable task instead of asking it to invent an entire analysis with no context.

### Prompt pattern

```text
You are helping with a Python analysis of [type of biological data].

Goal: [one specific outcome]
Inputs: [file format, column names, example values, or a small synthetic example]
Constraints: use [libraries/version], preserve [requirements], and do not change [parts]
Output: provide code plus a short explanation and three tests, including one edge case.
```

Never include passwords, API keys, or private data in the prompt. Replace sensitive values with synthetic examples.

### Example: ask for a small function

Suppose a table contains gene names and counts. A useful request is:

```text
Write a Python function using pandas that takes a DataFrame with columns
gene and count, removes rows with missing gene names, combines duplicate genes
by summing count, and returns genes sorted by decreasing count.

Include type hints, validation for negative counts, and pytest tests for an
empty table, duplicate genes, and a missing value.
```

A responsible workflow is:

1. Read the proposed function line by line and confirm that its assumptions match the data.
2. Run the generated tests and add a test based on your own expected behavior.
3. Try an edge case such as an empty input or a negative count.
4. Compare the output with a hand-calculated example.
5. Keep only the code you understand and can explain.

### Example: use AI to debug, not guess

Provide the smallest reproducible example, the full error message, the expected result, and the result you received:

```text
This function should return one row per cell, but it returns duplicate cells.
Here is a synthetic input, the code, the output, and the traceback.
Identify the smallest likely cause. Explain why it causes duplication, propose
one fix, and give a test that would fail before the fix and pass afterward.
Do not rewrite unrelated parts of the analysis.
```

Do not accept a debugging answer merely because it sounds reasonable. Reproduce the failure, apply one change at a time, and run the relevant test suite.

### Good coding-assistant tasks

- Explain an unfamiliar function or traceback in plain language.
- Turn a prose requirement into pseudocode and test cases.
- Generate a small helper function with explicit assumptions.
- Suggest clearer variable names or documentation.
- Review code for missing validation, fragile file handling, or untested edge cases.
- Translate a command between environments after checking the tool versions.

### Poor coding-assistant tasks

- Asking for a complete biological analysis without describing the data or study design.
- Running generated code on sensitive data without review.
- Accepting a package recommendation without checking maintenance, license, and compatibility.
- Reporting AI-generated output as if it were an experimental result.

## GenAI as a Discovery Aide

Discovery use means using AI to widen and organize your thinking. It can help turn a broad interest into searchable questions, compare possible methods, and identify terms you may not know. It should not be treated as a literature database or as proof that a hypothesis is correct.

### Example: turn a broad topic into questions

```text
I am studying how cell type affects gene expression in single-cell RNA-seq.
Generate six research questions that differ in scale and testability.
For each question, list the measurable variables, a possible confounder, and
one type of evidence needed to support the conclusion. Mark which questions
are descriptive and which are causal.
```

Use the response to choose search terms and refine your plan. Then consult databases and primary papers directly. Confirm the terminology, publication details, methods, and limitations yourself.

### Example: build a search strategy

```text
Create a literature-search plan for batch correction in single-cell RNA-seq.
Organize it into: core concepts, synonyms, competing methods, evaluation
metrics, and known limitations. Suggest combinations of keywords for a
database search. Do not invent papers or citations.
```

The resulting terms might help you search resources such as PubMed, Google Scholar, or a field-specific database. Search results, abstracts, and full papers remain the sources of record.

### Example: compare methods before choosing one

```text
Compare pseudobulk analysis and cell-level mixed-effects models for a
single-cell RNA-seq experiment with biological replicates. Use a table with
the unit of analysis, assumptions, strengths, limitations, and situations in
which each method is inappropriate. State what additional study information
you need before recommending either method.
```

This kind of answer is a starting point for discussion. The correct choice depends on the design, replication, outcome, and assumptions of the actual experiment.

### Generate hypotheses carefully

AI can suggest mechanisms or connections, but a generated hypothesis is not a discovered fact. For each proposed idea, ask:

- What observation would support it?
- What observation would weaken it?
- What alternative explanation is plausible?
- What experiment or analysis could distinguish the alternatives?
- Which primary sources provide relevant evidence?

## Prompt Design Checklist

A strong prompt usually includes:

- **Context:** What are you studying, and who is the intended audience?
- **Task:** What single action should the model perform?
- **Evidence:** Which files, sources, or definitions may it use?
- **Constraints:** What tools, formats, assumptions, or boundaries apply?
- **Output:** Should it return prose, a table, pseudocode, code, or questions?
- **Quality checks:** Should it identify uncertainty, edge cases, alternatives, or tests?

Instead of asking, `Explain RNA-seq`, ask:

```text
Explain the difference between bulk RNA-seq and single-cell RNA-seq for a
beginner in computational biology. Use no more than 250 words, include one
small comparison table, define technical terms, and list two limitations of
each technology. Separate established facts from practical rules of thumb.
```

## A Student's Review Checklist

Before submitting work that used GenAI, confirm:

- I can explain every line of generated code that remains in my work.
- I ran the code and checked its output on known or synthetic examples.
- I verified important scientific claims using reliable sources.
- I did not share confidential, identifiable, or credential-bearing data.
- I have labeled assumptions, uncertainty, and limitations.
- I followed the course or institution's disclosure requirements.
- I recorded enough information to describe how AI contributed.

## Further Reading in This Repository

- [AI tools and integrations](../ai-tools/README.md)
- [Course overview](../README.md)
- [RNA foundation model and alignment notebook](../notebooks/ai_coding_styles_rnafm_alignment.ipynb)
- [Protein structure prediction workflow](../notebooks/protein_structure_prediction_workflow.ipynb)
- [Readings collection](README.md)

