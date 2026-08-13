# CB2: AI-Enhanced Computational Biology Course

A redesigned computational biology course leveraging AI models for problem-solving and AI-assisted programming.

## Directory Structure

```
├── modules/                          # Course modules organized by topic
│   ├── 01-sequence-analysis/        # DNA/RNA sequence analysis with AI
│   ├── 02-protein-structure/        # Protein folding & structure prediction
│   ├── 03-phylogenetics/            # Evolutionary analysis with AI
│   └── 04-genomics/                 # Genomic data analysis
├── assignments/                      # Assignments and projects
├── notebooks/                        # Jupyter notebooks for interactive learning
├── datasets/                         # Data files for coursework
│   ├── sample-data/                 # Pre-processed sample datasets
│   └── raw/                         # Raw datasets
├── ai-tools/                         # AI integrations & configurations
│   ├── llm-prompts/                 # LLM prompts for biology problems
│   ├── ml-models/                   # ML model configurations
│   └── integrations/                # API integrations (Claude, GPT, etc.)
├── utils/                            # Utility scripts and helpers
├── docs/                             # Documentation
│   ├── guides/                       # Setup & learning guides
│   └── api-references/              # API documentation
├── setup/                            # Configuration & environment setup
└── README.md                         # This file
```

## Getting Started

### Prerequisites
- Python 3.10+
- Jupyter Notebook
- Git

### Installation

```bash
# Clone the repository
git clone <repo-url>
cd CB2

# Set up environment (if using virtual environment)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r setup/requirements.txt
```

## Course Modules

Each module contains:
- **Lecture notes** - Core concepts and theory
- **Notebooks** - Interactive Jupyter notebooks with examples
- **Assignments** - Practical exercises and projects
- **AI integrations** - Examples using LLMs and ML models

### Module Topics
- **01-Sequence-Analysis**: DNA/RNA analysis with AI-powered pattern recognition
- **02-Protein-Structure**: Protein structure prediction using AI models
- **03-Phylogenetics**: Evolutionary analysis and tree building
- **04-Genomics**: Large-scale genomic data analysis with AI

## Key Features

✨ **AI-Powered Learning**
- LLM-assisted code explanation and debugging
- AI models for biological problem-solving
- Interactive examples with popular ML frameworks

💻 **Programming-First Approach**
- Hands-on coding exercises
- AI pair programming assistance
- Real-world biological datasets

📚 **Comprehensive Resources**
- Setup guides for local and cloud environments
- API references for biological databases
- Best practices for AI in computational biology

## Contributing

See [docs/guides/CONTRIBUTING.md](docs/guides/CONTRIBUTING.md) for guidelines.

## License

[Add your license here]

## Resources

- [Setup Guide](docs/guides/setup-guide.md)
- [AI Integration Guide](docs/guides/ai-integration-guide.md)
- [Dataset Documentation](datasets/README.md)
