# Code example for word2vec analysis of Reddit data

This repo serves as an instruction for how to carry out an analysis of word embeddings based on the example of Reddit data. In the chapter "Collective Representations" in my book *Data Theory* (Lindgren, 2020), I write:

>**Mapping the language of Reddit**
>
>The data for the case study in this chapter was retrieved from [pushshift.io](https://pushshift.io), which is an open big data project that stores copies of all Reddit posts and comments. The analysis to follow is based on all data for 2018, which corresponds to more than 1.2 billion comments. A word2vec model was created, based on all of these comments using [the gensim package](https://github.com/RaRe-Technologies/gensim) for the Python programming language. The workflow and code used to create the model is available at [github.com/simonlindgren/datatheory-reddit-w2v](https://github.com/simonlindgren/datatheory-reddit-w2v). With the model created, it can be queried in a variety of ways, by posing questions, the responses to which help reveal the site’s linguistic structure (pp. 104-105).

The above mentioned code and workflow is made available in this repo through an annotated Jupyter Notebook (`datatheory-w2v.ipynb`).

----
Lindgren, S. (2020) [*Data Theory: Interpretive Sociology and Computational Methods*](https://politybooks.com/bookdetail/?isbn=9781509539277&subject_id=3&tag_id=42). Cambridge: Polity.

