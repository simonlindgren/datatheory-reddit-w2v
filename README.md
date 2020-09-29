# Code example for word2vec analysis of Reddit data

This repo serves as an instruction for how to carry out an analysis of word embeddings based on the example of Reddit data. In the chapter "Collective Representations" in my book *Data Theory* (Lindgren, 2020), I write:

>**Mapping the language of Reddit**
>
>The data for the case study in this chapter was retrieved from [pushshift.io](https://pushshift.io), which is an open big data project that stores copies of all Reddit posts and comments. The analysis to follow is based on all data for 2018, which corresponds to more than 1.2 billion comments. A word2vec model was created, based on all of these comments using [the gensim package](https://github.com/RaRe-Technologies/gensim) for the Python programming language. The workflow and code used to create the model is available at [github.com/simonlindgren/datatheory-reddit-w2v](https://github.com/simonlindgren/datatheory-reddit-w2v). With the model created, it can be queried in a variety of ways, by posing questions, the responses to which help reveal the site’s linguistic structure (pp. 104-105).

## Workflow and code

With the data gathered from pushshift.io, the field `body` was extracted from the downloaded json data, and split by sentence, into one big file with one sentence per line. Punctuation and leading/trailing whitespace was removed. The resulting sentences were saved in `sentences/reddit-sentences-2018`.

The model was trained using gensim with the code in the cell below (based on [this tutorial](https://rare-technologies.com/word2vec-tutorial/)).

```
# Import libraries and set up logging
import os
import gensim, logging
logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)

# Prepare a memory-friendly iterator that won't try to keep the entire sentence list in RAM 
class MySentences(object):
    def __init__(self, dirname):
        self.dirname = dirname
 
    def __iter__(self):
        for fname in os.listdir(self.dirname):
            for line in open(os.path.join(self.dirname, fname)):
                yield line.split()
 
 
# Point it to a directory containing one or several files with one sentence per line 
sentences = MySentences('sentences')

# Train the w2v model
model = gensim.models.Word2Vec(sentences, min_count=40) # exclude words occurring less than 40 times

# If you don't plan to train the model any further, calling 
# init_sims will make the model much more memory-efficient.
model.init_sims(replace=True)

# Save the model to disk
model.save('reddit-w2v.model')
```

## Querying the model

### Two examples of queries

![image](https://github.com/simonlindgren/datatheory-reddit-w2v/blob/master/images/most_simiilar.png)

![image](https://github.com/simonlindgren/datatheory-reddit-w2v/blob/master/images/doesnt_match.png)

### Two examples of visualisations

Using [Gephi](https://github.com/gephi/gephi). Recursive queries for `most_similar` using similarity scores as edge weights.

![image](https://github.com/simonlindgren/datatheory-reddit-w2v/blob/master/images/word_network.png)

Using TensorFlow [Embedding Projector](https://projector.tensorflow.org/).


![image](https://github.com/simonlindgren/datatheory-reddit-w2v/blob/master/images/word_embedding.png)

----
Lindgren, S. (2020) [*Data Theory: Interpretive Sociology and Computational Methods*](https://politybooks.com/bookdetail/?isbn=9781509539277&subject_id=3&tag_id=42). Cambridge: Polity.

