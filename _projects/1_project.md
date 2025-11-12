---
layout: page
title: Translators Comparison — Google vs AI4Bharat (IndicTrans2)
description: STS & BLEU evaluation of Google Translate vs. AI4Bharat’s IndicTrans2 on IIT-Bombay Hindi–English data.
img: assets/img/translators.png  # optional: add an image at this path or delete this line
importance: 5
category: Machine Learning and Deep Learning
---

<!-- top-only button -->
<div class="mb-3">
  <a class="btn btn-sm btn-primary" href="https://github.com/Chava-Sai/Translators_Comparsion" target="_blank" rel="noopener">Code</a>
</div>

## Problem Statement
In light of Google Translate’s weaknesses for low-resource and certain Indic languages, can we identify a stronger alternative?  
How do those alternatives compare on **accuracy** and **semantic fidelity** across diverse linguistic contexts?

<div class="d-flex gap-3 my-3">
  <img src="https://i.imgur.com/pDtiiou.png" width="120" alt="Google Translate logo">
  <img src="https://i.imgur.com/0JSSL2o.png" width="130" alt="AI4Bharat logo">
</div>

## Dataset
We use the **IIT Bombay** Hindi–English parallel corpus (Kaggle mirror), ~**1M** sentence pairs.

## Methodology (Hindi → English)
1. Feed Hindi sentences to **two translators** (Google Translate and **IndicTrans2**).  
2. Compare each translation to the **reference English** using:
   - **STS** (Semantic Textual Similarity; 0–1 scale)  
   - **BLEU** (n-gram overlap)

## Google Translate — Neural Machine Translation (NMT)
Google Translate uses NMT trained on large bilingual corpora and attention-based architectures.

<div class="my-2">
  <img src="https://i.imgur.com/OelpDRU.png" alt="Google NMT Architecture" class="img-fluid rounded z-depth-1">
</div>

### Sample Translations (Google)
<table class="table table-sm">
  <thead><tr><th>Hindi</th><th>Reference English</th><th>Google Translation</th></tr></thead>
  <tbody>
    <tr>
      <td>ऐ मेरे बन्दों! आज न तुम्हें कोई भय है और न तुम शोकाकुल होगे।</td>
      <td>“O My servants, today no fear is on you, neither do you sorrow”</td>
      <td>O my prisoners! Today you have no fear nor you will be heartbroken</td>
    </tr>
    <tr>
      <td>वही है जो आकाशों में भी पूज्य है और धरती में भी पूज्य है और वह तत्वदर्शी, सर्वज्ञ है</td>
      <td>And it is He who in heaven is God and in earth is God; He is the All-wise, the All-knowing.</td>
      <td>He is the one who is also revered in the sky and is also revered in the earth and he is a philosopher, omnisc.</td>
    </tr>
    <tr>
      <td>रहे वे लोग जिन्होंने इनकार किया, तो उनके लिए तबाही है। और उनके कर्मों को अल्लाह ने अकारथ कर दिया</td>
      <td>But as for the unbelievers, ill chance shall befall them! He will send their works astray.</td>
      <td>Those who refused, so there is havoc for them. And Allah made their deeds unconscious</td>
    </tr>
    <tr>
      <td>फिर कैसी रही मेरी यातना और मेरे डरावे?</td>
      <td>How then were My chastisement and My warnings?</td>
      <td>Then how was my torture and my scared?</td>
    </tr>
  </tbody>
</table>

## AI4Bharat — IndicTrans2
Transformer-based **encoder–decoder** adapted for Indic languages; script unification (e.g., to Devanagari) improves lexical sharing and translation quality.

<div class="my-2">
  <img src="https://i.imgur.com/oaxPIK1.png" alt="IndicTrans2 Encoder–Decoder" class="img-fluid rounded z-depth-1">
</div>

