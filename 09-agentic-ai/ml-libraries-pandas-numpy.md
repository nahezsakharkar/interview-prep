---
title: "ML Libraries for AI Integration: Pandas, NumPy, Scikit-Learn"
tags: ["agentic-ai","python","ml-libraries"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# ML Libraries for AI Integration

For engineers building AI-powered applications, libraries like Pandas and NumPy are not used for training models, but for **Data Engineering** and **Post-processing** of LLM outputs.

## 1. NumPy (Numerical Python)
The foundation for all numerical computing in Python. It provides the `ndarray` (N-dimensional array), which is far more efficient than Python lists.

**Key Use Case in AI**: Vectorization. When handling embeddings (high-dimensional vectors), NumPy allows you to perform operations on millions of vectors simultaneously.

```python
import numpy as np

# Calculating Cosine Similarity between two embeddings
def cosine_similarity(v1, v2):
    dot_product = np.dot(v1, v2)
    norm_v1 = np.linalg.norm(v1)
    norm_v2 = np.linalg.norm(v2)
    return dot_product / (norm_v1 * norm_v2)

emb1 = np.array([0.1, 0.2, 0.8])
emb2 = np.array([0.1, 0.3, 0.7])
print(f"Similarity: {cosine_similarity(emb1, emb2)}")
```

## 2. Pandas
The gold standard for data manipulation and analysis. It provides the `DataFrame`, which is essentially an in-memory SQL table.

**Key Use Case in AI**: RAG (Retrieval Augmented Generation) data cleaning. Before indexing documents in a vector DB, Pandas is used to chunk text, remove duplicates, and filter noise.

```python
import pandas as pd

# Cleaning a dataset before indexing for RAG
df = pd.read_csv("docs.csv")
# Remove duplicates and empty rows
df_clean = df.drop_duplicates(subset=['content']).dropna(subset=['content'])
# Filter for specific categories
relevant_docs = df_clean[df_clean['category'] == 'financial_rules']
```

## 3. Scikit-Learn
A comprehensive library for machine learning. In AI integration, it is often used for "Small ML" tasks that are too cheap for an LLM.

**Key Use Case in AI**:
- **Clustering (K-Means)**: Grouping similar user queries to improve cache hit rates.
- **Preprocessing**: Scaling and normalizing data before feeding it into a model.
- **Evaluation**: Using metrics like Precision, Recall, and F1-score to evaluate a RAG pipeline.

## Complexity Comparison

| Operation | Python List | NumPy Array | Pandas DataFrame |
| :--- | :--- | :--- | :--- |
| **Memory** | High (per-object) | Low (contiguous) | Moderate (columnar) |
| **Speed** | Slow (loops) | Fast (vectorized) | Fast (vectorized) |
| **Indexing** | $O(1)$ by index | $O(1)$ by index | $O(1)$ by index/label |
| **Filtering** | $O(n)$ | $O(n)$ | $O(n)$ (but optimized) |

## Interview questions

### Q1: Why use NumPy arrays instead of Python lists for embeddings?
**Model answer**: Python lists store pointers to objects, which are scattered in memory. NumPy arrays store data in contiguous memory blocks. This allows the CPU to use SIMD (Single Instruction, Multiple Data) instructions, performing operations on entire arrays in a fraction of the time.

### Q2: How does Pandas help in a RAG pipeline?
**Model answer**: RAG requires a "clean" knowledge base. Pandas is used to handle the data-cleaning stage: removing noise, splitting large documents into overlapping chunks for better retrieval, and filtering out irrelevant content based on metadata.

### Q3: When would you use Scikit-Learn instead of an LLM?
**Model answer**: For structured, high-volume tasks. If the goal is to classify a million documents into 5 categories, a Scikit-Learn classifier is $1000\times$ cheaper and faster than an LLM. I use the LLM to label a small "gold set" of data, then train a Scikit-Learn model on that set for production scale.

### Q4: What is "Vectorization" in the context of NumPy?
**Model answer**: Vectorization is the process of replacing explicit `for` loops with array expressions. Instead of looping through 1 million items to add 1 to each, you call `array + 1`. This pushes the loop down into highly optimized C/Fortran code.

### Q5: How do you handle missing data in a Pandas DataFrame before feeding it into a model?
**Model answer**: Depending on the case, I use `df.fillna()` to replace NaNs with a mean/median (Imputation) or `df.dropna()` to remove the records entirely. For categorical data, I use "One-Hot Encoding" via `pd.get_dummies()`.

## Related notes

- [RAG](../09-agentic-ai/rag.md)
- [Python Fundamentals](../02-languages/python-fundamentals.md)
- [LLM Fundamentals](../09-agentic-ai/llm-basics.md)
