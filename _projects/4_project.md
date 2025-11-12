---
layout: page
title: Fake and Hate Speech Detection in Multilingual Social Media Text
description: Multi-task learning model for detecting fake news and hate speech in multilingual, code-mixed text using embeddings, clustering, and shared neural layers.
img: assets/img/fakehate.png   # preview image on projects grid
importance: 4
category: work
---

<!-- top-only button -->
<div class="mb-3">
  <a class="btn btn-sm btn-primary" href="https://github.com/Chava-Sai/Fake-Hate-Investigating-the-role-of-fake-narratives-in-spreading-hateful-reactions" target="_blank" rel="noopener">Code</a>
</div>

## Overview
This project focuses on identifying **fake news** and **hate speech** in multilingual social media posts, leveraging transliteration, translation, embedding extraction, and clustering techniques to improve detection accuracy.

<div class="text-center my-3">
  <img src="https://i.imgur.com/a4msRUM.png" alt="Model Flow" class="img-fluid rounded z-depth-1" width="700">
</div>

---

## Features
- **Transliteration & Translation** — Convert *Hinglish* text to Hindi and English using *IndicXlit* and *IndicTrans2*.
- **Embedding Extraction** — Use pre-trained models like *BERT*, *XLM-RoBERTa*, *ALBERT*, *Electra*, and *mBERT*.
- **Cluster-Based Feature Engineering** — Compute distances from cluster centers for enhanced representation.
- **Multi-Task Architecture** — Shared layers for simultaneous *Fake Detection* and *Hate Detection*.

---

## Model Architecture

### Preprocessing
1. **Text Cleaning:** Remove symbols, punctuation, and normalize emojis.  
2. **Transliteration:** Convert Hinglish → Hindi using *IndicXlit*.  
3. **Translation:** Translate Hindi → English using *IndicTrans2*.  

### Embedding Extraction
Embeddings generated from:
- **BERT**
- **XLM-RoBERTa**
- **ALBERT**
- **Electra**
- **mBERT**

### Multi-Task Learning
Architecture includes:
- **Shared Layers** — Used by both fake and hate classifiers.  
- **Branch 1:** Fake detection.  
- **Branch 2:** Hate detection.  
- **Cluster Features:** Added as auxiliary signals.


---

## Visualization

### Cluster Formation & Distance Calculation

<div class="row">
  <div class="col-sm-6 text-center">
    <p><strong>Cluster formation (t-SNE)</strong></p>
    <img
      src="{{ '/assets/img/TSNE.png' | relative_url }}"
      alt="t-SNE visualization of route clusters"
      class="img-fluid rounded z-depth-1"
      loading="lazy"
    >
    <p class="caption text-muted mt-1">t-SNE projection of route embeddings colored by cluster.</p>
  </div>

  <div class="col-sm-6 text-center">
    <p><strong>Distance calculation / accuracy</strong></p>
    <img
      src="{{ '/assets/img/Accuracy.png' | relative_url }}"
      alt="Accuracy over epochs for cluster-distance features"
      class="img-fluid rounded z-depth-1"
      loading="lazy"
    >
    <p class="caption text-muted mt-1">Training accuracy trend with distance-to-centroid features.</p>
  </div>
</div>

### Results Comparison
<div class="row my-3">
  <div class="col-sm-6 text-center">
    <p><strong>Fake Detection Results</strong></p>
    <img src="https://i.imgur.com/dCszwHq.png" alt="Fake Detection Results" class="img-fluid rounded z-depth-1" width="420">
  </div>
  <div class="col-sm-6 text-center">
    <p><strong>Hate Detection Results</strong></p>
    <img src="https://i.imgur.com/S1EkNta.png" alt="Hate Detection Results" class="img-fluid rounded z-depth-1" width="420">
  </div>
</div>

---

## Results
| Model        | Task             | F1 Score (No Clusters) | F1 Score (With Clusters) |
|:-------------|:-----------------|:----------------------:|:------------------------:|
| **BERT**     | Hate Detection   | 81.97 | **97.15** |
| **Electra**  | Fake Detection   | 70.16 | **73.11** |
| **XLM-RoBERTa** | Hate Detection | 77.99 | **78.75** |
| **XLM-RoBERTa** | Fake Detection | 72.96 | **76.21** |

<div class="text-center my-2">
  <img src="https://i.imgur.com/a4msRUM.png" alt="Final Architecture Overview" class="img-fluid rounded z-depth-1" width="700">
</div>

---

## Installation

```bash
git clone https://github.com/Chava-Sai/Fake-and-Hate-Speech-Detection
cd Fake-and-Hate-Speech-Detection
pip install -r requirements.txt
```

## Preprocess Data

```bash
python preprocess.py --input_path path_to_data
```

## Train the Model

```bash
python train.py --model multi_task_model
```

## Evaluate

```bash
python evaluate.py --test_data path_to_test_data
```