# Word Vector Text Modulator #
Based on [a contribution](https://github.com/mbwolff/Word-Vector-Text-Modulator) to [2016 NaNoGenMo](https://github.com/NaNoGenMo/2016).

This repository contains the code and data necessary to modulate any text with word vectors derived from over 1,300 nineteenth-century French texts.

The following command will produce an interesting variation on the description of Charles Bovary's hat in the first chapter of _Madame Bovary_:

```
./modulateText.py maladroit adroit FlaubertBovary01.txt
```

### Prerequisites ###

* Python 2.7
* [treetagger](http://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/)
* Python modules:
  * [aspell](https://pypi.python.org/pypi/aspell-python-py2)
  * [pattern.fr](http://www.clips.ua.ac.be/pattern)
  * [gensim](https://radimrehurek.com/gensim/)
  * [treetaggerwrapper](https://pypi.python.org/pypi/treetaggerwrapper)

### A quick explanation of what's under the hood ###

[Vector space models of vocabularies offer promising techniques for exploring the semantic relationships between words](http://bookworm.benschmidt.org/posts/2015-10-25-Word-Embeddings.html). Using [gensim](https://radimrehurek.com/gensim/models/word2vec.html) to build such a model, the code presented here takes a pair of words (e.g. "homme" and "femme") and a given text as parameters to generate a new text based on computationally derived analogies. Each word in the original text is replaced by a word that is "most similar" to it according to the word pair. For instance, if "roi" is a word in the original text, it would be replaced like this:

```
>>> model.most_similar(positive=['femme', 'roi'], negative=['homme'], topn=1)
[(u'reine', 0.8085041046142578)]
```
The vector space model is able to complete the analogy: _"**reine**" is to "femme" as "roi" is to "homme"_. Handling verb conjugations and adjective agreements computationally in French is tricky but the code produces a mostly readable text needing occasional grammatical polishing (a good exercise for students). The code can modulate any text against any pair of words. The quality of the result depends on the corpus for the vector space model and the word pair chosen by the user.
