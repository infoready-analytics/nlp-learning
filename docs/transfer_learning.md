# What is Transfer Learning
According to [Wikipedia](https://en.wikipedia.org/wiki/Transfer_learning), Transfer Learning "focuses on storing knowledge gained while solving one problem and applying it to a different but related problem".

Let's look at the example of using BERT for sentiment classification: 
1. During **Pre-training**: it stores general knowledge about a language by going through huge volume of texts. 
2. During **Fine Tuning**: it stores sentiment knowledge by learning from a relatively small sentiment dataset. 
3. During **Interence**: it applies the knowledge learned in the previous two steps to predict sentiment of input text. 

Now we look at exactly what tasks were performed at each step in the context of transfer learning: 

## Pre-training
You can read about it here: https://github.com/google-research/bert#what-is-bert

BERT perform two tasks during pre-training: 
1. Masked word prediction
2. Next sentence prediction

These tasks were performed on huge volume of texts: Wikipedia (2.5B words) + BookCorpus (800M words) and are fairly expensive (four days on 4 to 16 Cloud TPUs). 

They are not directly related to the sentiment classification. They store generic knowledge about English language in the model, which is a major part of BERT's prediction power. 

What's more, these pre-training tasks are **unsupervised**. Making it feasible to learn from the huge amount of text data. (Imagine the cost to obtain the same amount of labelled data for **supervised** learning)

In practice, we probably never need to pre-train our own NLP model. It's almost always easier to start with a baseline that's pre-trained already. 

## Fine Tuning
To train a generic sentiment model, we "fine tune" the pre-trained BERT model with a labelled sentiment dataset. 

For example the [SST (Stanford Sentiment Treebank)](https://paperswithcode.com/dataset/sst). It consists of 11,855 labelled sentences. This is a very small dataset comparing to pre-training. 

By fine tuning on this classification task, BERT is able to learn sentiment classification on top of its generic language knowledge learned during pre-training. 

## Prediction
When we use this pre-trained, fine tuned BERT model for sentiment classification, there's no guarantee that the input text is in the same domain as the fine tuning dataset (in this case SST was from movie reviews). But since the model learned about language and sentiment in general, it still might perform well enough on sentiment in a different domain. This is arguably another example of transfer learning. 

# Fine Tuning vs Embedding
In the previous chapter we used a transformer model to generate embedding, then used a generic ML model to classify the embeddings. How's that different from "fine-tuning" a NLP model? 

A simplified answer would be: fine tuning not only trains the classification part of the model, but also subtly shifts the weights in the embedding parts of the model. The fine tuned embeddings should be more suitable for the task you tuned for. So generally spearking, if all other things were equal, a fine tuned model performs better than a fixed embedding model plus classification. 

# Fine Tuning a Transformer Model
Huggingface is an open source community that hosts many pre-trained NLP models. We will now use their model and API to fine tune a transformer model for our sentiment classification task from the previous chapters. 

## Task
Refer to Huggingface [documentation](https://huggingface.co/transformers/custom_datasets.html#fine-tuning-with-custom-datasets) on how to fine tune a pre-trained transformer model. 

Split the 2000 movie reviews we've been using in previous chapters into train and test sets. 

Fine tune a pre-trained transformer model using the train set then evaluate it on the test set. 

Save the results and compare to the models from previous chapters. 

## Tips
- Use Pytorch instead of Tensorflow. It is the preferred framework here at Arq. 
- It is recommended to follow the fine tuning code in [this section](https://huggingface.co/transformers/custom_datasets.html#fine-tuning-with-native-pytorch-tensorflow). Writing your own training loop makes it easier to understand what's going on behind the scenes. 
- Working with Huggingface API or transformer models is not always straightforward. Feel free to Google for other resources/tutorials, or reach out to the team if you are stuck. 

## Reflect
Did this transformer model perform better or worse than the model from previous chapters? What could be the reasons? 

What could you do to make it better? 

If you were to use this model in a production environment, what limitations should be considered? 

# Conclusion
When it comes to customised NLP model, fine tuning a pre-trained model is a commonly used approach. However there are cases when we can simply rely on pre-trained, pre-tuned ready to use models. We will explore those options in the next chapter. 