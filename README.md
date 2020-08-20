# Executive Summary
In this NLP project I built a Logistic Regression model to classify the posts from the following 2 subreddits as either Android or iPhone:
- https://www.reddit.com/r/androidquestions
- https://www.reddit.com/r/iphonehelp

The data collected was immediately saved to a CSV file, before checking for duplicates, null and outliers. I did not find any duplicate and null values, but I found and removed a few contextual outliers because the posts were about kindle, which were considered out of topic.

These are the steps for data cleaning:
- Remove HTML tags
- Remove unnecessary words url strings in the message
- Remove words that are causing high correlations
- Remove non-printable unicode characters
- Remove accented words
- Remove special characters. Keep letters and numbers
- Remove single characters between words
- Remove extra whitespaces
- Convert to lower case, split into individual words
- Remove stopwords
- Lemmatization

I explored the data to determine if they can be used to solve classification problem and found the folloiwing conditions were met:
- The dependent variable is either Android or iPhone, so it is a classification problem
- No unbalance class issue (ratio is 0.506 for both training and test datasets)
- The independent variables are numbers (they will be once vectorized into word counts or tf-idf)
- No high correlations among the the independent variables (less than 0.9)
- Independent variables are independence from one another (highest correlation is less than 0.9)

Next I performed a simple comparison of 3 models - Logistic Regression, KNN and Naive Bayes Multinomial, and shortlisted  Logistic Regression and Naive Bayes Multinomial because the accuracy and F1-score for KNN were rather low.

In the preprocessing and modeling phase I built a DummyClassifier as my baseline model, followed by GridSearch and manual tuning to find the best combination of vectorizer and classifier. Logistic Regression with TfidfVectorizer was chosen as our production model, because it has very high accuracy, F1-score and AUC-ROC, as well as being only marginally overfit. 

# Conclusion and Recommendation
- I built the production model based on Logistic Regression as classifier and TfidfVectorizer as our vectorizer. It has very high scores for accuracy (91.1%), F1-Score (91.7%) and AUC-ROC (91%). The best part is, there is no overfit or underfit issue, which makes it an ideal model for classification.

- I can confidently use this model to classify unseen data. Having say that, we will need to maintain the good performance by regularly updating the data from the two subreddits (AndroidQuestions, iPhoneHelp). On top of that I will look at other related subreddits (e.g. AndroidHelp) and other forums to continue helping the model learn and surpass its current performance. 

- The next step will be to test the routing of requests on our own case logging system, to see if the model is able to classify the requests correctly.

- I will also be looking into Sentiment Analysis for the requests coming into our own systems. Based on the sentiments, we will know if there are any negative or positive feedback about our apps or services, and highlight them to the Quality Assurance Team to follow up. In addition to that we will use sentiment analysis to classify a request into various levels of urgency.

- The application of NLP can be extended to self-help for users. Based on the words entered by users we can match them to known problems and recommend solutions to the users to try to fix themselves, relieving our support teams of common or known issues.
