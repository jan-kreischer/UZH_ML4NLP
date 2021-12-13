# Project 6 Topic Modeling

## Part 1 - Topic Modelling using LDA

**1.1 For each time-period assign a name to each generated topic based on the topic’s top words. List all topic names
in your report. **


**1.2 Do the topics make sense to you? Are they coherent? Do you observe trends? Discuss in 4-6 sentences**

|Description|Approx Micro F1|Approx Macro F1| 
|---|---|---|
|Model fine-tuned with 1000 sentences (and non-frozen embeddings)|0.9064|0.3462|
|Model with 3000 sentences (and non-frozen embeddings)|0.9301|0.4655|
|Model with 3000 sentences (and frozen embeddings)|0.9047|0.1903|

=> We can see that the model being fine tuned using 3000 sentences with non frozen base model parameters achieves the best performance.


## Part 2 - Resource Limited Competition: Sentiment Analysis

In Part 2, we are expected to submit a fine-tuned Transformer model for the IMDB Binary sentiment classification task. 

**2.1  Assign a name to each topic based on the topic’s top words (for each time-period). List all topic names in
your report.**

|model_name	|accuracy	|f1_macro	|f1_micro|
|--|--|--|--|
|distilbert-base-uncased-finetuned-sst-2-english|	0.8075|	0.806671|	0.8075|
|echarlaix/bert-base-uncased-sst2-acc91.1-d37-hybrid|	0.7055|	0.686775|	0.7055|
|gchhablani/bert-base-cased-finetuned-sst2|	0.8220|	0.821986|	0.8220|
|roberta-base|	0.5000|	0.333333|	0.5000|
|siebert/sentiment-roberta-large-english|	0.8880|	0.887986|	0.8880|

**2.2 Bianchi et al. 2021 claim that their approach produces more coherent topics than previous methods. Let’s test
this claim by comparing the coherence of the topics produced by CTM with the topics produced by LDA. Describe
your observations in 2-4 sentences.**


**2.3 Do the two models generate similar topics? Can you discover the same temporal trends (if there are any)?
Discuss in 4-6 sentences.**
