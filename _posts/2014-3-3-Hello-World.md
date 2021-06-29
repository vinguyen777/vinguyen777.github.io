---
layout: post
title: Twitter Sentiment Analysis in Java
---

Sentiment analysis is an application of Natural Language Processing (a branch of Artificial Intelligence) that revolves around detecting the sentiment of text. A common dimension for measuring sentiment uses labels positive, negative and neutral; there are many other possibilities as well (i.e. how strong the sentiment is, how active vs subdued it is, etc). Figure 1 contains two sample tweets about the current series Falcon and the Winter Soldier, one positive and one negative. As companies aspire to obtain detailed insights into the way their products are being perceived, social
media is a particularly popular arena for deploying sentiment analysis. As a result, there are many organisations offering apps or services for building them; a screenshot from a demo of such an app is given in Figure 2.

![_config.yml]({{ site.baseurl }}/images/sentiment-analysis.jpg)

The earliest and simplest techniques for performing sentiment analysis (although this type of
approach is still in fact widely used) only conducted keyword matching in the text on the basis of words
from a sentiment lexicon (i.e. a source of words that have known sentiment). Often, these lexicons do not have extensive coverage: there are many words with sentiment that are not included in them, particularly in the case of social media text, where misspellings, abbreviations and slang
are common. Consequently, there are other approaches to the task: there’s a large class of machine learning
techniques applied, as well as other techniques like label propagation, where sentiment labels are propagated through a graph structure.

In this project, I have worked with a set of real tweets collected by researchers who developed
one of the first approaches to sentiment analysis of tweets, and constructed my own tweet sentiment
analyser . Early stages of the project only employ a keyword-based approach, building up to a simple
version of label propagation later.

![_config.yml]({{ site.baseurl }}/images/figure1&2.png)

There are four sorts of data required.
- Tweets: Early sentiment analysis work
included the collection of a set of tweets, some for training
a machine learning model for sentiment analysis, and some for evaluating how good that model was.
That same data was utilised in this project with the following information for each tweet:

      • the gold polarity of the tweet (0 = negative, 2 = neutral, 4 = positive, = not given)
      
      • the id of the tweet (2087)
      
      • the date of the tweet (Sat May 16 23:58:44 UTC 2009)
      
      • the query (lyx)
      
      • the user that tweeted (e.g. robotickilldozr)
      
      • the text of the tweet (e.g. Lyx is cool)
      
![_config.yml]({{ site.baseurl }}/images/fig3.png)

- Basic Sentiment Words: There is a widely used subjectivity and sentiment lexicon
that from which the data were extracted. Each line is comprised of a word, followed by the typical sentiment of that word
without any additional context, indicated by the string positive or negative, e.g.

![_config.yml]({{ site.baseurl }}/images/fig4.png)

- Finegrained Sentiment Words: The full lexicon from above also includes information about
the strength of the sentiment: weaksubj indicates weak sentiment, and strongsubj strong.

![_config.yml]({{ site.baseurl }}/images/fig5.png)

- Inverse Index: This requires constructing a graph, linking tweets
that share words. 

![_config.yml]({{ site.baseurl }}/images/fig6.png)

Two classes, Tweet and TweetCollection, were created. While the former represents an individual
tweet, the latter represents a collection of them. A simple keyword-based method was then implemented for sentiment analysis of tweets, computing the total of positive and negative words in a tweet to determine the predicted polarity of the tweet. 

![_config.yml]({{ site.baseurl }}/images/fig7.png)

In the approach to sentiment labelling, I ended up
with quite a few unlabelled tweets, because several of them did not contain words from the sentiment
lexicon. As noted earlier, another technique is to propagate sentiment labels from one
tweet to another (similar) one. Therefore, a graph that linked together
‘similar’ tweets (for some definition of similarity) was constructed, and then connected components
in the graph were identified with a view to propagating sentiment labels via the edges in the graph within those
connected components.

![_config.yml]({{ site.baseurl }}/images/fig8.png)

The ultimate goal after constructing the graph is to propagate sentiment labels via the edges in the graph defined, and the majority labels in those connected components. Additionally, a richer sentiment labelling scheme was employed thereafter.

![_config.yml]({{ site.baseurl }}/images/fig9.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
