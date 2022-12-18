# MetaMining: Mining of Literature Data for Meta-analysis

**CS410 Course Project at UIUC**

**Chaochao Zhou (single member / project leader)**

**Email: cz76@illinois.edu**

## Presentation Recording

[![Watch the video](https://img.youtube.com/vi/65VKSAbeNhg/sddefault.jpg)](https://youtu.be/65VKSAbeNhg)

## Paper

This work has been documented in a paper, which will be online accessed soon:

**THE PAPER HAS BEEN SUBMITTED AND WILL BE RELEASED SOON**  
[Chaochao Zhou](https://scholar.google.com/citations?user=PYcUZ3YAAAAJ&hl=en&authuser=1&oi=ao), [Bo Yang](https://scholar.google.com/citations?user=OEyXN00AAAAJ&hl=en&authuser=1&oi=ao)  
Arxiv preprint 2022  
[[arxiv](https://arxiv.org/abs/)]

## Implementation

All codes and files are provided in the "/Demo" folder of this repo:  

### Codes
A Colab notebook "test.ipynb" is provided for demo. Please sequentially run the code cells in this notebook.

### Files
- Trained RNN model: current_model.h5
- A testing dataset (current_data) including:
  - Index-word dictionary: index_word.pkl
  - Text (token sequence): x_test.pkl
  - Entity label: y_text.pkl
  - Numeral label: nl_text.pkl

## Project Overview

### Objective

A single study may only include a small sample, which may lack statistical power in statistical analyses. Meta-analysis addresses this problem by combining the results of multiple scientific studies. However, meta-analysis requires researchers to extract/collect a large amount data by reviewing numerous publications, which is tedious and time-consuming. Therefore, it is desirable to develop a pipeline for automatic extraction of quantitative data from text

Given a text, the objective of this work is to extract the related entities of a numeral (N), including the metric (M) and unit (U), for example

<img width="650" alt="image" src="https://user-images.githubusercontent.com/33674922/206323838-e12320bc-2f0e-41eb-9c8a-bd868d7f3672.png">

### Challenges

- Multiple numerals may co-exist in a single sentence, so the relations corresponding to each numeral needs to be found. 
- The lengths of words to describe entities (metrics and units) vary in different sentences.
- A numeral may be associated with multiple metrics hierarchically.

### Contribution

Main works that were proposed and completed to solve the mining problem include:
- Collected texts and performed text pre-processing
- Created a dataset with text annotation of entities and relations
- Developed a recurrent neural network (RNN) and tested its performance 

### Test

Some randomly sampled predictions from the test set (that was not used for training) are demonstrated below:

<img width="600" alt="image" src="https://user-images.githubusercontent.com/33674922/206327212-d5287fee-9caa-4678-aacd-b3544935f8bc.png">
<img width="592" alt="image" src="https://user-images.githubusercontent.com/33674922/206327378-4ab5d7f2-078d-47a0-8fbe-999a094c889c.png">
<img width="592" alt="image" src="https://user-images.githubusercontent.com/33674922/206327395-ae5ecea8-a088-451d-87c1-2f5a7b752fc1.png">

### Summary

It is shown that the pipeline is viable to automatically extract structural data from general texts without special templates/patterns. Within the mined structured data, important measures can be further filtered and collected in combination with text retrieval implementations. It is anticipated to achieve better performance by expanding the dataset and investigating other machine learning models. We are working on the improvement of this pipeline, and will release a newer version in the near future. 
