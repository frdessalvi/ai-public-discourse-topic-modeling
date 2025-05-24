# Invesigating public concerns about AI: A Comparative Topic Modeling Analysis of Tweets and News Articles
*Language Technology course final project*  
Elisa Degara, Francesca Dessalvi, Clara Montemurro, Tommaso Giacomello
## Overview
Artificial intelligence (AI) is increasingly influencing a wide range of social, economic, and technological domains. While public discourse reflects optimism about its potential, it also reveals persistent anxieties and criticisms about the consequences of this technology. Understanding these concerns is not only key to evaluating sentiment, but also to anticipating societal response, informing policy, guiding responsible communication against public misunderstanding, and identifying risks of misinformation/disinformation. In this work we investigate public concerns about artificial intelligence (AI) by comparing their expression in traditional and social media. Using a curated set of English-language news articles and tweets from X (formerly Twitter), available on Kaggle, we isolated negatively framed content. For tweets,
we manually annotated posts and fine-tuned a sentiment classifier (Twitter-RoBERTa) to extract negative opinions. We then applied three topic modeling methods (LDA, NMF, SVD) to both corpora. Based on coherence scores and interpretability, we selected NMF and manually refined its output into a taxonomy of concerns. Our findings reveal both shared and medium specific anxieties: tweets emphasize speculative, emotional fears, while news articles focus on institutional and ethical risks. This analysis highlights how public narratives about AI are shaped by platform dynamics and communication norms.

## Data

- **Tweets**: Collected from a Kaggle dataset of ~20,000 English-language tweets (July–November 2024), filtered for relevant AI-related terms and manually annotated for sentiment.
- **News Articles**: Retrieved from LexisNexis (500 English-language articles, June–December 2024), filtered for negative framing and manually extracted concern-focused sentences.

Due to licensing and privacy constraints, datasets are not included in this repository.

## Methodology

- **Sentiment Classification**: Fine-tuned a Twitter-RoBERTa model on a subset of manually annotated tweets to classify sentiment as positive, neutral, or negative.
- **Preprocessing**: Cleaned and lemmatized texts, removed noise, and extracted frequent bigrams to enhance topic modeling.
- **Topic Modeling**: Applied LDA, NMF, and SVD to both corpora. Selected NMF based on coherence scores and interpretability.
- **Taxonomy Construction**: Manually refined NMF outputs into human-labeled categories of concern, specific to each medium.

  ## Key Findings
- **Tweets** tended to focus on emotional and speculative concerns such as bots, deepfakes, and AI in warfare.
- **News articles** focused more on institutional risks like privacy, algorithmic bias, and job displacement.
- These differences suggest that platform dynamics shape how AI-related concerns are framed and communicated.

## Limitations and Future Work

- **Dataset constraints**: The tweet dataset was sourced from a publicly available Kaggle collection and may not fully represent the diversity of public opinion. Similarly, the news articles were limited to English-language sources from the LexisNexis database, potentially excluding relevant perspectives from other media outlets or regions.
  
- **Lack of demographic metadata**: Without user-specific or publication-specific context, we were unable to explore how AI concerns vary across demographic groups.

- **Contextual limitations in social media**: Tweets were analyzed in isolation, without considering reply threads or user histories. This prevented a deeper understanding of conversational dynamics or influence patterns.

- **Manual interpretation of topics**: While NMF provided interpretable topic structures, the process of refining and labeling these topics was subjective, and subtle or overlapping meanings may have been missed.

For future work, we propose extending the analysis to:
- Include a broader range of media sources, languages, and timeframes.
- Analyze temporal sentiment shifts and reactions to specific AI-related events.
- Integrate conversation threads or network structures from social media to better understand discourse dynamics and the spread of concerns.
- Explore demographic or geographic segmentation where possible to tailor insight toward specific populations.




