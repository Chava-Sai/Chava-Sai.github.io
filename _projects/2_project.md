---
layout: page
title: IIITDWD_SVC — DravidianLangTech 2024
description: Breaking Language Barriers — Hate-Speech Detection in Telugu–English Code-Mixed Text (Rank 14, F1 = 0.6565)
img: /assets/img/projects/dravidianlangtech.jpg   # optional preview image
importance: 2
category: work
links:
  - name: code
    url: https://github.com/Chava-Sai/IIITDWD_SVC-DravidianLangTech-2024
  - name: publication
    url: https://aclanthology.org/2024.dravidianlangtech-1.19/
---

## Overview
Social media platforms foster communication but also amplify **hate and offensive language**.  
The **DravidianLangTech @ EACL 2024** shared task addressed **hate-speech detection** in **Telugu–English (Tenglish)** code-mixed YouTube comments, classifying them as *hate* or *non-hate*.  
Our team **IIITDWD_SVC** developed a multilingual NLP pipeline integrating transliteration, translation, and fine-tuned transformer models.

<p align="center">
  <img src=assets/img/IIITDWD_architecture.png alt="Architecture diagram" width="600">
</p>

---

## Dataset
Dataset provided by the competition organizers.  
Collected from **YouTube comments** and annotated for hate vs. non-hate.

| Split | Hate | Non-Hate | Total |
|:------|-----:|---------:|------:|
| Train | 1939 | 2061 | 4000 |
| Test  | 250  | 250  | 500  |

---

## Methodology
1. **Transliteration** — Convert Telugu content written in Latin script → Telugu script using *IndicXlit*.  
2. **Translation** — Translate Telugu → English via *IndicTrans2* for compatibility with English transformer models.  
3. **Tokenization & Training** — Use Hugging Face tokenizers per model; train and fine-tune with balanced batches.

### Models Used
- **BERT-Base Uncased** — contextual embeddings baseline.  
- **Hate-BERT** — pre-trained on banned Reddit posts for abusive language detection.  
- **XLM-RoBERTa** — cross-lingual model trained on 100 languages including Telugu & English.

---

## Results
Evaluation metric: **Macro F1 Score**  
Our **BERT-based model ranked 14th overall** among submissions.

| Team | F1 Score | Rank |
|:------|:--------:|:----:|
| Sandalphon | 0.7711 | 1 |
| **IIITDWD_SVC** | **0.6565** | **14** |

---

## Installation & Usage
```bash
# clone the repo
git clone https://github.com/Chava-Sai/IIITDWD_SVC-DravidianLangTech-2024.git
cd IIITDWD_SVC-DravidianLangTech-2024
pip install -r requirements.txt
```
## Pre-Process
```bash
python preprocess.py --data_path path_to_data
```
## Train
```bash
python train.py --model bert
```
## Evaluate
```bash
python evaluate.py --model bert
```