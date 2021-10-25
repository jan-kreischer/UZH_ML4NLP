Lab Report


In this project, we are asked to creat our own word-embedding using the Continuous-Bag-of-Word(CBOW) model based on two corpuses(hotel reviews and a scifi story) and test our embedding. We have build a CBOW2 model and make the hotel reviews dataset and the scifi text embeded in (Part1), and test the embedding (Part2). 


Part 1

- Hotel reviews dataset

After loading the data into colab, we firstly cleaned the data. For each of the reviews, substitute all numbers with spaces, make all alphabets lower case and delete all punctuation markes. After cleaning we get a list of reviews. Next, we delete all reviews that has less than 5 words, because to build a CBOW2 model, we need to have 4 content words(2 for the left and 2 for the right) for each of the target word. We also delete words that occurs only 1 time, since they are likely to be misspelled.

Wtih the reviews list, we then built the vocabulary list with all unique words of this dataset, with which we can later build the word2index and index2word dictionaries. This two dictionary will help us to map word to number during embedding.

Next, for every review in the reviews list, we creat tuples for every target word. The tuple contains the target word itself and a list composed of its former 2 words and later 2 words. These tuples are later transformed to tensor.

Then we defined a CBOW models with two linear layers, one of which is followed by a ReLU activation function and the other of which is followed by a LogSoftmax function. A batch size of 128, the dimension of 50 are set and then the tensor is passed into the model to train for 15 epoches.

- Scifi dataset

For the scifi dataset, the processing is very much the same. Firstly clean the numbers and all punctional marks. Then we get the word list and the unique vocabularies list to form the word2list dictionary to map the words to numbers.



We didn't do the optional CBOW5 part, because the processes to build a CBOW5 model is basically the same except building a longer content for each of the target. As for the performance result, as we discussed in the lecture, the CBOW5 model is more sementic and CBOW2 model is more syntactic in most of the cases.



Part 2

In Part 2, we are asked to find 3 nouns, 3 verbs and 3 adjectives from different frenquencies. So we takes 3 slices of words with different frequencies from the vocabulary of both dataset. 

|    frequency  |selected words|5 closest neighbours|
|--------------|-----------------|--------------------|
| high frequnt |        hotel      |   0           |
||1|
||2|
||3|
||4|
