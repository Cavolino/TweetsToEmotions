# Project 2. Kaggle Text to Emotion Dataset 2 

**Abstract:** *In this project, we analyzed a collection of 40K Twitter records classified in 13 different categories. Our investigation
spans different methodologies to enhance the understanding of the emotions in text data. We conducted an initial exploration of the dataset. Then we categorized the different tweets using different approaches: Empath, LDA, and BerTopic. Given as input the set of tweets belonging to the same category, the common goal of these three approaches was to identify keywords and check their compatibility with the emotion corresponding to the input category. We then investigated in more detail the tweets of each emotion. In particular, we evaluate the redundancy and the diversity between tweets of the same category. We also studied the agreement of each record with the antonyms of the emotion associated with it. Finally, we implemented several algorithms to increase the classification rate of the different categories.*


[**Dataset info:**](https://www.kaggle.com/datasets/pashupatigupta/emotion-detection-from-text/data?select=tweet_emotions.csv) 40K records Twitter dataset, classified into 13 categories: *neutral, worry, happiness, sadness, love, surprise, fun sentiment, relief, hate, empty, enthusiasm, boredom, anger*.

## Requests

### 1. Initial exploration: 
You may inspire from some existing programs in Kaggle handling the same dataset, write a script that outputs the histogram of the different categories. Comment on the distribution of the training samples across various categories.
### 2. Dataframse:
Write a script that concatenates all tweets of the same category and put them on a single file (data frame). Then use Empath categorization https://github.com/Ejhfast/empath-client, to output the key categorizes of each dataframe. Suggest a way to evaluate the matching between the categorizes generated by empath-category software and the labelling of the category in Twitter dataset (for each dataframe). Comment on the matching between the empath-category result and category title of each dataframe. 
### 3. LDA Topic Modelling:
Instead of using the Empath categorization, we want to use topic modelling to handle the category-record matching. For this purpose, write a script that uses LDA topic modelling with one topic and 3 words per topic. For each dataframe, we would like to investigate this matching by studying the mapping between the three keywords generated by the LDA and title category. We want to study this mapping at two levels: string matching and semantic analysis. Write a script that tests for each dataframe
- whether one of the generated keyword is the same as the tile category;  
-  whether on or more of these keywords are hyponym or hypernym of the title category. Present the result in a table that summarizes the result for all dataframes.   
### 4. BerTopic:
Instead of using LDA, we use another state-of-the-art topic modelling technique based on transformer: BerTopic, see https://github.com/MaartenGr/BERTopic. Study the example provided in github and suggest how you will proceed to imitate the reasoning of 3) or 2) to test whether the BERTopic generated topics match with the category title of each dataframe. Use the illustration provided in BERTopic to draw the result of this topic modelling. Summarize the result in a table.  
### 5. FuzzyWuzzy Redundancy and Diversity Evaluation:
We want to evaluate the extent of redundancy and diversity present in each dataframe. For this purpose, we start by looking into string matching. Use the fuzzywuzzy string matching package to calculate the ratio score of every pair (without repetition) of records belonging to the same category (data frame). Report the minimum, maximum and average ratio score (percentage indicating the amount of overlapping in terms of edit distance) for each data frame. A high minimum ration score indicates a high redundancy of elements of the class, while a small value may indicate high diversity.
### 6. FuzzyWuzzy Diversity Evaluation Pro:
To further elucidate the extent of diversity using FuzzyWuzzy metric, consider a subdivision of the ratio score between the minimum value and the maximum value into 10 equally separated threshold values, and write a script that identifies the number of records whose FuzzyWuzzy ration scores is beyond the corresponding threshold. Suggest a graphical illustration of your choice to illustrate this result. Repeat this process for each data frame. Comment on the extend of diversity & redundancy present in each dataframe.   
### 7. Proximity Evaluation with Antonym Relation:
We want to evaluate the proximity between the different categories using the antonym relation. For this purpose, for each category Ci, identify using lexical database of your choice (wordnet), the list of antonyms, say, Si1, Si2, …, Sin, and Sj1, Sj2, …,Sjm for categories Ci and Cj. Next, use the following construction: To evaluate the similarity between categories Ci and Cj, calculate the Wu and Palmer semantic similarity between category Ci (Cj) and each of antonym words Si1, Si2,…, Sin (Sj1, Sj2,…,Sjm) as follows:

$$
\begin{equation}
\begin{gathered}
Sim(C_i, C_j) = 1 - \frac{1}{2} \biggl[ \max\bigl(Sim_{wp}(C_i, S_{i1}), \ldots, Sim_{wp}(C_i, S_{in})\bigr) + \max\bigl(Sim_{wp}(C_j, S_{j1}), \ldots, Sim_{wp}(C_j, S_{jn})\bigr) \biggr]
\end{gathered}
\end{equation}
$$

Compare the results of the above construction and the simple Wu and Palmer similarity between Ci and Cj. Especially, discuss the discrepancy between the two models when looking for most similar category to each given category. Present the result in a table with a comparison with Wu & Palmer similarity.
### 8. Category Agreement with Antonyms, BERT Embeddings:
We want test the extent to which the records of each category agree with the antonym keywords. For this purpose, for each category Ci, whose antonyms are Si1, Si2, ..,Sin,  write a script that uses (base) BERT-embedding vector of each record R and the embedding vector of antonyms as follows: 

$$
\begin{equation}
\begin{aligned}
Sim(C_i, R) = 1-\max_{j=1,n}(Cos(BERT(R), BERT(S_{ij})))
\end{aligned}
\end{equation}
$$

where the cosine similarity between the two embedding vectors is the normalized measure. Identify the minimum, maximum and average  over all records R of category Ci. Present the result in a table and comment on the agreement between the category labelling and antonym-based reasoning. You may inspire from existing implementation in Kaggle that implements BERT model for classification purpose on the same dataset, provided in the initial link of this project description.
### 9. Classification Rate:
We want to devise a classifier that enhances the classification rate of the various categories. For this purpose, starting by a simple Random Forest classifier using 500 TF-IDF size as feature vector. You may inspire from the implementation of RoBERTa where a nice implementation of Logistic regression is detailed. Use the 80-20 % split of training -testing and 10 fold cross validation to output the confusion matrix.  Repeat the process when using XGBoost classifier, which in theory has some edge in handling imbalanced class dataset. Draw ROC graph to illustrate the performance of the classifier. 
### 10. RMSE Classification Score:
Select various choices for size of feature vector and choose alternative feature vectors (to IF-IDF) of your choice, and report the overall RMSE classification score for each class. 
### 11. Classification Rate with Deletion:
We want to find out whether a change in category design can influence the results. For this purpose, delete the categories that possess a relatively small number of samples from the classification scheme. Then, repeat 9) and determine the new classification rate for each category. 
### 12. Classification Rate with Merging:
Repeat 11 by merging the categories of small sample into a single meta-category, and repeat 11) accordingly. 
### 13. 
Identify potential improvement of your choice and identify appropriate literature to comment on the findings.

<br>
<hr>
<br><br>

<div style="text-align: right; font-size: 18px">

*Nov 2023*<br>
**Davide Moricoli, Andrea Cantore**
</div>
