# Word Vector Text Modulator
Based on [a contribution](https://github.com/mbwolff/Word-Vector-Text-Modulator) to [2016 NaNoGenMo](https://github.com/NaNoGenMo/2016).

This repository contains the code and data necessary to modulate any text with word vectors derived from over 1,300 nineteenth-century French texts.

The following command will produce an interesting variation on Baudelaire's prose poem _Enivrez-vous_:

```
./modulateText.py noir blanc BaudelaireEnivrezVous.txt
```

### A quick explanation of what's under the hood

[Ben Schmidt has written an excellent introduction to word embedding models](http://bookworm.benschmidt.org/posts/2015-10-25-Word-Embeddings.html). Using [gensim](https://radimrehurek.com/gensim/models/word2vec.html) to build such a model, the code presented here takes a pair of words (e.g. "homme" and "femme") and a text as parameters to generate a modulated text. Each word in the original text is replaced by a word that is "most similar" to it according to the word pair. For instance, if "roi" is a word in the original text, it would be replaced thusly:

```
>>> model.most_similar(positive=['femme', 'roi'], negative=['homme'], topn=1)
[(u'reine', 0.8085041046142578)]
```
Handling verb conjugations and adjective agreements computationally in French is tricky but the code produces a mostly readable text needing grammatical polishing (a good exercise for students). The code can modulate any text against any pair of words. The quality of the result depends on the corpus for the vector model and the word pair chosen by the user.
