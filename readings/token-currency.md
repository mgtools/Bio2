**“Tokens are the new currency of AI.”**

When we use modern AI systems, we are consuming a computational resource, and the cost is determined not simply by how much text the model produces, but by **everything the model has to process to complete the task**.

## Tokens Are the New Currency of AI

As AI becomes part of everyday computing, **tokens are becoming the new currency of computation**. Just as we learned to think about CPU time, memory, storage, and cloud-computing costs, we now need to think about **token budgets** when using large language models (LLMs).

A token is roughly a small piece of text—a word, part of a word, punctuation, or code. What matters economically is that **we pay not only for what an AI model produces, but also for what it must read, remember, reason over, retrieve, and sometimes repeatedly re-read.**

A useful approximation is:

**Total AI cost ≈ input tokens + context/history + reasoning + output tokens + tool/computing costs**

### Where do the tokens come from?

Consider asking an AI coding agent:

> “Look at my project and modify the program so that it supports FASTQ files.”

The visible prompt may contain only 15 tokens, but that is not necessarily the real workload. The AI may need to process:

**Your prompt**
↓
**System instructions**
↓
**Previous conversation history**
↓
**README + source code + configuration files**
↓
**Retrieved documentation or web pages**
↓
**Intermediate reasoning and agent actions**
↓
**Generated code and explanation**

Therefore, a short request can potentially trigger the processing of **tens or hundreds of thousands of tokens**.

This becomes particularly important in long conversations. Suppose a conversation has accumulated 80,000 tokens of relevant context. Your next message might contain only 20 tokens, and the answer might contain only 500 tokens, but the model may need to process much of that earlier context again. Thus:

**cost ≠ length of the answer**

Instead:

**cost = everything required to produce the answer**

This is why **context management is also cost management**.

### Different models have very different token prices

For API use, model choice can change the cost substantially. As of August 2026, for example, OpenAI's current GPT-5.6 family spans models optimized for different cost/performance points. Standard API prices per million tokens are approximately:

| Model         | Input | Cached input | Output |
| ------------- | ----: | -----------: | -----: |
| GPT-5.6 Sol   | $5.00 |        $0.50 | $30.00 |
| GPT-5.6 Terra | $2.50 |        $0.25 | $15.00 |
| GPT-5.6 Luna  | $1.00 |        $0.10 |  $6.00 |

([OpenAI Developers][1])

So using the most capable model for every task may be unnecessary. A simple file-format conversion, code explanation, or classification task might be handled by an inexpensive model, while a difficult algorithm-design or scientific-reasoning problem may justify a more expensive frontier model.

Anthropic follows a similar model hierarchy. For example, Claude Sonnet 5 is currently priced at an introductory **$2 per million input tokens and $10 per million output tokens** through August 31, 2026, moving afterward to $3/$15. Claude Opus 5 starts at approximately **$5/$25**, while the lower-cost Haiku tier is intended for high-volume workloads. ([Anthropic][2])

Thus, choosing an AI model increasingly resembles choosing a computing resource:

**small/fast model → routine work**
**medium model → most development work**
**frontier model → difficult reasoning and complex agentic tasks**

### Input can matter as much as output

It is tempting to think that asking an AI to “give me a short answer” makes the request cheap. It may not.

Imagine:

**Prompt:** 100 tokens
**Conversation history:** 20,000 tokens
**Source files:** 50,000 tokens
**Retrieved documentation:** 10,000 tokens
**Generated answer:** 500 tokens

The user sees only 500 tokens, but the AI may have processed roughly **80,000 input tokens**.

For agentic coding, the difference can be even larger because the agent may repeatedly inspect files, run commands, examine errors, modify code, and try again.

### History has a cost

Conversation history is especially important.

A long ChatGPT or Claude conversation can be extremely useful because the AI remembers what has already been discussed. But that context is computationally expensive.

Conceptually:

**Turn 1:** prompt → response

**Turn 20:**
previous conversation

* previous instructions
* current prompt
  → response

The twentieth request can therefore be much more expensive than the first, even when the two questions are the same length.

Modern systems address this partly through **prompt caching**. Repeated context can be charged at substantially lower rates. OpenAI, for example, explicitly distinguishes regular input, cached input, output, and—in some models—reasoning tokens. ([OpenAI Help Center][3])

