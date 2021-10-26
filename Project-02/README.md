# Project 2 Report
## *CBOW Word embedding with PyTorch* <br/><br/>


In this project, we are asked to creat our own word-embedding using the Continuous-Bag-of-Word(CBOW) model with two corpuses(hotel reviews and a scifi story) and test our embeddings. We have build a CBOW2 model and make the hotel reviews dataset and the scifi text embeded in (Part1), and test the embedding (Part2). 


## Part 1


- **Preprocessing**

- Hotel reviews dataset

After loading the data into colab, we firstly cleaned the data. For each of the reviews, substitute all numbers with spaces, make all alphabets lower case and delete all punctuation markes. After cleaning we get a list of reviews. Next, we delete all reviews that has less than 5 words, because to build a CBOW2 model, we need to have 4 content words(2 for the left and 2 for the right) for each of the target word. We also eliminate words that occurs only 1 time, since they are likely to be misspelled.

- Scifi dataset

For the scifi dataset, the processing is very much the same. Firstly clean the numbers and all punctional marks. Then we get the word list and the unique vocabularies list to form the word2list dictionary to map the words to numbers. We then eliminate words that occurs less than 100 time. In this relatively large corpus, we consider words occuring less than 100 times as uncommon words. They very much influence the training outcome.


- **Embedding**

Wtih the word list, we then built the vocabulary list with all unique words, with which we can later build the word2index and index2word dictionaries. This two dictionary will help us to map word to number during embedding.
Next, for the hotel reviews dataset, for every review in the reviews list, we create tuples for every target word. The tuple contains the target word itself and a list composed of its former 2 words and later 2 words. These tuples are later transformed to tensor.
Then we defined a CBOW models with two linear layers, one of which is followed by a ReLU activation function and the other of which is followed by a LogSoftmax function. A batch size of 128, the dimension of 50 are set and then the tensor is passed into the model to train for 30 epoches. For the scifi text dataset, the embedding is the same except that the text is all in one string instead of a list.


We didn't do the optional CBOW5 part, because the processes to build a CBOW5 model is largely the same except building a longer content for each of the target. As for the performance result, as we discussed in the lecture, the CBOW5 model usually gets a more sementic result and the CBOW2 result is more syntactic in most of the cases.

## Part 2

In Part 2, we are asked to find 3 nouns, 3 verbs and 3 adjectives from different frenquencies. So we takes 3 slices of words with different frequencies from the vocabulary of both dataset. 

-The 9 chosen words from the hotel review dataset and their neighbours are as follows:
|    frequency  |selected words|5 closest neighbours|
|--------------|-----------------|--------------------|
|high frequnt|        hotel      |'tuilieres', 'overload', 'bam', 'asun', 'visiting'|
|high frequnt|great|'fantastic', 'excellent', 'superb', 'best', 'palmetto'|
|high frequnt|clean|'beds', 'kalverstraat', 'bathrooms', 'victorian', 'spacious'|
|medium frequent|issue|'amzing', 'hawai', 'talk', 'greasy', 'like'|
|medium frequent|adequate|'small', 'tiananmen', 'single', 'expecting', 'wood'|
|medium frequent|smoking|'suitehotel', 'scenarios', 'legacy', 'caretakers', 'pillow'|
|least frequent|italy|'hotel', 'embargo', 'declare', 'crazy', 'hairstylist'|
|least frequent|filled|'stupid', 'hanson', 'fra', 'ankle', 'caren'|
|least frequent|comment|'hotel', 'bedding', 'intensive', 'walls', 'definitely'|

We can see that some of the neighbours given by the models makes sense while others does not. For higher frequent and explicit adjuestives, such as "great", the training result('fantastic', 'excellent', 'superb', 'best', 'palmetto') is more satisfactory. The first 4 are synonyms and the last one('palmetto') is like to be in a good hotel. While teh result for the others less frequent words, such as "common" or other ambiguous word such as "clean", "filled"(in terms of part of speech: can be a verb or a adj) are less satisfactory. 

-The 9 chosen words from the scifi text and their neighbours are as follows:
|    frequency  |selected words|5 closest neighbours|
|--------------|-----------------|--------------------|
|high frequnt|time|'said', 'first', 'thought', 'made', 'like'|
|high frequnt|think|'know', 'tell', 'enough', 'want', 'sure'|
|high frequnt|right|'said', 'man', 'made', 'course', 'little'|
|medium frequent|blood|'single', 'small', 'back', 'little', 'light'|
|medium frequent|smile|'power', 'ship', 'back', 'right', 'said'|
|medium frequent|tiny|'small', 'dark', 'turned', 'came', 'bright'|
|least frequent|party|'course', 'way', 'point', 'man', 'men'|
|least frequent|worry|'seems', 'however', 'right', 'girl', 'must'|
|least frequent|warm|'watched', 'snapped', 'went', 'saw', 'looking'|

As for the scifi dataset, the result is less satisfactory compared to the hotels reviews dataset. The difference in the result could be firstly caused by the difference between novel and reviews. In reviews, the sentence and phrases are more repetitive and the the use case are more explicit and fix. The second reason might be that the scifi model are not fully training.

We then chose two words \['good', 'job'] to get the 5 cloest neighbours from both of the datasets and the result is as follows:

| dataset  |selected word|5 closest neighbours|
|--------------|-----------------|--------------------|
|hotel reviews|good|'amandari', 'blooming', 'best', 'great', 'decent'|
|hotel reviews|job|'nameless', 'experience', 'precinct', 'bouncy', 'whopping'|
|scifi|good|'time', 'said', 'knew', 'like', 'first'|
|scifi|job|'even', 'work', 'point', 'time', 'though'|

Their neigbours in different dataset are different since in different use cases the words are used differently and the neighbouring words used with them are very different. For example in hotel dataset, when a customer comments that a hotel is good, he or she may mean that the hotel is decent, so when we train a hotel model. The model put these vertors('good','best', 'great', 'decent') closer. However, "decent" is not a common word in the scifi dataset, saying 'good' in the scifi text may means the timing is good. So the training data has every much influenced the result.
