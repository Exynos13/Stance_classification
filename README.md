# Stance Classification  of Tweets

## Description
Building a model to perform stance classification on tweets data i.e. to understand what is the stance of the author of the tweet to a particular target whether they are for it or against it.

## Data 
e data used from the dataset “Semeval-2016 Task 6: Detecting Stance in Tweets. Saif M. Mohammad et. al. In Proceedings of the International Workshop on Semantic Evaluation (SemEval-16). June 2016.” Which consists of tweets, targets and their stance labels.

## Data Processing
### Data Splitting
The dataset had two sets of data for training and testing. The Train dataset was split into two sets to perform training and validation based on stratification on the target class to ensure that the proportion of the data of the targets are equally present in both training and the validation sets.

### Data Augmentation
In order to mitigate the problem of imbalance, data augmentation was used in the minority classes for each target to give a better representation of the minority classes for the model while training. Thus avoiding the bias in the return. The techniques used for per forming augmentation was:
(a)replacing words with their synonyms in the tweet. 
(b) translating the tweet to French and retranslating itback to English.

### Data Preprocessing techniques
The Text data was pre-processed for the model by tokenizing, removing URL, @, #, punctuation and stopwords, the words were then lemmatized to make them more generic. The two inputs in the data (i.e. preprocessed text and target values) were concatenated to be sent to the data loader where the data was padded and made into batches. This was done for all 3 datasets.

## Evaluation Framework
The models was evaluated based on history curves (i.e. Loss and Accuracy curves) for the training and validation data to identify whether the model was overfitting, underfitting or had a good fit and based on the output conclusions the next model in the tuning process was selected. The loss function used was categorical cross entropy as the final output was classified into three classes AGAINST, FAVOR, NONE. Therefore the labels was one hot encoded before feeding into the network.
Since the Data was imbalanced additional metrics like AUC (area under ROC curve), precision, recall and F1 score was measured to judge the overall performance of the model with more emphasis on the F1 Score as imbalance in data may affect the loss and accuracy of the curve. was The macro F1 score was used to treat every class equally and the class weights were measured to handle the imbalance. Early stopping was added in the model based on validation loss to not waste any computational resources.

## Model selection
The Base model used was using a transfer learning on the model glove-twitter-100. The model was selected based on the research “Estimating Distributed Representation Performance in Disaster-Related Social Media Classification” Which also performed testing based on twitter data using various models such as glove, word2vec, ELMO and Bert their final evaluation on these model showed the overall performance of the models were quite similar and in some cases the word embedding model performed better than the transformer based model. So taking into account of the computational resource required and the time required to train the model and also the fact that glove-twitter-100 was specially trained on twitter it made perfect sense to choose it as the
base model for the stance classification.

## Parameter Tuning
models were tuned using class weights adding gap and dropout layers, adding learning rate scheduler, adding regularization and also fine tuning

## Result
The Final model selected which was the best tuned out of the other models. This model was performing best overall in terms of the fit and the model performance. Test data was then evaluated on this
model with a result of Loss: 0.9928 Accuracy: 0.5396 AUC: 0.7314 Precision: 0.5636 Recall: 0.4788 F1Score :0.5055
The model Performed the best in correctly classifying the AGAINST, then FAVOR Stance was classified right with majority and worst performance for the Stance NONE.


