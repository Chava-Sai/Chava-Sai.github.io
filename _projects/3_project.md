---
layout: page
title: Explainable Hate Speech Detection using Generative AI
description: Multilingual hate-speech and fake-news detection using QLoRA and Retrieval-Augmented Generation (RAG).
img: /assets/img/LLMArchitecture.png    # preview image on the projects grid
importance: 3
category: work
links:
  - name: code
    url: https://github.com/Chava-Sai/Explainable-Hate-Speech-Detection-using-Generative-AI
---

## Overview
This project explores the detection of **hate speech** and **fake news** using **Quantized Low-Rank Adaptation (QLoRA)** and **Retrieval-Augmented Generation (RAG)**.  
It combines generative and retrieval-based approaches to identify harmful content with high accuracy and interpretability.

<div class="text-center my-2">
  <img src="{{ '/assets/img/RAGWorkflow.png' | relative_url }}" alt="Project Architecture" class="img-fluid rounded z-depth-1" width="600" loading="lazy">
</div>

---

## Features
- **Transliteration & Translation** — Uses *IndicXlit* and *IndicTrans2* to normalize code-mixed Hindi–English text.  
- **Embedding Extraction** — Employs *BERT*, *XLM-RoBERTa*, and *Electra* for robust multilingual embeddings.  
- **QLoRA Fine-Tuning** — Efficiently fine-tunes large models by adapting low-rank matrices within quantized layers.  
- **RAG Integration** — Combines retrieval from a vector database (via *LangChain*) with generation for grounded classification.  

---

## Model Architecture

### Workflow Overview
1. **Data Preprocessing**
   - Clean, transliterate, and translate code-mixed Hindi–English text using *IndicXlit* and *IndicTrans2*.  
   - Remove unwanted symbols and normalize punctuation.  
   - Manually label data as **Hate/Non-Hate** and **Fake/Non-Fake**.

2. **QLoRA Fine-Tuning**
   - LoRA updates only a subset of parameters using low-rank matrices.  
   - QLoRA adds quantization for memory-efficient training on 7B-parameter models.

<div class="text-center my-2">
  <img src="{{ '/assets/img/LLMArchitecture.png' | relative_url }}" alt="LoRA Architecture" class="img-fluid rounded z-depth-1" width="600" loading="lazy">
</div>

3. **Retrieval-Augmented Generation (RAG)**
   - Retrieves relevant context documents from a vector store using *LangChain*.  
   - Incorporates retrieved text into generation, producing grounded, explainable predictions.

<div class="text-center my-2">
  <img src="{{ '/assets/img/LLMFlowChart.png' | relative_url }}" alt="RAG Workflow" class="img-fluid rounded z-depth-1" width="600" loading="lazy">
</div>

4. **Training Hyperparameters**
   - Applied to models such as *Mistral 7B*, *DeepSeek 7B*, *Zephyr Alpha 7B*, and *Zephyr Beta 7B*.  
   - Parameters (LoRA rank, dropout, quantization bits) tuned for efficiency without GPU overload.

---

## Results

### Hate-Speech Detection
| Model | Macro-F1 (QLoRA) | Macro-F1 (RAG + QLoRA) |
|:------|:---------------:|:----------------------:|
| Mistral 7B | 72.3 | **72.8** |
| DeepSeek 7B | 72.3 | 70.9 |
| Zephyr Beta 7B | 69.6 | 70.8 |
| Zephyr Alpha 7B | 67.1 | 69.7 |

### Fake-News Detection
| Model | Macro-F1 (QLoRA) | Macro-F1 (RAG + QLoRA) |
|:------|:---------------:|:----------------------:|
| Mistral 7B | 77.3 | **78.2** |
| DeepSeek 7B | 74.7 | **78.4** |
| Zephyr Beta 7B | 77.3 | 78.2 |
| Zephyr Alpha 7B | 74.7 | 78.4 |

---

## Installation

```bash
git clone https://github.com/Chava-Sai/Explainable-Hate-Speech-Detection-using-Generative-AI
cd Explainable-Hate-Speech-Detection-using-Generative-AI
pip install -r requirements.txt
```