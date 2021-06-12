# Neural Machine Translation (NMT) with attention mechanism

This notebook focuses on training a Neural Machine Translation(NMT) model with and without attention mechanism to Translate sentences from English to Dutch language, and compare the results.

## Section 1- Data Collection and Preprocessing

The dataset to train the NMT system was available from the OPUS project (http://opus.nlpl.eu/).
- Language Selected: English(Source) - Dutch(Target)
- Corpus: Tatoeba v2021-03-10 -- en(English) - nl(Dutch)
NOTE: Downloaded zip file from moses link -> extracted files and renamed them to english.txt and dutch.txt

- Limited the number of sentences to 10,000 lines -- As per requirement of the assignment. We can increase the no. of sentences to give the model more data to train on and improve its performance. But this increase in training data also increases the training complexity as well as training resources.
- Adding '<bof>' to denote beginning of sentence and '<eos>' to denote the end of the sentence to each target line(Dutch Sentences).
- Perform the pre-processing step of the text - this includes converting all text to lowercase and removing punctuations(it can occur anytime and offers little help in translations).
- Print dataset statistics after preprocessing: 
	- Number of samples
	- Number of unique source and target language tokens
	- Max sentence length of source and target languages
	- Source Vocabulary and Target Vocabulary
- Split the data into train, development and test set