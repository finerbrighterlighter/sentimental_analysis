# Sentimental Analysis

This project is the Assignment of RADS 611: Advanced Modeling Techniques - Natural Language Processing Class 
at Department of Clinical Epidemiology and Biostatistics, Faculty of Medicine Ramathibodhi Hospital.
Data is scrapped from [HonestDocs](http://www.honestdocs.co/). The instruction is to select three hospital, including Ramathibodhi Hospital and compare
the ratings amongst, also to perform Natural Language Processing tasks.

Five ipython notebooks are attached.
1. web_scraping_translation.ipynb
2. sentence_level_analysis.ipynb
3. word_ml_models.ipynb
4. LDA_topic_modelling.ipynb
5. visualization.ipynb

## Web Scraping and Translation

Honestdocs is a website where people can rate and share about their experiences at respective hospitals. 
It is a website aimed for Thai people and hospitals, naturally leading to the majority of comments are in Thai language.
Since our program being an International Program, and also me being Burmese, the assignment instructs us to use google translate api for python to translate the comments into English.

My choice of Hospitals are Ramathibodhi Hospital , Siriraj Hospital<sup>[1](#myfootnote1)</sup> and King Chulalongkorn Memorial Hospital.
The scraping process is done using Beautifulsoup library. The source code shared by Ajarn is largely unchanged.
After the processes for three hospitals are done, they are concatenated into a single dataframe and csv file due to personal preference.

Duplicated comments are searched by grouping with Hospital and Comments. The first one is kept and the rest are dropped.

Google Translate Api has daily limit of characters. Yandex Translate is applied becuase Api token is free.
The result dataframe is saved in **"candidate_hospitals_translated.csv"**.

### Sample Size

![](/viz/data_size.svg)

![](/viz/ratings.svg)

## Sentence Level Polarity

Rating 1 and 2 are considered **negative**. Rating 4 and 5 are considered **postive**. Rating 3 are dropped.
Spacy is used to remove the stopwords. 

Each comment has multiple sentences. Sent_tokenize from NLTk is used to separate them into multiple sentences.Each sentence is analyzed for a polarity using Sentence Intensity Analyzer library. Score is calculated in compound of three polarity. All the scores for each sentence is summed for the comment. If the comment's total score is more than 1, it is considered **Positive sentiment**.

Accuracy | F1 score for positive | F1 score for negative
-|-|-
0.80 | 0.88 | 0.43

## TFIDF and Machine Learning Models

Rating 1 and 2 are considered **negative**. Rating 4 and 5 are considered **postive**. Rating 3 are dropped.
Spacy is used to remove the stopwords. Punctuations are removed.

Multiple Machine Learning models are applied to TF-IDF vectors.

Model | Accuracy
-|-
Multimoial Naive Bayes | 0.80
Bernoulli Naive Bayes | 0.82
Logistic Regression | 0.81
Stochastic Gradient Descent | 0.83
Support Vector Classifier | 0.81
K Nearest Neighbour Classifier | 0.82
Multi-layer Perceptron | 0.83

All models perform similar but top three performing models, Multi-layer Perceptron, Stochastic Gradient Descent and K Nearest Neighbour Classifier are further tuned.

Model | Tuned Parameters
-|-
Multi-layer Perceptron | ```"clf__activation": ("tanh", "relu"),"clf__solver":("lbfgs","sgd", "adam"),"clf__learning_rate":("constant", "adaptive")}```
Stochastic Gradient Descent | ```"clf__alpha": [1e-3,1e-4,1e-5],"clf__penalty":['none','l2','l1']}```
K Nearest Neighbour | ```"clf__n_neighbors": [5,10,20],"clf__weights":["uniform","distance"],"clf__algorithm":["auto","ball_tree","kd_tree","brute"],#1 for manhattan, 2 for euclidean"clf__p": [1,2]}```
TF-IDF | ```"tfidf__ngram_range": [(1, 1), (1, 2), (1,3)],"tfidf__use_idf": [True, False],```

After tuning the Hyperparameters,

Model | F1 Score for Positive | F1 Score for Negative | Accuracy
-|-|-|-
Multi-layer Perceptron | 0.86 | 0.67 | 0.84
Stochastic Gradient Descent | 0.88 | 0.61 | 0.83
K Nearest Neighbours | 0.81 | 0.57 | 0.80
Sentiment Intensity Analyzer | 0.86 | 0.49 | 0.80

Probably because my dataset has significantly less samples for negative sentiment. <br>
The models perform worse for negative sentiments classification. <br>
In conclusion, **Multi-layer Perceptron** performs the best overall, out of the three candidates. <br>
On the other hand, all three models performs better or as accurate as the **Sentiment Intensity Analyzer**.

## LDA Topic modelling

The dataset is separated into six different dataframe, Positive and Negative for all hospitals.
Coherence score up to 10 topics are calculated for each dataframe.

## Wordcloud

Hospital | Positive | Negative
-|-|-
Rama|![](/viz/rama_pos_wc.svg)|![](/viz/rama_neg_wc.svg)
Siriraj|![](/viz/sriraj_pos_wc.svg)|![](/viz/sriraj_neg_wc.svg)
Chula|![](/viz/chula_pos_wc.svg)|![](/viz/chula_neg_wc.svg)

<a name="myfootnote1">1</a>: Siriraj Hospital is mispelled as Sriraj Hospital in my variables mostly, because I did not realised there is an extra "i" between "S" and "r".
Somehow I was confused with the Sanskrit work "Sri".
