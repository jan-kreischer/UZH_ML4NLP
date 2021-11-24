# Project 5 (Sequence and Sentiment Classification using Transformers)

## Part 1 - Named Entity Recognition using BERT

**1.1 When initializing the BertForTokenClassification-class with BERT-base you should get a warning message. Explain why you get this message.**
```
Some weights of the model checkpoint at bert-base-german-cased were not used when initializing BertForTokenClassification:  
- This IS expected if you are initializing BertForTokenClassification from the checkpoint of a model  
trained on another task or with another architecture  
(e.g. initializing a BertForSequenceClassification model from a BertForPreTraining model).  
- This IS NOT expected if you are initializing BertForTokenClassification from the checkpoint of a model that you expect to be exactly identical   
(initializing a BertForSequenceClassification model from a BertForSequenceClassification model).  
Some weights of BertForTokenClassification were not initialized from the model checkpoint at bert-base-german-cased and are newly initialized:  
['classifier.bias', 'classifier.weight'].  
You should probably TRAIN this model on a down-stream task to be able to use it for predictions and inference.  
```

We added the received error message here in order to make clear what we are talking about.  
This error message is received because the BERT model ‘bert-base-german-cased’  
that we want to use for our BertForSequenceClassification model 
has been pre-trained on another architecture (BertForPreTraining). 
This means that the layers of our target architecture (BertForSequenceClassification), which are not present in our base
architecture (BertForPreTraining) will be randomly initialized.
This layers of our base model (BertForPreTraining), which are not part of our
target architecture (BertForSequenceClassification) will be discarded.
This means that the model has to be fine tuned on a down stream task in order to learn the proper weights in the randomly intialized layers.

**1.2 Which model performed best on the evaluation set?**. 

|Description|Approx Micro F1|Approx Macro F1| 
|---|---|---|
|Model fine-tuned with 1000 sentences (and non-frozen embeddings)|0.9064|0.3462|
|Model with 3000 sentences (and non-frozen embeddings)|0.9301|0.4655|
|Model with 3000 sentences (and frozen embeddings)|0.9047|0.1903|

**1.3 Are there differences between f1-micro and f1-macro score? If so, why?**. 
There are big differences between micro and macro f1.
The macro f1 metric is computed by independently computing the f1 score for each class/ label seperately and then taking the average 
(In this case all classes are weighted equally).  
The micro f1 is computed by weighting the f1 score of every class by the number of samples supporting this class  
(In this case the weight of a class is poportional to its number of samples).
The big negative deviation between micro and macro f1 just says that the model is performing well
for frequent classes of labels while performing worse for at least one minority class.
For example it might able to correctly label people with 'PER' and others with 'O' but it might be bad in 
correctly labeling 'ORG'.  
If the frequency of 'PER' and 'O' is much higher than the 'ORG' label entity, this leads to
a deviation in micro and macro f1 (Like we observerd).  

**1.4 How large is the performance gap between 1’000 and 3’000 sentences for finetuning?**.    
There is a performance gap between a BERT model being fine tuned on 1000 and 3000 sentences 
of ≈3\% micro F1 and ≈12\% macro F1. This performance difference is quite significant.
Therefore more fine tuning sampels certainly improved the performance.
It would be interesting how far you can increase the models performance by increasing the
amount of data used for fine tuning.

**1.5 Is it better to freeze or not to freeze the embeddings?**  
Since the performance of the model being trained on 3000 sentences with non frozen embeddings exceeds
the performance of the reference model, it is better to not freeze the embeddings.
This makes sense since the warning from 1.1 basically notifies us that the base model needs to
be fine tuned at first before using it. However, if the weights of the base model are frozen
then this fine tuning only happens in the final layer.
Therefore, for this task and base model it is better not to freeze the embeddings.
However, this depends on the specific base model and scenario.

## Part 2 - Resource Limited Competition: Sentiment Analysis
