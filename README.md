# IaC-Eval: Enhanced with Open Source LLMs and Containerization

This project is an enhanced version of the original IaC-Eval project, focusing on proving that lightweight, specialized open-source LLMs can compete with OpenAI's models for Infrastructure-as-Code (IaC) generation tasks.

## 🎯 Project Objective

The main goal of this enhanced version is to demonstrate that open-source LLMs, despite being much lighter and more specialized, can rival OpenAI's LLMs in generating quality Terraform HCL code. This work challenges the assumption that only large, proprietary models can handle complex infrastructure code generation tasks.

**IaC-Eval** is a comprehensive project for quantitatively evaluating the capabilities of large language models in cloud Infrastructure-as-Code generation. The framework specifically targets Terraform HCL code generation and provides the first human-curated and challenging IaC dataset containing 458 questions ranging from simple to difficult across various AWS cloud services.

**Dataset Features:**
- 458 carefully curated Infrastructure-as-Code tasks
- Varying difficulty levels from simple to complex
- Coverage of diverse AWS services and use cases
- Human-validated reference solutions
- Available on [HuggingFace](https://huggingface.co/datasets/autoiac-project/iac-eval)

For detailed information about the original project, evaluation methodologies, and dataset structure, please refer to the [original README](README_original.md).

## 🚀 New Features

We have extended the original IaC-Eval project with the following enhancements:

### 1. Complete Pipeline Containerization
- **Dockerized Environment**: Full containerization of the evaluation pipeline for consistent, reproducible results
- **Easy Deployment**: One-command setup using Docker Compose
- **Isolated Environment**: No need to manage complex dependencies manually

### 2. Ollama Integration
- **Open Source LLMs**: Integration of various open-source models through [Ollama](https://ollama.com/)
- **Local Inference**: Run evaluations locally without external API dependencies
- **Cost-Effective**: Eliminate API costs while maintaining evaluation quality

### 3. Results Showcase
- **Live Demo**: View our comprehensive results at [pierrelaurent.ovh/llm4cloud/](http://pierrelaurent.ovh/llm4cloud/)
- **Performance Comparison**: Side-by-side comparison between open-source and proprietary models
- **Interactive Dashboard**: Explore results across different models and strategies

## 🛠️ Quick Setup with Docker

### Prerequisites
- Docker and Docker Compose V2 installed on your system
- AWS credentials for Terraform validation

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd iac-eval-tsp
    ```
2. **Run the automated setup**
   ```bash
   ./run-docker-pipeline.sh
   ```
3. **Follow the interactive prompts**
    - Enter your AWS credentials
    - Select an Ollama model (e.g., Ollama-codegemma:7b)
    - Choose an evaluation strategy (normal, multi-turn, COT, FSP)
    - Set the number of samples to evaluate

4. **Monitor the evaluation, the pipeline will automatically :**
    - Pull the required Docker images
    - Set up the evaluation environment
    - Run the selected model against the IaC dataset
    - Generate comprehensive results in CSV format

## 📁 Project Main Structure
```
├── evaluation/                    # Core evaluation pipeline and metrics
│   ├── eval.py                   # Main evaluation script
│   ├── models.py                 # LLM model implementations and interfaces
│   ├── metrics.py                # Evaluation metrics (BLEU, exact match, etc.)
│   ├── data.py                   # Dataset loading and processing utilities
│   ├── prompt_templates.py       # Prompt generation for different strategies
│   ├── llm-judge-eval.py         # LLM-based evaluation metrics
│   ├── config_*.json             # Configuration files for different models
│   ├── misc/                     # Additional evaluation utilities
│   │   ├── ablation/             # Ablation study scripts
│   │   ├── ablation-judge/       # LLM judge ablation studies
│   │   ├── ablation-multiple-sample/  # Pass@k metrics calculation
│   │   └── complete-dataset-measurement/  # Dataset complexity analysis
│   └── logs/                     # Evaluation logs and outputs
│
├── retriever/                     # RAG (Retrieval-Augmented Generation) components
│   ├── llama_index_retriever.py   # Document retrieval and indexing
│   ├── terraform-provider-aws/    # AWS Terraform documentation
│   └── aws-index/                 # Pre-built document index
│
├── templates/                     # Prompt templates for different strategies
│   ├── cot/                       # Chain of Thought prompts
│   ├── fsp/                       # Few-Shot Prompting templates
│   ├── multi-turn/                # Multi-turn conversation templates
│   └── rag/                       # RAG-specific prompt templates
│
├── local-dataset/                 # Local dataset storage and management
│   ├── data/                     # Core dataset files
│   └── processed/                # Preprocessed dataset variants
│
├── results/                       # Evaluation results and metrics
│   ├── [model-name]/             # Results organized by model
│   └── aggregated/               # Cross-model comparison results
│
├── licenses/                      # License information for models
│   └── README.md                  # License details for different LLMs
│
├── util/                         # Utility scripts and helpers
│   ├── aws_utils.py              # AWS credential and service utilities
│   └── terraform_utils.py        # Terraform validation helpers
│
├── docker-compose.yml            # Docker orchestration configuration
├── Dockerfile                    # Container definition with dependencies
├── entrypoint-iac-eval.sh       # Container entrypoint script
├── run-docker-pipeline.sh       # Automated setup and execution script
├── setup.sh                      # Environment setup script
├── environment.yml               # Conda environment specification
└── README_original.md            # Original project documentation
```

## 📊 Evaluation Strategies
- **Standard**: Direct prompt-to-code generation
- **Multi-turn**: Interactive refinement with error feedback
- **COT (Chain of Thought)**: Step-by-step reasoning approach
- **FSP (Few-Shot Prompting)**: Learning from examples
- **RAG**: Retrieval-augmented generation with documentation

## 📄 License
This project maintains the same license as the original IaC-Eval project. See [LICENSE.txt](LICENSE.txt) for details.