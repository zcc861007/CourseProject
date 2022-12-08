# CourseProject - MetaMining: Mining of Literature Data for Meta-analysis

**Chaochao Zhou (single member / project leader)**

cz76@illinois.edu

## Introduction

### Motivation
A single study may include a small sample, which may lack statistical power in statistical analyses. Meta-analysis is attractive, as it is a statistical analysis that combines the results of multiple scientific studies. However, meta-analysis requires researchers to extract/collect a large amount data by reviewing numerous publications, which is tedious and time-consuming. Therefore, it is desirable to develop a pipeline for automatic extraction of quantitative data from text

### Objective

For a numeral (N) in text, I aim to extract its relevant entities, including the metric (M) and unit (U), for example

<img width="798" alt="image" src="https://user-images.githubusercontent.com/33674922/206323838-e12320bc-2f0e-41eb-9c8a-bd868d7f3672.png">

### Challenges

- Multiple numbers may co-exist in a single sentence, so it requires to find the corresponding pairs of numbers and metric. 
- The lengths of words to describe entities (metrics and units) vary.
- A numeral may be associated with multiple metrics hierarchically. In this case, only the closest relation (e.g., in a clause) was considered.

### Contribution
The project was proposed and implemented by Chaochao Zhou alone. Main works include:
- Collected texts and performed text pre-processing
- Created a dataset including text annotation of entities and relations
- Developed a recurrent neural network (RNN) and tested its performance 

## Methods

### Text Collection

From the PubMed database, I collected 2451 abstracts of publications in the recent year (from Nov 2021 to Nov 2022) using a single keyword of “thrombectomy”. I randomly chose 100 abstracts, and segmented each abstract into sentences. Then, I filtered sentences that include numerals, resulting in 521 sentences. Further, each sentence was segmented into a list of words (unigram word-based learning)

### Text Annotation

I used the “brat” annotation tool to annotate relations of a numeral with the unit and metric (allowing missing relations). Some annotation examples:

<img width="792" alt="image" src="https://user-images.githubusercontent.com/33674922/206325114-1f353218-8a25-40d2-995d-dc7283aa0ad6.png">
<img width="792" alt="image" src="https://user-images.githubusercontent.com/33674922/206325129-e5bcc7e9-e298-4a0e-9d9f-da3b879ad609.png">
<img width="792" alt="image" src="https://user-images.githubusercontent.com/33674922/206325141-9a2702ab-1e21-4771-8397-fa521e69689c.png">

### Annotation to Label

The annotated relations were converted to lables (0 - None; 1 - Unit; 2 - Metrics). As each instance only considers one numeral, other numerals have been masked as “[num]”. For example:

<img width="825" alt="image" src="https://user-images.githubusercontent.com/33674922/206325534-c98526ce-5323-4d69-a847-422591d490f7.png">

### Training and Testing Sets

In total, 521 annotated sentences were expanded to 1758 examples (i.e., text-label pairs) with one marked numeral (other numerals were masked). Using a ratio of 9:1, the total 1758 examples were randomly split into a training set with 1582 examples and a testing set with 176 examples

### RNN and Training

A many-to-many RNN including embedding and GRUs was implemented, with the learning curves during training shown below. After training, the training accuracy is 0.9829 and the validation accracy is 0.9785.

<img width="700" alt="image" src="https://user-images.githubusercontent.com/33674922/206424841-6e44b479-f764-44bb-bc1a-8ce6a3ae829b.png">

## Implementation and Test

### Repo of Codes and Files

Please see all codes and files in the "/Demo" folder in this repo:  
- A Colab notebook for demo: test.ipynb
- Trained RNN model: current_model.h5
- A testing dataset (/Demo/current_data) including:
  - Dictionary for index-word conversion: index_word.pkl
  - Text (token sequence): x_test.pkl
  - Entity label: y_text.pkl
  - Numeral label: nl_text.pkl

### Testing

Some randomly sampled predictions from the test set (that was not used for training) are demonstrated below:

<img width="600" alt="image" src="https://user-images.githubusercontent.com/33674922/206327212-d5287fee-9caa-4678-aacd-b3544935f8bc.png">
<img width="592" alt="image" src="https://user-images.githubusercontent.com/33674922/206327378-4ab5d7f2-078d-47a0-8fbe-999a094c889c.png">
<img width="592" alt="image" src="https://user-images.githubusercontent.com/33674922/206327395-ae5ecea8-a088-451d-87c1-2f5a7b752fc1.png">

## Summary and Improvement

The preliminary results showed that units and metrics associated with numerals can be extracted by RNN with decent prediction accuracy. The pipeline is viable to automatically extract structural data from publication texts, and the data of the same measure can be further filtered in combination with text retrieval. 

Of course, there are several aspects that need to be improved.

- The ground-truths were built by myself, so there could be inconsistency due to ambiguity in the writing of original text, complex relations, or my knowledge limitations about measures in thrombectomy. 
- The small dataset was created from the literature about “thrombectomy”, so it is necessary to expand the dataset and consider other domains. 
- I currently implemented a RNN to tackle the relation extraction of numerals and entities, while pretrained models such as BERT which encoding information from a large text corpus should be attempted.


