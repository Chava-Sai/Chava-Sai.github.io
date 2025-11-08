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

<h3>Hate-Speech Detection</h3>
<table class="table table-sm">
  <thead>
    <tr><th>Model</th><th>Macro-F1 (QLoRA)</th><th>Macro-F1 (RAG + QLoRA)</th></tr>
  </thead>
  <tbody>
    <tr><td>Mistral 7B</td><td>72.3</td><td><strong>72.8</strong></td></tr>
    <tr><td>DeepSeek 7B</td><td>72.3</td><td>70.9</td></tr>
    <tr><td>Zephyr Beta 7B</td><td>69.6</td><td>70.8</td></tr>
    <tr><td>Zephyr Alpha 7B</td><td>67.1</td><td>69.7</td></tr>
  </tbody>
</table>

<h3>Fake-News Detection</h3>
<table class="table table-sm">
  <thead>
    <tr><th>Model</th><th>Macro-F1 (QLoRA)</th><th>Macro-F1 (RAG + QLoRA)</th></tr>
  </thead>
  <tbody>
    <tr><td>Mistral 7B</td><td>77.3</td><td><strong>78.2</strong></td></tr>
    <tr><td>DeepSeek 7B</td><td>74.7</td><td><strong>78.4</strong></td></tr>
    <tr><td>Zephyr Beta 7B</td><td>77.3</td><td>78.2</td></tr>
    <tr><td>Zephyr Alpha 7B</td><td>74.7</td><td>78.4</td></tr>
  </tbody>
</table>

---

## Installation

```bash
git clone https://github.com/Chava-Sai/Explainable-Hate-Speech-Detection-using-Generative-AI
cd Explainable-Hate-Speech-Detection-using-Generative-AI
pip install -r requirements.txt
```
## Preprocess Data
```bash
python preprocess.py --input_path path_to_data
```
## Train the Model
```bash
python train.py --model QLoRA
```
## Evaluate
```bash
python evaluate.py --test_data path_to_test_data
```