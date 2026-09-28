# Results:

## E01 ## 
*train a trigram language model, i.e. take two characters as an input to predict the 3rd one. Feel free to use either counting or a neural net. Evaluate the loss; Did it improve over a bigram model?*

### Counting model Trigram, with prob matrix in shape (729, 27) ###
- Total Negative Log Likelihood: 504,653
- Amount Bigrams/Tokens: 228,146
- Average NLL per Bigrams/Tokens: **2.21197**

the overall performance improved slightly vs. the bigram count model.


### NN Trigram; weight matrix (729, 27) ###
- 1000 epochs with learning rate -50; regularization strength 0.01
- Average NLL per Bigrams/Tokens: **2.25059**

the overall performance improved slightly vs. the NN Bigram model (with same architecture, hyperparameters and epochs)

## E02 ##
*split up the dataset randomly into 80% train set, 10% dev set, 10% test set. Train the bigram and trigram models only on the training set. Evaluate them on dev and test splits. What can you see?*

### Counting model Bigram; prob matrix (27, 27) ###

NLL on whole set before splitting up:
- Total Negative Log Likelihood: 559,952
- Amount Bigrams/Tokens: 228,146
- Average NLL per Bigrams/Tokens: **2.45436**

NLL on dev split:
- Total Negative Log Likelihood: 55,711
- Amount Bigrams/Tokens: 22,696
- Average NLL per Bigrams/Tokens: **2.45468**

NLL in test split:
- Total Negative Log Likelihood: 56,125
- Amount Bigrams/Tokens: 22,859
- Average NLL per Bigrams/Tokens: **2.45525**

NLL stays roughly the same.

### Counting model Trigram; prob matrix (729, 27) ###

NLL on whole set before splitting up:
- Total Negative Log Likelihood: 504,653
- Amount Bigrams/Tokens: 228,146
- Average NLL per Bigrams/Tokens: **2.21197**

NLL on dev split:
- Total Negative Log Likelihood: 50,942
- Amount Bigrams/Tokens: 22,696
- Average NLL per Bigrams/Tokens: **2.24453**

NLL in test split:
- Total Negative Log Likelihood: 51,115
- Amount Bigrams/Tokens: 22,859
- Average NLL per Bigrams/Tokens: **2.23611**

NLL slightly worse compared to calculating it without splitting up.

### NN Bigram; weight matrix (27, 27) ###

NLL on whole set before splitting up:
- 1000 epochs with learning rate -50; regularization strength 0.01
- Average NLL per Bigrams/Tokens: **2.48045**

NLL on dev split:
- 1000 epochs with learning rate -50; regularization strength 0.01
- Average NLL per Bigrams/Tokens: **2.46008**

NLL in test split:
- 1000 epochs with learning rate -50; regularization strength 0.01
- Average NLL per Bigrams/Tokens: **2.46040**

NLL nearly identical after splitting the dataset.

### NN Trigram; weight matrix (729, 27) ###

NLL on whole set before splitting up:
- 1000 epochs with learning rate -50; regularization strength 0.01
- Average NLL per Bigrams/Tokens: **2.25059**

NLL on dev split:
- 1000 epochs with learning rate -50; regularization strength 0.01
- Average NLL per Bigrams/Tokens: **2.26259**

NLL on test split:
- 1000 epochs with learning rate -50; regularization strength 0.01
- Average NLL per Bigrams/Tokens: **2.25385**

NLL nearly identical after splitting the dataset.

## E03 ##
*use the dev set to tune the strength of smoothing (or regularization) for the trigram model - i.e. try many possibilities and see which one works best based on the dev set loss. What patterns can you see in the train and dev set loss as you tune this strength? Take the best setting of the smoothing and evaluate on the test set once and at the end. How good of a loss do you achieve?*

Trigram NN; weight matrix (729, 27)
- Basecase: NLL of 2.2 - 2.3 with learning rate -50; regularization strength 0.01 and several tousand epochs on dev_split / test_split
- lambda 0.1: 1k epochs: 2.27114 -> 2,5k epochs more: 2.25572; -> not convincing
- lambda 0.001: 1k epochs: 2.23897-> 2,5k epochs more: 2.23285; -> definitely better than 0.1 -> also better than with 0.01 -> i go with this lambda
Final step: 5k more epochs with lambda 0.001 -> training loss 2.19047 -> testset: **2.22169**
...

## E04 ##
*we saw that our 1-hot vectors merely select a row of W, so producing these vectors explicitly feels wasteful. Can you delete our use of F.one_hot in favor of simply indexing into rows of W?*

Replaced one-hot encoding with this line "logits = W[xs]"; improved the speed of epochs significantly
...

## E05 ##
*look up and use F.cross_entropy instead. You should achieve the same result. Can you think of why we'd prefer to use F.cross_entropy instead?*

Good fit for the model, less code
