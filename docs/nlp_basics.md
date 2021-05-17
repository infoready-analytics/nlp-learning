# Intro
In this section, you will build a sentiment classification model with the more traditional NLP techniques. No deep learning involved. 

# Preparation
## Download Data
Download the sentiment dataset [News Group Movie Review Sentiment Classification (cornell)](https://raw.githubusercontent.com/jbrownlee/Datasets/master/review_polarity.tar.gz). This is a collection of movie reviews from the website imdb.com and their positive or negative sentiment. 

This dataset contains 2000 movies reviews, classified as positive or negative, 1000 each. 

## Pick a tool
It is recommended to use Jupyter Lab. Because some of the steps and output may be more obvious and interactive in a notebook environment. 

Put your notebook into `notebook/` folder. 

Otherwise if you chose to do it in .py files, put your code into `src/` folder. 

## Data Pre-processing
First thing you should do is to convert the .txt files in the downloaded dataset into a proper format. 

It is recommended to create a pandas dataframe with simply two columns: ['text', 'sentiment'], and save it as a .csv files to use for the rest of the course. 

# Count Vectorising
The majority of the effort in most NLP problems would be spent on converting words into numbers, so that they could be processed by machines. This is usually called **Vectorising**, since a sentence is usually converted into several numbers, therefore represented by a "vector". 

**Count Vectorising** is one of the simpliest ways to convert words into numbers. It assigns each word in a dictionary with a number, then simply do a lookup and replace. 

You can find many resources online if you want to learn more, for example this one: https://medium.com/swlh/understanding-count-vectorizer-5dd71530c1b

# First NLP Task: Count Vectorisation
Here's your first NLP task: 

## Task
**Vectorise the sentiment dataset using Count Vectorising**

## Tips
- CountVectorizer from sklearn is an easy choice. 
- You should save the result into the `data/` folder for future reference. 

# Classification on Count Vectors
Now that you have the vectorised representation of the sentiment dataset, here's the next step: 

## Task
**Train a sentiment model using the Count Vectors, and record the results**

## Tips
- Pick a simple classification model: Logistic Regression, Tree based models etc. whichever you are comfortable with. 
- Do train/test split, evaluate your model on the test set, save evaluation scores for future reference. 

# Improve on Count Vectorisation
There are a few obvious drawbacks for Count Vectorising: 
- Since each word gets assigned a number, when the vocabulary is large, the training data matrix could have a huge number of columns. This could be a problem even for modern hardware. 
- Variations of the same word got different numeric representations, for example: 'is', 'are', 'was', 'am' all convert to different numbers. 
- "Meaningless" words got the same weights as more meaningful words. For example: 'to', 'am', 'be', 'with' etc. 

## Task
Improve your classification model based on Count Vectorisation using below techniques: 
- Lemmatise the text
- Remove the "stop words"
- Use TF-IDF vectorising instead of Count Vectorising
- Retrain your classification model and compare the results with Count Vectorisor based model

## Tips
- `gensim` package provides a few easy tools for stop words removal and lemmatising. 
- Many packages provides TFIDF vectorisor, try `sklearn` or `gensim`

## Reflect
- Did the classification performance improve? 
- How did each technique improve/hurt the model performance? 
- Examine the outcome of the classification task. **Where did the model do well, and where did it mis-classify, could you find any patterns?**
- Any other pre-processing techniques you could try to improve the model? 

# Conclusion
By now you should have some basic ideas on how NLP used to be done. There has been a huge leap from what we've seen so far to what we actually do nowadays. Knowing the limitations will help you understand the motivations behind most of the development in NLP over the past few years. 

Furthermore, not everything can be solved by throwing data at a deep learning model. There are times when it's more efficient and appropriate to fallback to the basics. 