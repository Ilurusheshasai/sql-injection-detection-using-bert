# sql-injection-detection-using-bert
This repository provides a sample code to train a BERT model to properly classify if a given string is SQL injection or not.

This project was developed as part of the coursework of IS-734.

SQL injection remains a major database integrity concern in cybersecurity. Our approach uses Google's neural network model BERT (Bidirectional Encoder Representations from Transformers) to solve this. BERT was trained on a massive corpus of unpublished books and English Wikipedia and fine-tuned with 34,445 data points, including SQL injection sentences and generic statements. These methods used BERT's superior language understanding to discriminate between malicious and ordinary SQL queries.

Our vector preprocessing strategy helped BERT process and learn from textual material. With 110 million parameters and 12 cascaded encoders, the model detected subtle SQL injection patterns and contexts. Continuous dataset refinement focused on SQL injection patterns improved the model's performance despite initial obstacles.

The project produced a powerful SQL injection detection solution that strengthened database security. Its success shows that powerful AI can be used in cybersecurity. It emphasizes the importance of high-quality, diversified datasets in AI model training. We want to grow our dataset and study more advanced models like BERT-Large to adapt to cyber threats. This project protects against specific cyber assaults and enables AI-based cybersecurity.

## Data Collection and Preparation
# Data Sources: 
The primary dataset includes 34,445 data points, with 11,455 SQL injection sentences and 22,990 non-SQL generic sentences, sourced from Kaggle.
# Data Enhancement: 
To improve model accuracy, the dataset is expanded and diversified with a variety of SQL injection patterns and regular sentences.
# Tokenization: 
Break down sentences into individual words or tokens.
# Vectorization: 
Convert tokens into numerical vectors that can be processed by the neural network. This step is crucial as BERT understands numerical input.

## Model Selection: BERT Uncased (2018)
Stage 1: In the initial stages we didn't start with the BERT model we started with a basic idea that mainly focuses on the identification of patterns in the given input. So we wanted to start with logistic regression and random forest models to classify the input as SQL injection or not.
Observation 1: We have achieved absolutely good performance metrics for precession, recall, and Accuracy we have achieved 99.0 % in all these metrics on both models.
We have suspected this behavior of the models and tried to test the trained models. To do this we have created a custom dataset which we used to test the models. It is here we have realized that the models are producing flawed results.
Results at the end of this stage:

			Results at the end of stage 1

As you can see from the above results “Drop TABLE users” should be an SQL injection and %2A%28%7C%28mail%3D%2A%29%29 should also be an SQL injection (we knew it is an SQL injection because it is labeled as SQL injection in the data we used for training). 
This might look good but when we are dealing with security we can't let our models even have a single flaw. 
So tried to understand the reason behind this anomalous behavior.
Initially, while vectorization we have created long vectors of all possible words available in our dataset. So we strongly believe that it is caused by the ‘Curse of Dimensionality’. 

Stage 2: 
To improvise this result we tried to create bi-grams words and used them to fit each sentence against the label.
We have used a random forest model for this classification task.
The results we obtained looked like this:

		Results at the end of Stage 2
We still suspected the results and checked the top bigrams that are mostly responsible for SQL injection. We couldn't find the most basic and commonly known patterns are not even found in the top 150 bigrams that are responsible for SQL injections using their importance scores.
So we didn't proceed with further work on these models.


