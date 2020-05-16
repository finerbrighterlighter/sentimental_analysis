# sentimental_analysis

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

## Sentence Level Polarity

Sentence Intensity Analyzer library is applied.





<a name="myfootnote1">1</a>: Siriraj Hospital is mispelled as Sriraj Hospital in my variables mostly, because I did not realised there is an extra "i" between "S" and "r".
Somehow I was confused with the Sanskrit work "Sri".
