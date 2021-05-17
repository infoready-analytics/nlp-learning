# Intro
This section aims to familarise you with the concept of Word Embedding and how it could be used to improve your NLP models. 

# What is Word Embedding
As fancy as it sounds, Word Embedding is just another way of converting words into vectors. 

Why the name "embedding"? Instead of the varying length CountVector/TF-IDF vectors, Word Embedding usually outputs vectors with fixed length. Therefore you could think of the embedding model operates in a fixed N-dimensional space, where N is the length of the output vector. 

The "embedding" process is usually a machine learning process to find the best place for a word in this N-dimensional space, aka "embed" a word into the space. 

Comparing to the meaningless numbers assigned in CountVector, Word Embedding process tries to place (or embed) the words in a way that words with similar meaning are placed close to each other, and words with opposite meanings are placed in the opposite sides of the multi-dimensional embedding space. 

This particular feature of word embedding allows us to do things that were not possible with the basic NLP techniques we've tried in the previous section. 

# Play with Pre-trained Word Embedding Model


# Sentiment Classification with Word Embeddings


# More on Word Embeddings


# Conclusion
