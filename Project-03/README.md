# Exercise 3 - Language Identification with CNNs



This project is about language identification using convolutional neural networks (CNNs).
In a first step, the most important distributional properties of the dataset are inspected and plotted.
The dataset contains a total of 65954 samples split into 52675 training samples and 13279 test samples.
Every sample comprises a "tweet" column with the textual content and a "label" column with the associated language.
The histogram shows that there are many labels with very low frequency (strong class imbalance).
For example 60 labels occur less than 100 times in the whole dataset.
However, English occurs more than 20,000 times. We are dealing with this class imbalance in a later step.
We merge the training and the test data into one dataframe for easier pre-processing and to ensure that training and test data comes from the same distribution
We saw that some languages/ labels do not appear in the training data while appearing in the test data and the other way around
Since this is not desirable we merge training and test data into one dataset and before starting to train we randomly shuffle and split into train and test data again. This ensures that all labels appear in the training and test data.

## Pre-Processing

We decided to use a very similar preprocessing process similar to project number 1.
First of all we remove patterns like retwees, hyperlinks, emojis, xml, hashtags which do not help with the classification.
Then we detect all languages with a small number of occurences (< 100). We use back translation and upsamling in order to increase the sample size to at least 100.
The labels are then transformed into indices and the tweets are tokenized and vectorized and then padded to all have a unit length of 80.
When then split the vectorized data into training and test data based on a 80:20 split. 10 percent of the training data is then used as validation data. 

## Part 1
We decided to build the CNNs using keras. We tried out different values for the optimizer, learning rate, dropout, number of filters, stride, kernel size, different pooling strategies and batch sizes. Since we are not dropping any classes neither from the training nor the train set we see that our best classifier
performs very well on average (Weighted F1 score of 97%). However, if you consider the macro F1 score (which weights the F1 equally for every label) you can 
see that the model performs not really well, because it only achieves a macro F1 of 50%. 
An easy trick in order to increase the macro F1 score, would be to drop all the labels with small sample size from the training and test set.

|Model Nr.|Optimzer|Learning Rate|Dropout Rate|#Filters|Stride|Kernel Size|Pooling|Batch Size|Accuracy|Macro F1|Weighted F1|
|-|-|-|-|-|-|-|-|-|-|-|-|
|1.|sgd|0.1|0.5|128|1|3|GlobalMaxPooling1D|64|0.84|0.19|0.83|
|2.|sgd|0.01|0.25|256|1|7|GlobalMaxPooling1D|128|0.89|0.15|0.88|
|3.|adam|0.01|0.25|512|2|3|GlobalMaxPooling1D|64|0.88|0.15|0.89|
|4.|adam|0.001|0.5|128|1|5|GlobalMaxPooling1D|64|0.95|0.5|0.94|
|5.|adam|0.001|0.25|128|1|5|GlobalMaxPooling1D|128|0.97|0.5|0.97|





## Part 2
Take the best performing model and evaluate it on the test set. We decided to evaluate model number 5 on the test data since it showed the best validation accuracy. Model number 5 yielded us with an accuracy of 92% and  

|Model Nr.|Optimzer|Learning Rate|Dropout Rate|#Filters|Stride|Kernel Size|Pooling|Batch Size|Accuracy|Macro F1|Weighted F1|
|-|-|-|-|-|-|-|-|-|-|-|-|
|5.|adam|0.001|0.2|128|1|5|GlobalMaxPooling1D|128|0.92|0.5|0.91|

## Part 3
Reason about the observed effects of your 5 best hyperparameter settings on model performance. You do not need to be sure that the reasons you provide are correct – the goal is to provide educated (or well-reasoned) guesses.

## Part 4
 Compare the outputs of the best CNN model to your best performing model from Exercise 1. Which classifier scores
 higher on the test set? Do you have an idea, why this might be?


Implement a language classifier in PyTorch or Keras-Tensorflow. We suggest reusing and adjusting the class structure from exercise 2 (which may be inspired by Rao and McMahan). However, you are free to create your own, new class structure. Keep in mind that for language classification we work on the character level. Thus, your Vocabulary class (that is, if you have one) will not hold a vocabulary of words, but a vocabulary of characters.

We merged the given training and test data into one dataset, so we had to write less code for the pre-processing.
At first we cleaned the data by removing emojis, twitter @ mentions, numeric patterns etc..
Since the tweet itself is the only featuretext corpus that we are given, we thought about possible features that we could engineer
and that would help us with classifying the language a tweet is written in.
