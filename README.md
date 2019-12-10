# Subreddit Classification: r/movies vs. r/television

----

## Table of Contents

 - [Problem Statement](#Problem-Statement)
 - [Executive Summary](#Executive-Summary)
 - [Conclusions and Recommendations](#Conclusions-and-Recommendations)

----
## Problem Statement
 
We have been tasked with webscraping Reddit in order to build a classification model that allows us to determine whether text has come from one of two subreddits.  In this case, we have chosen to classify between r/movies and r/television in a way such that Netflix can use our modeling.  Ultimately, our problem statement contains three elements.   First, can we build a model that classifies text from reddit posts and titles into the correct subreddit between r/television and r/movies? We will assess models based on testing set accuracy. Second, what are the key features that drive the distinction in content between the two subreddits?  We will do this by looking at logistic regression coefficients.  Third, how can our client, Netflix, take advantage of this information?

This project was completed with General Assembly in October 2019.

----
## Executive Summary

First off, given that we are taking blocks of text, we know that we will be using Vectorizers so we can input this information into our model.  Second, we know that we are going to be building Classification models as we are attempting to classify our posts into one of a select number of categories (in this case, r/movies or r/television).  

We begin by using scraping tools to collect data from Reddit's API.  We collected approximately 2,500 posts (split approximately evenly between the two subreddits).  After accounting for duplicate posts, we ended up with a data set that included 704 television posts and 436 movies posts.  

We then used Beautiful Soup and RegEx in order to clean HTML characters to prepare to enter it into our Vectorizers.  We also manually scrubbed some posts to find leftover HTML characters that were not removed by our other data cleaning tools. At this point, we were ready to begin modeling.

For the first stage of our moodeling, we wanted to look at our classification models on a pure accuracy basis.  At this stage, we felt it was best to use gridsearching to look at Logistic Regression, Naive Bayes, and Decision Trees with both the Count and TFIDF Vectorizers and three fold cross validation. We then fit our models using the best parameters determined during grid searching. We did not make any changes to the stop words (i.e. did not add difficulty to our model) at this point.

Next, we wanted to answer part two of the problem statement and build a Logistic Regression model while incorporating additional "obvious" stop words (such as the titles of the subreddits) in order to determine some sort of feature importance.  At this stage, we were able to begin to identify trends in the text based on looking at the Logistic Regression beta coefficients.

Finally, we summarized our findings and were able to make some recommendations to the Company.  These are outlined in the Conclusions and Recommendations section of code book and this ReadMe.

----
## Conclusions and Recommendations

The problem statement for this project contains three elements.  First, can we build a model that classifies text from reddit posts and titles into the correct subreddit between r/television and r/movies?  Second, what are the key features that drive the distinction in content between the two subreddits?  Third, how can our client, Netflix, take advantage of this information?

The first stage of my modeling process was to build the most successful classifer possible based on accuracy scores on our testing data as a means of answering part one of the problem statement.  For modeling, we looked at Logistic Regression, Naive Bayes, and Decision Trees models with both Count and TFIDF Vectorizers and different combinations of hyperparameters.  We used Grid Searching techniques to automate these processes.  Our results were quite interesting.  Although a Decision Tree model with the Count Vectorizers produced the best training score at 99.9% accuracy, this model only had 80.7% accuracy on the testing set (unsuprising given Decision Trees' propensity to overfitting).  Therefore, our best pure classification model was determined to be Multinomial Naive Bayes with the Count Vectorizer, which produced 94.1% accuracy on the training set and 86.0% on the testing set.  

As for phases two and three of the problem statement, we knew that we wanted to build a Logistic Regression given the interpretability of the coefficients in the model.  Additionally, we wanted to view a model that eliminated words that made for easy identifiers (such as the names of the subreddits).  This Logistic Regression model returned a testing accuracy score of 82.8%.  Importantly for our purposes, we are able to view the coefficients and look at their importance to the model - specifically by our ability to say that certain words appearing in a post made the post a certain amount more likely to be classified into r/television (our positive class).  Please see the section titled "Feature Importance Table" for a detailed breakdown of this analysis.

Finally, we can begin to answer the question as to how Netflix can take advantage of this information.  We can see what types of things drive interest in movies and television.  This model can potentially be used for targeted marketing to various consumers, development planning for determining what kinds of projects interest people, and, it so follows, budgeting.  Moreover, we can take this model further in the coming time by potentially conducting time series analysis to discuss how discourse has changed over time and look at various trends.  All in all, this model provides information in ways that can make relationships between our data science team and the marketing, finance, and creative teams quite productive for the Company.