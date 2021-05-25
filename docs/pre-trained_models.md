# Intro
When talking about NLP models, there's usually a distinction between "pre-train" and "fine-tune". In this chapter, we will instead use "pre-trained models" to refer to all types of models that are either pre-trained or fine-tuned and are ready to use. 

# Huggingface
We've had a few opportunities using Huggingface so far, they offer a wide range of pre-trained models. 

## Task
Go to https://huggingface.co/models, find a download a pre-trained sentiment model. 

Then perform sentiment prediction on the movies review dataset we've been using, without any training or tuning. 

Compare the result to the transformer model we fine tuned by ourselves in the previous chapter. 

## Tips
Be mindful of the model framework, download Pytorch instead of Tensorflow. 

# Cloud Serivces
The major cloud providers like AWS, GCP, Azure all provide their own NLP APIs. If you are already working in their ecosystem, and the task didn't require pinpoint accuracy, it's a good idea to use their APIs as baseline. 

## Task
Use AWS Comprehend to generate sentiment for the movies review dataset. 

Compare the result to the locally trained and pre-trained Hugginface models. 

## Tips
AWS Comprehend sentiment API should be free up to a certain number of inferences. 

# Conclusion
For common NLP tasks, pre-trained models and cloud APIs could be good enough. It's usually worthwhile to try one of them as baseline whenever possible. 