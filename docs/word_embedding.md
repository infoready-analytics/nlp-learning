# Intro
This chapter aims to familarise you with the concept of Word Embedding and how it could be used to improve your NLP models. 

# What is Word Embedding
As fancy as it sounds, Word Embedding is just another way of converting words into vectors. 

Why the name "embedding"? Instead of the varying length CountVector/TF-IDF vectors, Word Embedding usually outputs vectors with fixed length. Therefore you could think of the embedding model operates in a fixed N-dimensional space, where N is the length of the output vector. 

The "embedding" process is usually a machine learning process to find the best place for a word in this N-dimensional space, aka "embed" a word into the space. 

Comparing to the meaningless numbers assigned in CountVector, Word Embedding process tries to place (or embed) the words in a way that words with similar meaning are placed close to each other, and words with opposite meanings are placed in the opposite sides of the multi-dimensional embedding space. 

This particular feature of word embedding allows us to do things that were not possible with the basic NLP techniques we've tried in the previous chapter. 

# Training Word Embedding Model
Training Word Embedding basically means taking a large corpus of text and try placing all the words from the text into an embedding space. This involves running a neural network model through huge amount of text data. It's usually very expensive and time consuming. 

In practice we almost never train a word embedding model by ourselves. There's always pre-trained word embeddings out there, by Google, Facebook and other renowned research groups. They are usually trained with better hardware and more data than we could manage. 

# Play with Pre-trained Word Embedding Model
Open Jupyter notebook and run below code: 
```Python
import gensim.downloader
embed_model = gensim.downloader.load('glove-wiki-gigaword-50')
embed_model.most_similar('twitter')
```

You should get output like:
```Python
[('facebook', 0.933304488658905),
 ('myspace', 0.8801369667053223),
 ('youtube', 0.8430657982826233),
 ('blog', 0.8262056708335876),
 ('blogs', 0.8064823746681213),
 ('blogging', 0.7970671653747559),
 ('tumblr', 0.7901090383529663),
 ('email', 0.7782611846923828),
 ('tweets', 0.7604536414146423),
 ('e-mail', 0.7538726925849915)]
```

What above code does is using `gensim` to load up a pre-trained `Glove` word embedding model. Which was trained on 6 billions tokens (words) of Wikipedia text, with a vocabulary of 400 thousand words (you can see why it's impractical to train it on our own). The one we are downloading is the smallest version of the model, embedding those words into a 50 dimensional space. Which means this model takes a word and generates a vector of 50 numbers. 

`gensim` package provides a convenient wrapper for the model, which exposes .most_similar() method that returns the words with similar meanings. What it does behind the scene is doing cosine similary queries against the entire vocabulary. 

# From "Word" to "Sentence"
So far we know that Word Embedding models convert a word into a vector. But in practice we rarely work with individual words, instead we work with sentences and paragraphs. How do we represent a sentence with numbers? 

The answer is suprisingly simple, we just take the average of all the word vectors in the sentence. But as always, there are some caveats to this method. 

## Think about this
Look at these two sentences: 

`My cat caught a mouse`

`My mouse caught a cat`

What would happen if we generate sentence embeddings by averaging word embeddings? 

# Sentiment Classification with Word Embeddings
Now it's time to upgrade your sentiment model with Word Embeddings. 

## Task
Train a new sentiment model using the same data your've used in NLP Basics. This time converting each review into vectors using a word embedding model before feeding them into a classification model. 

Record the outcomes and compare them to the TF-IDF based model. 

## Tips
- You shouldn't need much pre-processing (lemmatising, stop words etc.) because the vocabulary of word embedding model is usually huge, it would capture most variations of common words and the nuance in their different forms. 
- For simplicity just average the word embeddings in a sentence/paragraph. 

## Reflect
- Did the word embedding model perform better than the TF-IDF model?
- Check the predictions, what mistakes did the new model make, is there any patterns? 

# Conclusion
Word Embedding is a huge step up from TF-IDF in a few ways: 

- It captures the meanings of words instead of assigning meaningless index. 
- It enables unsupervised transfer learning. By running the embeding model through huge volume of text, it automatically learns the "meaning" of each word. The knowledge is then saved as pre-trained model for downstream use. All is done without any labelled data. 
- It compresses the feature space. TFIDF or CountVector generates a matrix of X by N where X is the number of examples and N is the number of unique words in the corpus. With a large corpus, N can be prohibitively big. This severely limits the application of the model. Whereas Word Embedding always place words into a fixed length feature space. 
- It eliminates the need for comprehensive pre-processing. Before word embedding, NLP model's performance depends a lot of the pre-processing techinques. Partly because the feature space was so big, it was necessary to simplify and discard less important information, by removing some words or lemmatising some others. But some information was lost in the process regardless. With the huge vocabulary and fixed feature space of word embeddings, such trade-off is usually unnecessary. 

However it should be clear by now, that the main drawback is that it's not order or context aware. In the following chapters we will see how more advanced NLP models handle context. 