Caching changes an important rule of AI engineering:

**Do not ask only “How many tokens are there?” Ask “How many NEW tokens must the model process?”**

### AI agents make token budgeting even more important

The issue becomes much more significant when moving from ordinary chat to **agentic AI**.

A coding agent may perform:

**request → inspect repository → reason → edit code → run program → read error → inspect more files → revise → test → reason again → produce answer**

Each step may involve another model call.

Therefore:

**Agent cost ≈ Σ cost of all model calls + tool/computing costs**

A five-minute interaction with an agent can involve far more tokens than the final response suggests.

This is relevant to tools such as ChatGPT/Codex, Claude/Claude Code, and GitHub Copilot. [OpenAI](https://openai.com/?utm_source=chatgpt.com), [Anthropic](https://www.anthropic.com/?utm_source=chatgpt.com), and [GitHub](https://github.com/?utm_source=chatgpt.com) increasingly provide systems in which the model is not merely generating text—it is **reading files, calling tools, executing code, searching information, and iterating toward a solution**.

### Codespaces illustrates another kind of cost

GitHub Codespaces is somewhat different: **Codespaces itself is not an AI model**. It provides the cloud development environment in which AI-assisted coding can take place. Its costs therefore include traditional cloud resources such as **compute time and storage**, rather than simply tokens. GitHub currently lists Codespaces as starting around **$0.18/hour for compute and $0.07/GB for storage**. ([GitHub][4])

GitHub Copilot adds the AI layer. Its plans range from free usage to paid Pro and Pro+ tiers, with different allowances for AI usage. ([GitHub][5])

Therefore, an AI-assisted programming environment may involve several currencies simultaneously:

**Tokens** — LLM inference
**Compute hours** — Codespaces/cloud machines
**Storage** — repositories, environments, datasets
**Tool calls** — search, code execution, retrieval, etc.
**Human time** — perhaps the most expensive resource of all

### Token efficiency will become a programming skill

The goal should therefore not simply be to minimize tokens. It should be to maximize:

**useful work / cost**

A cheap model that repeatedly fails can ultimately cost more than an expensive model that solves the problem in one attempt.

Good AI-assisted programming will increasingly involve **model routing**:

> Use the cheapest model that can reliably perform each part of the task.

For example:

**Luna / Haiku-class model** → summarize files, extract information, simple transformations
**Terra / Sonnet-class model** → programming, analysis, routine reasoning
**Sol / Opus-class model** → difficult algorithm design, complex debugging, scientific reasoning

The agent itself can potentially make these decisions automatically.

## The bigger idea

We are moving from a world in which programmers mainly managed **CPU, memory, disk, and network resources** to one in which they must also manage **intelligence as a computational resource**.

That resource is increasingly measured in tokens.

So **“tokens are the new currency”** means more than paying for generated words. Every prompt has a computational budget. The relevant questions become:

**What model should I use? How much context should I provide? How much history should I retain? What information should be cached? How much reasoning is necessary? When should I use an expensive frontier model? When is a smaller model sufficient?**

Learning to answer these questions—and achieving the best result within a **token and dollar budget**—is becoming an important part of AI literacy and AI-assisted programming.

One distinction I would emphasize if this is for your computational biology/AI course: **ChatGPT and Claude are applications/services; GPT and Claude Sonnet/Opus/Haiku are model families; Anthropic is the company; Codespaces is a cloud development environment; and GitHub Copilot is the AI coding service.** Keeping those levels separate will make the cost discussion much clearer.

[1]: https://developers.openai.com/api/docs/models/gpt-5.6-sol?utm_source=chatgpt.com "GPT-5.6 Sol Model | OpenAI API"
[2]: https://www.anthropic.com/news/claude-sonnet-5?utm_source=chatgpt.com "Introducing Claude Sonnet 5 \ Anthropic"
[3]: https://help.openai.com/en-us/articles/4936856-how-can-i-estimate-the-cost-of-my-usage?utm_source=chatgpt.com "What are tokens and how to count them? | OpenAI Help Center"
[4]: https://github.com/pricing?utm_source=chatgpt.com "Pricing · Plans for every developer"
[5]: https://github.com/features/copilot/plans?utm_source=chatgpt.com "GitHub Copilot · Plans & pricing"
