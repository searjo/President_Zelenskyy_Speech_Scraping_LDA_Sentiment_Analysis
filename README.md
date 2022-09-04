# President_Zelenskyy_Speech_Scraping_LDA_Sentiment_Analysis
As a part of a project, I scraped all of President Zelenskyy's speeches in 2021-2022 and conducted LDA and Sentiment Analysis. We used this to model financial performance. 

The text and sentiment, along with the LDA analysis, is below. Note - in the output, the LDA dashboard is not available in the PDF output.

The objective of this  is to analyze the use of text-based features that capture news
sentiment and topics discussed in the news for forecasting financial performance. 
To meet this objective headlines and article descriptions from the BBC were used to compute
sentiment scores using NRCLex and VADER, whilst an LDA was used to determine the topic
shares of each article. Together with the lags of the dependent financial series these text-based
features were used in a LASSO regression to compute a rolling forecast.

The text data consists of 4787 BBC headlines and descriptions, along with the date and time they
were published and a link to their URL. Each description contains on average 110 characters.
To extract usable features for our data set we vectorized the text through tools available on used
Natural Language Processing (NLP). For vectorization analysis the text was pre-processed using three
main methods: lowercase, stemming, and lemmatization. First, all symbols, figures, and stop-words
were removed from the text. The first pre-processing method simply takes the lowercase of all words in
the text. The second removes the suffixes that are created from different conjugations of a word. This
allows us to have a unique root for a word despite many potential conjugations and alterations. Hence,
this allows counts of the word within a corpus to be more reflective of the true use of the word in all
of its variations. Lemmatization adopts the idea of converting many conjugations and alterations to a
root word as in stemming, but with stemming the removal of part of a word can make it unidentifiable
for human readers. Lemmatization fixes this issue by converting the different formats of a word to one
specified format of a root word. For example, the word homes would be converted to home.
Two popular methods to inspect term frequency are the count vectorizer and the TF-IDF (Term
Frequency Inverse Document Frequency) vectorizer available in Sci-kit Learn [5]. These allow us to
inspect unigrams, bigrams, and trigrams of the text to better understand the most popular or relevant
words and combinations of them. The count vectorizer method considers the absolute count of a
term in a document, whilst the latter considers term frequency as being inversely related to document
frequency.
The  bgrams and trigrams highlight that the BBC articles were mainly related to sports
and the conflict in Ukraine. The latter bears significant relevance given the patterns observed in the
financial series.


The TF-IDF gives us insight into the number of times a term appears in each document relative to
the number of documents it appears in (words that appear in more documents are weighted lower).
Hence, TF-IDF adjusts for a bias within the general CountVectorizer particularly for long documents.
Although the TF-IDF vectorizer is often more practical than the more straightforward count vectorizer, given that the collected documents did not have a large discrepancy in document size it was not as useful for our analysis - for example, the top 25 bigrams are the same as in Figure 9. That said,
you can see in 11 that some new trigrams not included in figure 10 are present: this includes ¡World
Snooker Championships¿ and ¡Nazanin Zaghari-Ratcliffe¿, a British author who returned home after
being detained in Iran for five years.


While positive and negative NRC vlues are fairly balanced, you can see that anger scores and negative scores piked significantly during the invasion of Ukraine by Russia (note these scores are higher given the lack of data – you can see when more data is aggregated
that the scores even out). When the data is not aggregated the sentiment scores are extremely dense
- however, for doing analysis on a particular article, this specificity might be useful.


The rolling window analysis indicates a fluctuation between positive and negative sentiments, but
they both remain around the same level. This is useful to know as you would expect a journalistic
institution to remain fairly neutral on topics - and therefore limit emotion one way or the other. Trust
is the next most common emotion which is in line with what is ideally conveyed by a reputable news
outlet. We can also see anticipation (news is often forward-looking) and surprise and joy. Disgust is
least common, which may indicate the BBC does not express negative sentiment with words the NRC
has labeled as disgust (these are likely less professional). Of particular note is the spike in negative
sentiment and anger around the time Russia invaded Ukraine - although there is less data for the
period to weight down these scores, it is still interesting to see an outlet such as the BBC used words
that expressed anger during this time.
For VADER, the analysis indicates that neutrality is by far the most common emotion - this is likely
the desired result for a journalistic publication that aims to report the facts without bias. The compound score tends to fluctuate between extremely positive and negative. The Vader results are slightly more difficult to interpret given the fluctuations - this may indicate it
had a difficult time gauging sentiment without the help of ’social media’ cues such as emojis, all-caps,
and excessive punctuation.


4.2.3 LDA
The second set of text features reflects the topic allocation of our BBC articles using Latent Dirichlet
allocation (LDA). Given the diverse range of topics, a global publication will report on domestic news,
global conflict, sports, culture, politics etc. We implemented an LDA to try and identify these topics
through Machine Learning. These topics are then used to calculate the topic shares per article in the
data set. LDA topic modeling methods are popular in text mining and social media analysis to identify
patterns and hidden semantic structures within the text, as exemplified by [16].
This method we use is based on the paper by [3]. The use of the algorithm is to generate a
probabilistic model using a three-level hierarchical Bayesian model for text corpora, where collections
of text are modeled as a finite mixture over a set of underlying topics. This allows us to obtain a topic
model for the text defined by the topic probabilities.
These topic probabilities are obtained using two Dirichlet distributions for hyperparameters α and
β which are defined by the latent class driving the words in the text. These are then used as the
conditions for the joint distribution for a bag of words (wd) and the topic indicator for each word (zd).
The multinomial mixture model is defined as:
p(wd|β, π) = X
k=1:K
p(wd|zd = ek, βk)p(zd = ek|π) (2)
For our application, the gensim library [15] was used. This uses variational Bayes, where the Gibbs
sampler uses the prior in an algorithm for the likelihood that a word in a document is attributed to
a topic in each step. Where this function is driven by the Dirichlet distributions of α and β. The
LDA was thus considered a reasonable statistical model to real the latent semantic structure of the
considered texts.
For the LDA the text for pre-processed using three main methods: lowercase, stemming, and
lemmatization. The three pre-processing methods were contrasted and various LDA results compared.
Although no clear cut winner was observed, we can see the LDA did a moderately successful job in
topic modelling when given 8 topics. We chose the lemmatizer given the output was not very different
and it allows the words to be more readable.


LDA Results
While there is some topic overload (Ukraine/Russia war in particular dominate two topics), some topics are quite neatly defined, including the Queen’s
Jubilee, the UK rail workers strike, the Roe v. Wade abortion ruling by the US Supreme Court, and
another on the Premier League. Given the large number of topics covered by the BBC, it’s certainly
interesting to see these topics defined. That said, we ran this LDA over a dozen times using different
parameters and did not always get clean results. Some other outputs included models more focused
on the news around Wimbledon tennis, asylum seekers being sent to Rwanda, and on the F1 Grand Prix.
