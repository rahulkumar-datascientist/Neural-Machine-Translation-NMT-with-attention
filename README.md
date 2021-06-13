# Neural Machine Translation (NMT) with attention mechanism

This notebook focuses on training a Neural Machine Translation(NMT) model with and without attention mechanism to Translate sentences from English to Dutch language, and compare the results.

## Section 1 - Data Collection and Preprocessing

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
- Assign each unique word an integer value for both the source and target vocabulary. As we need the sentences mapped to its respective integer sequence to train the neural net model.
- Using pre-trained GloVe embedding, I map the source vocabulary token(word) to its respective 100 - Dimensional vector.

## Section 2 - Translation Model training using Seq2Seq model
	
<p align="center">
  <img src="https://lena-voita.github.io/resources/lectures/seq2seq/general/enc_dec_linear_out-min.png" width=650>
</p>

- Defined Encoder Architecture
	- Mapping each source token in the sentence to its corresponding vector representation(embedding).
	- Passing the embeddings to the LSTM layer and save the final cell state and hidden values.
- Defined Decoder Architecture
	- Mapping each target token in the sentence to the latent dimension(output dimension). - This helps in learning the target tokens vector representation(embedding). 
	- Passing the embedded decoder sentence and the previous encoder states(saved above) to the LSTM layer and get the decoded output.
	- Pass the decoded sequence through a dense layer using 'softmax' activation function to get the final decoded sentence.
- Create the model by passing encoder input sequence and decoder input sequence as the inputs and decoded sequence as output.
- Trained the model by the help of callbacks and compare the training v/s validation accuracy.

## Section 3 - Testing

- I test the model using the test set by passing the test sentence and getting the translated sentence and evaluate it using the BLEU metric.
- Used the nltk library to calculate the sentence and corpus level BLEU score for each of the 1, 2, 3 and 4-gram sequence.

## Section 4 - Using the Attention mechanism to train the Seq2Seq model

<p align="center">
  <img src="https://lena-voita.github.io/resources/lectures/seq2seq/attention/general_scheme-min.png" width=650>
</p>
	

- Using the same Encoder and Decoder architecture with minute changes.
- We save all the intermediate cell state and hidden values of the encoded sequence.
- Calculate the DOT product of the input encoded sequence(coming from Encoder) and decoded output sequence(coming from Decoder) and pass it through Softmax layer. - This value informs us about how much each word is activating.
- We then again calculate the DOT product of the previous step and encoder input sequence to get the context and the attention score.
- Then I add the context and the decoded output sequence and pass them through the time-distributed layer to get the final output.
- created the model and trained tested and evaluated using the BLEU metric.

image reference : https://lena-voita.github.io/resources/lectures/seq2seq/general/enc_dec_linear_out-min.png and https://lena-voita.github.io/resources/lectures/seq2seq/attention/general_scheme-min.png