### Sample Translations (IndicTrans2)
<table class="table table-sm">
  <thead><tr><th>Hindi</th><th>Reference English</th><th>IndicTrans2 Translation</th></tr></thead>
  <tbody>
    <tr>
      <td>ऐ मेरे बन्दों! आज न तुम्हें कोई भय है और न तुम शोकाकुल होगे।</td>
      <td>“O My servants, today no fear is on you, neither do you sorrow”</td>
      <td>O My servants! Today you will have no fear nor will you grieve</td>
    </tr>
    <tr>
      <td>वही है जो आकाशों में भी पूज्य है और धरती में भी पूज्य है और वह तत्वदर्शी, सर्वज्ञ है</td>
      <td>And it is He who in heaven is God and in earth is God; He is the All-wise, the All-knowing.</td>
      <td>He is the one who is God in the heavens and God on the earth. He is the Wise and the All Knowing.</td>
    </tr>
    <tr>
      <td>रहे वे लोग जिन्होंने इनकार किया, तो उनके लिए तबाही है। और उनके कर्मों को अल्लाह ने अकारथ कर दिया</td>
      <td>But as for the unbelievers, ill chance shall befall them! He will send their works astray.</td>
      <td>But as for those who disbelieve, for them is perdition. And He will waste their deeds.</td>
    </tr>
    <tr>
      <td>फिर कैसी रही मेरी यातना और मेरे डरावे?</td>
      <td>How then were My chastisement and My warnings?</td>
      <td>How [terrible] were My punishment and My warnings!</td>
    </tr>
  </tbody>
</table>

## Metrics — STS & BLEU
**STS** measures meaning similarity on a 0–1 scale: 0 = none, 0.5 = moderate, 1 = identical meanings.  
**BLEU** captures n-gram overlap with the reference.

<div class="text-center my-2">
  <img src="https://i.imgur.com/eBAxmSq.png" width="250" alt="STS scale" class="img-fluid rounded z-depth-1">
</div>

## Results (examples)
<table class="table table-sm">
  <thead>
    <tr>
      <th>Reference English</th>
      <th>Google</th>
      <th>IndicTrans2</th>
      <th>STS (G)</th>
      <th>STS (I2)</th>
      <th>BLEU (G)</th>
      <th>BLEU (I2)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>O My servants, today no fear is on you, neither do you sorrow</td>
      <td>O my prisoners! Today you have no fear nor you will be heartbroken</td>
      <td>O My servants! Today you will have no fear nor will you grieve</td>
      <td>0.2912</td>
      <td>0.5101</td>
      <td>0.0026</td>
      <td>0.0159</td>
    </tr>
    <tr>
      <td>And it is He who in heaven is God and in earth is God; He is the All-wise, the All-knowing.</td>
      <td>He is the one who is also revered in the sky … philosopher, omnisc.</td>
      <td>He is the one who is God in the heavens … the Wise and the All Knowing.</td>
      <td>0.0531</td>
      <td>0.9191</td>
      <td>0.0055</td>
      <td>0.0098</td>
    </tr>
    <tr>
      <td>But as for the unbelievers, ill chance shall befall them! He will send their works astray.</td>
      <td>Those who refused … Allah made their deeds unconscious</td>
      <td>But as for those who disbelieve … He will waste their deeds.</td>
      <td>0.0000</td>
      <td>0.7391</td>
      <td>0.0000</td>
      <td>0.0566</td>
    </tr>
    <tr>
      <td>How then were My chastisement and My warnings?</td>
      <td>Then how was my torture and my scared?</td>
      <td>How [terrible] were My punishment and My warnings!</td>
      <td>0.0000</td>
      <td>0.2606</td>
      <td>0.0000</td>
      <td>0.0039</td>
    </tr>
  </tbody>
</table>

## Takeaways
- **IndicTrans2** consistently shows **higher STS** and **better BLEU** on challenging religious and formal text styles.  
- Script unification + Indic pretraining help preserve **semantic nuance** in morphologically rich languages.

---
**Repo:** <a href="https://github.com/Chava-Sai/Translators_Comparsion" target="_blank">Translators_Comparsion</a>