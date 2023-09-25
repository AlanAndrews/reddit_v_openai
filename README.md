# Project 3
** Classifying human-generated vs AI-generated text **

## Executive summary

For this project I used the Python Reddit API Wrapper - Praw to collect 5250 question and answer pairs from various subreddits. 
The subreddits I collected QA pairs from were: AskReddit, AskScience, AskHistorians, Ask_politics, AskCulinary.
I also used AskUK, AskStatistics, AskScitech as subreddits to make test calls to the API.
I created a loop to collect attributes from the 999 top comments in each subreddit. 
The attributes for each post that I collected were the post title, main text of the subreddit post, when it was created ('created_utc'), and the top response as well as how many upvotes the top response received. 

---

After collecting the Reddit Q/A pairs I used the OpenAI API to feed te questions to the DAVINCI model. 
I utilized the python backoff module and submitted the reddit questions in batches of 20 to stay below the rate limit set by the API. 

---

After collecting all my data I Removed all posts that had been [deleted] or [removed]. And Removed '\n' and '\\_' from all the posts.
I then labeled answers as either AI generated (1) or not (0).

---

I used pipelines and gridsearches to find optimal hyperparameter values for the various models I fit to the training data. Overall I fit 10 modells: Multinomial Naive Bayes, Logistic Regression, Bernoulli Naive Bayes, and Linear Support Vector Classification with Countvectorizer preprocessing and Multinomial Naive Bayes, Logistic Regression, Gaussian Naive Bayes, K-nearest neighbors,  and Random Forest with TFID Vectorizer.

---

The 'best' performing models were the logistic regression model and LSVC with TFID vectorizer preprocessing. 

**LOGR TFID**
>Accuracy: 0.8898,
Precision: 0.8773,
Recall: 0.9060,
Specificity: 0.8736,
F1 Score: 0.8914

**LSVC TFID**
>Accuracy: 0.8694
Precision: 0.8779
Recall: 0.8578
Specificity: 0.8810
F1 Score: 0.8810


---

I also created heatmaps and confusion matrices to compare model performance. 



