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
The above bigrams and trigrams highlight that the BBC articles were mainly related to sports
and the conflict in Ukraine. The latter bears significant relevance given the patterns observed in the
financial series.


The TF-IDF gives us insight into the number of times a term appears in each document relative to
the number of documents it appears in (words that appear in more documents are weighted lower).
Hence, TF-IDF adjusts for a bias within the general CountVectorizer particularly for long documents.
Although the TF-IDF vectorizer is often more practical than the more straightforward count vectorizer, given that the collected documents did not have a large discrepancy in document size it was not as useful for our analysis - for example, the top 25 bigrams are the same as in Figure 9. That said,
you can see in 11 that some new trigrams not included in figure 10 are present: this includes ¡World
Snooker Championships¿ and ¡Nazanin Zaghari-Ratcliffe¿, a British author who returned home after
being detained in Iran for five years.
