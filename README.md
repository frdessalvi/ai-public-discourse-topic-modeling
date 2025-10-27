# Investigating Public Concerns about AI  
*A Comparative Topic Modeling Analysis of Tweets and News Articles*

Artificial Intelligence (AI) is rapidly transforming social, economic, and technological domains. Public discourse reflects both optimism about its potential and persistent anxieties about its risks. Understanding these concerns is crucial for anticipating societal responses, guiding policy, and countering misinformation.

This project analyzes how public concerns about Artificial Intelligence (AI) are expressed across **social** and **traditional** media, combining **sentiment classification** and **topic modeling**. It was developed as the final project of a *Language Technology  (NLP)* course.

---

## Dataset Overview

| Source | Size / Period | Description |
|---------|---------------|-------------|
| **Tweets (X)** | ~20,000 English tweets (Jul 2023–Nov 2024) | Filtered for AI-related terms, manually annotated for sentiment. |
| **News Articles** | 500 English articles (Jun 2023–Dec 2024) | Retrieved from LexisNexis; manually extracted concern-focused sentences. |

> Due to licensing and privacy constraints, datasets are not included in this repository. Scripts and configs can reproduce the pipeline on equivalent data.

---

## Methodology

### 1. Sentiment Classification

We fine-tuned a `Twitter-RoBERTa-base` model on **2 000 manually annotated tweets** to classify overall sentiment toward AI as **negative**, **neutral**, or **positive**.  

| Model | Accuracy | Macro-avg F1 | Notes |
|--------|-----------|--------------|-------|
| Baseline (LogReg + TF-IDF) | 0.651 | 0.642 | Simple linear baseline |
| DistilBERT | 0.654 | 0.631 | Lightweight transformer |
| **Twitter-RoBERTa-base** | **0.698** | **0.694** | Best performance |

> `Twitter-RoBERTa-base` achieved the highest accuracy and macro-F1, confirming the value of pre-training on Twitter data for this domain.

Tweets predicted as *negative* were retained for subsequent topic modeling.

---
### 2. Text Preprocessing
- Lowercasing, punctuation & stopword removal  
- Lemmatization (SpaCy)  
- POS filtering (nouns, verbs, adjectives, adverbs)  
- Bigram extraction using **NPMI > 0.5** and occurring in ≥2 documents 
- Vocabulary filtering: removed overly common (>50% for news, >70% for tweets) or too rare terms (<2 documents for news, <10 for tweets)  
- Representations: **TF–IDF** for `NMF` and `SVD`, **Bag-of-Words** for `LDA`

---
### 3. Topic Modeling

We applied **LDA**, **NMF**, and **SVD** to both the tweet and news corpora after identical preprocessing.  
To select the best model, we combined two coherence metrics — semantic (`Cv`) and statistical (`UMass`) — into a weighted score:

`Score = 0.75 × Cv + 0.25 × UMass`.

| Model | Tweets (Normalized Cv) | News (Normalized Cv) |
|--------|------------------------|----------------------|
| LDA | 0.25 | 0.52 |
| **NMF** | **1.00** | **0.99** |
| SVD | 0.13 | 0.25 |

A one-sided **Wilcoxon signed-rank test** (*p* < 1×10⁻⁴) confirmed that **NMF** significantly outperformed LDA and SVD across both corpora.  
After manual refinement of NMF topics, coherence further improved:  
- **Tweets:** 0.60 → 0.82  
- **News:** 0.49 → 0.75  

> **Result:** NMF yielded the most interpretable and coherent topics, making it the preferred model for final taxonomy construction.

---
## Results 

After identifying **NMF** as the most coherent model, we manually grouped its topics into broader, human-labeled categories of public concern.  
Overlapping topics were merged under unified, descriptive labels, producing the following **refined taxonomies** for news and tweets.

| Medium | Refined Categories of Concern | Description |
|---------|------------------------------|--------------|
| **News** | 1. AI & automation substituting human labor<br>2. Algorithmic bias (incl. gender bias)<br>3. Abusive use of Generative AI (e.g., child imagery)<br>4. Deceptive AI in crime and scams<br>5. General existential threat posed by AI<br>6. Privacy & data security | Structured, analytical framing focused on institutional, ethical, and societal risks. |
| **Tweets** | 1. Bot activity<br>2. AI substituting human labor<br>3. Fears of AI in warfare and geopolitics<br>4. General existential threat posed by AI<br>5. Misinformation and deepfakes<br>6. AI’s influence on thinking and education | Emotional, speculative engagement reflecting personal fears and reactive discourse. |

> Both media highlight similar concerns but diverge in framing.  
> **Tweets** emphasize *speculative and personal* fears (bots, militarized AI, misinformation), whereas **news articles** stress *institutional and ethical* issues (job automation, bias, privacy).
> These contrasts illustrate how platform dynamics and communication norms shape AI narratives.

---

## Limitations and Future Work

- **Dataset coverage:** Public Kaggle and LexisNexis subsets may not reflect the full diversity of opinions.  
- **Lack of demographics:** User- or publication-level context not available.  
- **Manual refinement:** Human labeling of topics can be subjective.

**Future extensions**
- Broaden media sources and time frames  
- Track temporal shifts in AI discourse  
- Integrate conversation-level structures for tweets

---

## References
- **Twitter-RoBERTa-base** — [Hugging Face Model Card](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment)  
  *Barbieri et al., “TweetEval: Unified Benchmark and Comparative Evaluation for Tweet Classification,” ACL 2020.*

- **DistilBERT** — [Hugging Face Model Card](https://huggingface.co/distilbert-base-uncased)  
  *Sanh et al., “DistilBERT, a distilled version of BERT,” arXiv:1910.01108 (2019).*
---

*Authors:* Elisa Degara · Francesca Dessalvi · Clara Montemurro · Tommaso Giacomello  
*Course:* Language Technology, 2025 – Bocconi University





