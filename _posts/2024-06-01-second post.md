---
title: NER for Telugu language
date: 2023-06-01 20:14 +0300
author: Hanvitha_Shreya_Roopa_Moulika
---

## Problem Statement

Develop a Named Entity Recognition (NER) model for the Telugu language aimed at accurately identifying and classifying entities such as names of persons, organizations, locations, dates, and other relevant entities within Telugu text data. The model should be capable of analyzing Telugu text from various domains and genres, including news articles, literature, and more.

## Motivation

1. Telugu, a widely spoken Indian language, poses significant challenges for building Named Entity Recognition (NER) models due to its highly inflectional and agglutinating nature.
2. Annotated corpora, gazetteer lists, and capitalization cues, commonly used in NER for other languages, are not readily available for Telugu
3. The complexity of Telugu's linguistic rules results in varied word forms, spelling variations, and free word order, making it difficult to identify named entities.
Eg: Telugu word Rana is a name but can also be used a verb is different context.
    Nagarjuna Hospital is a place but can be interpreted as a name in some cases.
4. NER has numerous applications in NLP and is used while performing text mining, machine translation, question answering, indexing for information retrieval, automatic summarization, etc.

## Approach

### [Dataset Link](https://github.com/Hanvitha-51/NER_Telugu/tree/main/Dataset)

### Data Collection

   1. GLiNER
   2. Form of Information  Retreval Evaluation(FIRE)
   3. fastText word vectors

| NAMED ENTITY TAG  | MEANING | EXAMPLE|
|------|------|------|
| person | person name | nagarjuna నాగార్జున|
| Location | location name |Hyderabad హైదరాబాద్|
| organization | organization name |Google గూగుల్ |
| miscellanous | number, data, event, things ,year and, occupation | 1977 |

Dataset


|NAMED ENTITY TAG| 	MEANING|
|------|------|
| person|	1563|
|location|	1915|
|organization| 778|
|miscellaneous|	2004|


DATA SET|	NO OF TOKENS|	NO OF ENTITIES|
|------|------|------|
Train|	33597|	4382|
Test|	14399|	1878|
Total|	47996|	6260|

### Preprocessing
NEs belonging to four classes, namely, person (PERSON), location (LOC), organization (ORG) and other miscellaneous NEs (MISC) were manually identified and tagged using the standard IOB scheme.

### Modeling
1. Train an NER model (e.g., CRF, LSTM) using the labeled dataset
2. Generate character level  embeddings using Bi-LSTM 
3. FastText embeddings lookup 
4. Concatenate both embeddings
5. Generate contextual word embeddings using Bi-LSTM

### Evaluation
Compare our classifier with other language independent classifier which are publicly available, CRF++
Compare different metrics like precision, recall

## Implementation

### [Codes Link](https://github.com/Hanvitha-51/NER_Telugu)

Brief summary of classes and methods that we have implemented:

1. Utilis.py:
    1. Handle unknown tokens
    2. Yielding data in iterable format
    3. Padding sequences
    4. Generate mini batches

2. Model.py:
      1. Builds model architecture
      2. Reinitiating weights of layers
      3. Manages the training loop
      4. Tests the model on test set

3. Config.py:
      1. defines a configuration
      2. manages path
      3. centralizing crucial parameters

4. GenUtilities.py:
      1. ProgressTracker class: tracks loss and accuracy 
      2. averages metric value
      3. Summarizes training duration and average metrics.

1. add_word_embeddings()
      1. Initialization
      2. Word, Character Embeddings
      3. Concatination
      4. Dropout regularization

2. add_logits()
      1. Bi-LSTM 
      2. Dropout regularisation
      3. Projection layer
      4. Reshaping final logits

3.  functions add_train()
      1. Optimizer selection
      2. Gradient computation
      3. Gradient clipping
4. run_epoch()
      1. Batch Iterations
      2. Feed Dictionary creation
      3. Optimization and loss computation
5. Predict()
      1. word processing using batch prediction
      2. Tag prediction
6. Evaluate()
      1. Accuracy calculation on test set
      2. Compute other matrics like precision, recall etc

## Results
### CRF++
CRF, or Conditional Random Fields, is a statistical modeling method used for structured prediction. It is particularly effective for labeling and segmenting sequential data, which makes it suitable for tasks like NER 

Metric|	Score|
|------|------|
Precision|	78.25|
Recall|	72.66|
F-measure|	75.03|


CLASS|	F-measure|
|------|------|
Person|	74.52|
location|	76.56|
organization|	54.76|
miscellanou|	80.28|

### YamCha
Yamcha, on the other hand, is a tool based on Support Vector Machines (SVM) designed for text chunking and NER. It uses a sequence labeling approach and can handle large-scale data efficiently. Yamcha allows for the incorporation of various features and is known for its high speed and accuracy

Metric|	Score|
|------|------|
Precision|	78.71|
Recall|	74.92|
F-measure|	76.27|
 
CLASS|	F-measure|
|------|------|
Person|	76.08|
location|	79.89|
organization| 54.32|
miscellanou	80.15|

### GitHub Account

Metric |	Score|
|------|------|
Precision|	97.56|
Recall |	75.12|
F-measure|	81.14|
 
CLASS|	F-measure|
|------|------|
Person|	82.01|
location|	81.06| 
organization|	84.49|
miscellenous|	90.45|


### Our Model

Metric|	Score|
|------|------|
Precision|	85.35|
Recall|	73.55|
F-measure|78.85|


CLASS|	F-measure|
|------|------|
Person|	78.07|
location|	79.81|
organization|	89.89|
miscellanou|	90.02|

## Conclusion

We have developed a Named Entity Recognition model specifically for the Telugu language. The performance of this model has been evaluated using key metrics, with the results detailed below:

Precision: 85.35
Recall: 82.33
F-Measure: 82.09
These metrics indicate the effectiveness and reliability of our model in processing and understanding the Telugu language.





