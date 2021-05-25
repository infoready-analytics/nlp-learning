# Latent Dirichlet Allocation (LDA)
When it comes to Topic Modelling, LDA is probably the most popular choice. 

The output of LDA looks like this: 

<img src=https://miro.medium.com/max/1400/1*yCd5BcHDDWMFF7emZu1VcA.png></img>

As you can see it discovers common topics out of a corpus of text. Each topic is defined by a list of words, each word has a weight. 

The basic assumption of LDA is that each **Document** in the corpus is a composition of **Topics**, then each **Topic** is a composition of **Words**. The algorithm tries to allocate words into topic and topics into document in the most **coherent** way. 

For more details on LDA, here's a good read: 
https://towardsdatascience.com/topic-modeling-and-latent-dirichlet-allocation-in-python-9bf156893c24#:~:text=Topic%20modeling%20is%20a%20type,document%20to%20a%20particular%20topic.

## Caveats
There are quite a few limitations about LDA: 

First of all you might have noticed the words in LDA output were lemmatised or stemmed. Unlike the more sophisticated NLP models we've used before, LDA doesn't understand word meanings or context. It treats words as simple tokens. 

The stemmed/lemmatised words are not a result of LDA itself, but for LDA to work decently we will have to pre-process (tokenise) the documents in this way, so that LDA has fewer tokens and variations to deal with. 

Also because LDA doesn't have inherent understanding of word meannings or context, the topics found don't usually make sense. We should be careful while presenting the output of LDA to business users. Multiple iterations of pre-processing, topic selection and topic interpretation may be required to achieve an acceptable outcome. 

Since LDA assumes each document is a collection of  topics, each document is almost always assigned with multiple topics. In cases where you want to simply group documents into categories, LDA's multi-topics output can make this difficult. Clustering is probably the better choice. 

LDA analyses the co-occurrence of words over a collection of documents. Therefore it works poorly when the documents are short or the number of documents were small. Since there would not be enough examples for it to work with. 

The final and probably most limiting feature of LDA is probably that you have to specify the exact number of topics beforehand. This is tricky because we resort to LDA when we knew little about the data. Number of topics is just one of the hyperparameter you could tune to achieve better outcome, and there are metrics like coherence score to help you determine the optimal hyper parameters. But again, good coherence score doesn't guarantee good outcome from a human understanding point of view. 

## Task
Apply LDA topic modelling to the movie review dataset. Try interpreting the output. 

## Tips
If the output doesn't make sense, try following: 
- Stemming/Lemmatising
- Removing stop words
- Changing number of topics
- Changing hyperparameters (alpha, beta, eta, number of passes etc.)

# Conclusion
We've touched upon LDA Topic Modellinig in this chapter, to summarise its pros and cons: 

Pros: 
- Easy to apply and produces decent topics with some tuning
- Generates word importance within the topics
- Generates topics composition for each document

Cons:
- Requires text pre-processing, sometimes extensively to achieve good result
- Requires hyperparameters tuning
- Output could be hard to interpret or summarise
- Output may not make sense despite your best efforts
- Performs poorly with short documents or small corpus

In the next chapter we will look into clustering, which could be a more suitable solution in certain scenarios. 
