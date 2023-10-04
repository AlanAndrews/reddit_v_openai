# Project 3
** Classifying human-generated vs AI-generated text **

## Problem statement
**This work was carried out to fulfill requirements for the General Assembly Data Science Immersive Bootcamp project 3. Each individual in the class was tasked with 1) collecting approximately 5000 question-answer pairs from Reddit using the Python Reddit API Wrapper, 2) feeding the questions  collected from Reddit to ChatGPT using the OpenAI API and collecting the responses, 3) using the data we collected to train a Natural Language Processing machine learning classifier model capable of predicting whether a response came from a human or AI, and 4) providing insights and conclusions based on the work carried out.**

**This type of work might be asked of a data scientist to determine what proportion of users on a website are bots or human users.**

## Executive summary

Using the Python Reddit API Wrapper - PRAW - I collected 5250 question and answer pairs from various subreddits. 
The subreddits I collected QA pairs from were: AskReddit, AskScience, AskHistorians, Ask_politics, AskCulinary.
I also used AskUK, AskStatistics, AskScitech as subreddits to make test calls to the API.
I created a loop to collect attributes from the 999 top comments in each subreddit. 
The attributes for each post that I collected were the post title, main text of the subreddit post, when it was created ('created_utc'), and the top response, as well as how many upvotes the top response received. 

---

After collecting the Reddit Q/A pairs I used the OpenAI API to feed te questions to the DAVINCI model. 
I utilized the python backoff module and submitted the reddit questions in batches of 20 to stay below the rate limit set by the API. 

---

After collecting all my data I Removed all posts that had been [deleted] or [removed]. And Removed '\n' and '\\_' from all the posts.
I then labeled answers as either AI generated (1) or not (0).

---

I used pipelines and gridsearches to find optimal hyperparameter values for the various models I fit to the training data. Overall I fit 10 modells: Multinomial Naive Bayes, Logistic Regression, Bernoulli Naive Bayes, and Linear Support Vector Classification with Countvectorizer preprocessing and Multinomial Naive Bayes, Logistic Regression, Gaussian Naive Bayes, K-nearest neighbors,  and Random Forest with TFID Vectorizer.

---

**One half of the responses in the dataset were human-generated and the other half were generated by AI, therefore the accuracy baseline against which to compare any models created is 0.5. i.e. if a response was randomly selected from the dataset there is a 50% chance that it was generated by human and 50% it was generated by chatgpt. Models should at least be expected to perform better than a random selection.
 
The 'best' performing models were the logistic regression model and LSVC with TFID vectorizer preprocessing (see below). **They generally performed well at predicting whether a response was generated by a human (Accuracy: 0.8898 and 0.8951 on test data, respectivley) and compared to other models implemented in this work, were not too overfit (Accuracy scores of 0.9277 and 0.9405 on training data). 

**I relied on accuracy (the ratio of correct predictions to the total number of predictions made) as the primary method of determining model performance because 1) it is very often used as a default method for this purpose and is easy to interpret, 2) dataset is perfectly balanced (50/50 human to ai), meaning there is no concern of a model predicting a majority class more often than a minority class, 3) misclassifications in this case will not have too harmful of an effect (compared to say, a medical-related classification problem).

**LOGR TFID**
>Accuracy: 0.8898,
Precision: 0.8773,
Recall: 0.9060,
Specificity: 0.8736,
F1 Score: 0.8914

**LSVC TFID**
>Accuracy: 0.8951
Precision: 0.8779
Recall: 0.8578
Specificity: 0.8810
F1 Score: 0.8810


---

I also created heatmaps and confusion matrices to compare model performance. 
![Alt text](./figures/hm_perf_test.png)
---
![Alt text](./figures/hm_perf_train.png)


## Recommendations and Conclusions
**R


