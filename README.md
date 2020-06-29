# Determining Changes in Sentiment and Subjectivity in Historic US Government Documents
***Griffin Talan***

## Introduction
It is common to hear vaguely defined phrases such as "political tension", "divisive rhetoric", "identity politics", and many others when speaking about United States government affairs. What do we mean when confidently speak in terms like this? We all have a sense that things are changing quickly and causing turmoil in our society, but we don't have metrics to understand the underpinning causal factors associated with them. In this project, I aim to analyze US historic documents using natural language processing to see if there are measurable changes in three different dimensions; political ideology, sentimental tone, and speaker subjectivity.

## Data Collection

**Model Training Data**

| Dataset  | Analysis Dimension  |
|---|---|
|[Ideological Books Corpus](https://people.cs.umass.edu/~miyyer/ibc/index.html)   |Political Ideology - Conservative, Neutral, and Liberal   |
|[Rotten Tomatoes Subjectivity-Labeled Reviews](http://www.cs.cornell.edu/people/pabo/movie-review-data/)   |Subjectivity   |
|[UCI Combined Sentiment-Labeled Reviews (Amazon, IMDB, and Yelp)](https://archive.ics.uci.edu/ml/datasets/Sentiment+Labelled+Sentences)   |Sentiment   |


**Analyzed Historic Government Documents**

| Dataset  |
|---|
|[State of the Union Speeches - Webscraped](https://www.presidency.ucsb.edu/documents/presidential-documents-archive-guidebook/annual-messages-congress-the-state-the-union#Table%20of%20SOTU)   |
|[Inaugural Speeches](https://www.kaggle.com/adhok93/presidentialaddress)   |
|[Supreme Court Decisions](http://scdb.wustl.edu/data.php)   |
|[Department of Justice Press Releases](https://www.kaggle.com/jbencina/department-of-justice-20092018-press-releases)   |





## Exploratory Data Analysis and Preprocessing

All Data were formatted into two columns - text and analysis dimension.

***Text Preprocessing***
For text processing, documents were converted into lowercase, stripped of all non-alpha characters, and tokenized by word. After evaluating training models, I decided to leave in stop words and not stem the data to retain syntactical nuances in sentence structure.

***Analysis Dimension Preprocessing***
Political Ideology: Conservative = -1, Neutral = 0, Liberal = 1
Sentiment: Negative = 0, Positive = 1
Subjectivity: Objective = 0, Subjective = 1


## Model Training and Evaluatuion

In order to account for the differing document lengths and nuanced syntactical information associated with sentiment and subjectivity analysis, Bidirectional Long-Short Term Memory (LSTM) Recurrent Neural Networks (RNN) were used in this analysis. This model type allowed for correlations between words that were near and far from, and before and after a given word in each document.

***Political Ideology***

Though the data was human labeled, I was unable to optimize a model that reproducibly scored higher than a baseline of predicting a single outcome. This analysis dimension was removed from the experiment.

***Sentiment***

The model trained on the sentiment dataset produced training and validation accuracies of ~85% 

Accuracy             |  Log Loss
:-------------------------:|:-------------------------:
![](../data/images/sent_acc.png)  |  ![](../data/images/sent_loss.png)


***Subjectivity***

The model trained on the subjectivity dataset produced training and validation accuracies of ~85%

Accuracy             |  Log Loss
:-------------------------:|:-------------------------:
![](../data/images/subj_acc.png)  |  ![](../data/images/subj_loss.png)


## Results

Inaugural speeches were ommitted from the results graphs as they showed no trend and were highly variable in their scoring. Considering that there were trends in State of the Union Speeches - this may be attributed to the subject matter discussed in each respective document. State of the Union Speeches may be more aimed at events that occurred in a year, whereas the Inaugural Speeches may be more of a "victory lap" - though I have no objective evidence to support this. 

***Sentiment Analysis***

When analyzing the changes in positivity (sentiment dimension) over time, no discernable trend becomes visible. There seems to be a decline in positivity with regards to State of the Union Speeches, but the high variability in that metric would lead to it not being a very strong discussion point. Interestingly, the Supreme Court decisions show a relatively stable, slightly-negative sentiment.

![](../data/images/sent_ovr.png)



***Subjectivity Analysis***

When analyzing changes in subjectivity over time, a more stable, positive trend is seen in both the State of the Union Speeches and Supreme Court decisions. In fact, a large spike in subjectivity is observed in speeches that occurred after the world wars. This will be discussed further below when analyzing the composition of majority/minority decisions in the Supreme Court. Though the supreme court did see an increase in subjective tone, no single document scored above 0.4 on the objective-subjective scale - exemplifying the objective nature of legal decision making as compared to the subjective tones taken by politicians. 

![](../data/images/subj_ovr.png)


As mentioned above, the subjective tone in US government documents saw a discernible increase in the post-war era, demonstrating the increasing polarization that is the basis of the problem stated in the introduction. This is further exemplified when analyzing the change in majority/minority composition. Around 1950, the makeup of the Supreme Court transitioned from primarily one party to a more balanced makeup. It seems that the country required a coordinated response to opposition forces, and has since divided itself internally.

![](../data/images/court_other_data.png)



## Conclusions and Experimental Limitations

As demonstrated in the results section, natural language processing can be used in some sense to describe long-term trends in the state of societal affairs. Though there are limitations and concerns I have with this methodology (discussed below), the drastic changes that begin in the post-war era lend to the idea that some real change is being observed in subjective tone. It seems that when the country requires a concerted response to a problem, objective tone takes precedence, whereas in times of peace a subjective tone does. 

The major concerns I have with this experiment are threefold. First, the language used in society changes over time, and these changes can not easily be assessed or accounted for with such large works. One example is the word "fantastic". In the 19th century, this word would be associated with something that is imaginative or non-concrete whereas in modern time, it refers to the subjective sentimental state associated with something. Second (and closely related to the first), a neural network model associated with text can not easily be time normalized. The training data used to create these models are all based on (modern) human labeled data collected in the last 10 years and has its limitations when compared to older text. It would be near impossible to find a dataset that spans that time with accurate labels to define a specific analytical dimension. Third, the document lengths that were used in model training were much shorter than most of the texts used for predictions. To see if this is an influence, I would tokenize the documents by sentence rather than word and see if that would affect outcomes. 

Even with these limitations, the resultant predictions don't seem to be trivial. The relative subjective tones shown between court decisions and political speeches demonstrate this effectively. 