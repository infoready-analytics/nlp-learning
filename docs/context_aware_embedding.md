# Intro
In the previous chapter we looked at word embeddings and the main drawback if we use it alone: it's not context aware. In this chapter we will look at ways to improve that. 

# Motivation
Sentences with the exact same words but different orders:

`My cat caught a mouse`

`My mouse caught a cat`


Same or similar words that have different meanings in different contexts:

`I got a parking fine`

`It is a fine day in the park`

In the previous chapter, we tried generating sentence embedding by simply averaging the word embeddings. In which case, it was impossible to differentiate the  meanings in above scenarios. 

It's not enough to learn embeddings for individual words, an embedding model should learn to generate different embeddings when the same words are used in different context. 

# Solution
If we use a sentiment model as an example: the model needs to look at the example `I got a parking fine` and learn that it's negative, then look at `It is a fine day in the park` and learn that it's positive. Despite both examples have the word `fine`. 

Let's imagine the inputs and outputs of such model. 

Output is easy, for a classification model, it could simply be a number between 0.0 and 1.0. Negative if < 0.5, positive if >= 0.5

Input is a bit tricky. Let's say we use pre-trained word embedding with an embedding size of 50. Meaning each word is represented by a vector of 50 numbers. 

So `I got a parking fine` becomes a 5 by 50 matrix. `It is a fine day in the park` becomes a 8 by 50 matrix. 

## Varying Length Input
The first obvious challenge is that the input size is not fixed. It varies depending on the length of the input sentence. 

Two straightforward approches to this: 
- Use a Convolutional Neural Network (CNN). CNNs usually take a bigger input and "compress" it to a smaller size. The main limitation with CNN is that it requires fixed input size. We could usually pad the sequence if it's shorter or truncate if it's longer. 
- Use a Recurrent Neural Network (RNN). RNNs takes a sequence of any length and generated fixed size output. We don't have to worry about the input length but RNNs are slower to train due to its sequential natural. 

"Attention" mechanism and the "Transfomer" family of models based on it, were a later development comparing to the CNN/RNN of earlier days. They learn context much more efficiently but like CNN they deal with fixed length input, therefore requires padding/truncating. 

Implementing Deep Learning models is much more complex than what we've tried so far, for now we will not attempt building a deep NLP model from scratch. In practice that's also rarely necessary. 

But if you are interested there are plenty of examples on the internet. Here's an example of using LSTM (a type of RNN) and word embeddings for text classification: 
https://towardsdatascience.com/multiclass-text-classification-using-lstm-in-pytorch-eac56baed8df

## Transformers
The majority of the state of the art NLP models in the past few years came from the "Transformer" family mentioned above. To understand how they work, you may need basic understanding of sequential neural network and attention mechanism. 

There's a good source on Cousera for the basics. It's free if you only read the materials: 
https://www.coursera.org/learn/nlp-sequence-models?specialization=deep-learning

Google's [BERT](https://en.wikipedia.org/wiki/BERT_(language_model)#:~:text=Bidirectional%20Encoder%20Representations%20from%20Transformers,and%20his%20colleagues%20from%20Google.) was the most famous one that brought this age of transformers to NLP. There are numerous resources online about BERT, feel free to read about it. 

# Generate Sentence Embedding Using Pre-trained Models

## Task
Read the documentation of "Sentence Transformers" package here: 
https://github.com/UKPLab/sentence-transformers

Install the package and download one of the pre-trained models. 

Use Sentence Transfomers to generate embeddings for the sentiment classifcation task in the previous chapters, then train the same classification model on top of the new embeddings. 

Compare the results to the average word embedding model. 

## Tips
- This is a bit less hand holding comparing to the previous tasks. Reach out to the team if you are stuck. 

## Reflect
Compare the mistakes made by the average word embedding model, did the sentence transformer embedding model make the same mistakes? 

# Conclusion
We've gone from the basics all the way to transformer models. In the next chapter will dig into the usage of transformer models, because that's what we actually do for a lot of NLP tasks nowadays. 