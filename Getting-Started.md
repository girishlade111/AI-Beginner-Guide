# 🚀 Getting Started

## Overview

A pragmatic path to get your workstation or cloud environment ready and your first projects running. This section will guide you through setting up your development environment from scratch, whether you're working locally or in the cloud.

## Prerequisites

Before diving into AI development, ensure you have:

### Programming Skills
- **Python proficiency**: Understanding of functions, classes, and virtual environments
- **Data structures**: Familiarity with lists, dictionaries, tuples, and sets
- **Object-oriented programming**: Basic OOP concepts

### Mathematical Foundation
- **Linear Algebra**: Vectors, matrices, matrix operations
- **Calculus**: Derivatives, gradients (for understanding optimization)
- **Probability & Statistics**: Distributions, expectation, variance

*Don't worry if your math skills are rusty—many concepts can be learned as you go!*

### Version Control
- **Git basics**: clone, branch, commit, push, pull
- **GitHub/GitLab**: Basic repository management

## Environment Setup (Local)

### Step 1: Install Python and Git

**Python 3.10+**
- **Windows**: Download from [python.org](https://www.python.org/downloads/)
- **macOS**: `brew install python@3.11`
- **Linux**: `sudo apt-get install python3.11` or equivalent

**Git**
- **Windows**: Download from [git-scm.com](https://git-scm.com/)
- **macOS**: `brew install git`
- **Linux**: `sudo apt-get install git`

Verify installations:
```bash
python --version  # Should show Python 3.10+
git --version
```

### Step 2: Create a Virtual Environment

Virtual environments keep your project dependencies isolated:

```bash
# Create virtual environment
python -m venv .venv

# Activate it
# On macOS/Linux:
source .venv/bin/activate

# On Windows:
.\.venv\Scripts\activate

# You should see (.venv) in your terminal prompt
```

### Step 3: Upgrade Core Tools

```bash
pip install --upgrade pip setuptools wheel
# Optionally install uv (faster pip alternative)
pip install uv
```

### Step 4: Install Core Libraries

Install essential data science and ML libraries:

```bash
pip install numpy pandas scikit-learn jupyter matplotlib seaborn
```

**What these do:**
- `numpy`: Numerical computing, array operations
- `pandas`: Data manipulation and analysis
- `scikit-learn`: Classical machine learning algorithms
- `jupyter`: Interactive notebooks for experimentation
- `matplotlib` & `seaborn`: Data visualization

### Step 5: Optional Deep Learning Stack

**PyTorch** (Recommended for beginners):
```bash
# CPU version
pip install torch torchvision torchaudio

# GPU version (CUDA 12.1)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

**TensorFlow** (Alternative):
```bash
pip install tensorflow
```

*Choose one framework to start—don't install both unless necessary.*

## Cloud Options

Not ready for local setup? Use these free cloud platforms:

### Google Colab
- **Free GPU/TPU access**
- Browser-based Jupyter notebooks
- Pre-installed ML libraries
- [colab.research.google.com](https://colab.research.google.com/)

###  Kaggle Notebooks
- Free GPU hours
- Access to Kaggle datasets
- Community competitions
- [kaggle.com/code](https://www.kaggle.com/code)

### GitHub Codespaces
- VS Code in the browser
- 60 hours free per month
- Full development environment

## Project Scaffold

Organize your AI projects with a consistent structure:

```
my-ai-project/
├── data/
│   ├── raw/          # Original, immutable data
│   └── processed/    # Cleaned, transformed data
├── notebooks/        # Jupyter notebooks for exploration
├── src/              # Source code (models, utilities)
├── models/           # Trained model weights
├── reports/          # Generated analysis, figures
├── configs/          # Configuration files
├── tests/            # Unit and integration tests
├── requirements.txt  # Project dependencies
├── .gitignore        # Files to exclude from git
└── README.md         # Project documentation
```

### Initialize Your Project

```bash
# Create directory
mkdir my-ai-project
cd my-ai-project

# Initialize git
git init

# Create initial structure
mkdir -p data/{raw,processed} notebooks src models reports configs tests

# Create gitignore
echo ".venv/\n*.pyc\n__pycache__/\ndata/raw/\nmodels/*.pth\n.env" > .gitignore

# Initial commit
git add .
git commit -m "Initial project structure"
```

## Actionable Tips

### Dependency Management

**Pin versions** for reproducibility:
```bash
# After installing packages
pip freeze > requirements.txt

# To install from requirements
pip install -r requirements.txt
```

**Use `requirements.txt`** or **`pyproject.toml`** to track dependencies.

### Environment Variables

**Never commit API keys or secrets!**

Use `.env` files with `python-dotenv`:

```bash
pip install python-dotenv
```

```python
# In your code
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv('API_KEY')
```

### Start Small

- **Use small datasets** while developing (faster iteration)
- **Subset large datasets** for initial experimentation
- **Scale up** only after your pipeline works

### Code Quality

Install linting and formatting tools:
```bash
pip install black flake8 isort
```

## Frequently Asked Questions

### Why are my installs so slow?

**Solutions:**
- Use binary wheels instead of building from source
- Try local package mirrors
- Consider `mamba` or `conda` for scientific stacks:
  ```bash
  conda install pytorch numpy pandas scikit-learn
  ```

### Google Colab times out—how do I save my work?

- **Mount Google Drive** to persist data:
  ```python
  from google.colab import drive
  drive.mount('/content/drive')
  ```
- **Checkpoint models** to Drive or cloud storage
- **Use Colab Pro** for longer sessions ($9.99/month)

### Should I use Conda or pip?

**pip + venv**: Simpler, lighter, works everywhere  
**Conda**: Better for complex scientific dependencies, environment management

*Recommendation: Start with pip, switch to Conda if you hit dependency conflicts.*

### How do I handle large datasets?

- **Streaming**: Process data in chunks
- **Cloud storage**: S3, GCS, Azure Blob
- **Data version control**: Tools like DVC

## Advanced Notes

### Reproducibility Best Practices

1. **Capture exact versions**:
   ```bash
   pip freeze > requirements-lock.txt
   ```

2. **Seed random number generators**:
   ```python
   import random
   import numpy as np
   import torch

   random.seed(42)
   np.random.seed(42)
   torch.manual_seed(42)
   ```

3. **Log hardware and environment**:
   - Python version
   - CUDA version (if using GPU)
   - OS and architecture

4. **Use experiment tracking**:
   - MLflow
   - Weights & Biases
   - TensorBoard

### Docker for Consistency

For ultimate reproducibility, containerize your environment:

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
CMD ["python", "train.py"]
```

## Next Steps

Now that your environment is set up:

1. **Explore** [AI Fundamentals](./AI-Fundamentals.md) to understand core concepts
2. **Try** a simple project: Iris flower classification with scikit-learn
3. **Join** the community—see [Resources](./Resources.md) for links

---

**Pro Tip**: Keep a "learning journal" notebook where you document new concepts, code snippets, and troubleshooting solutions. Future you will thank present you! 📝
