---
title: R- Wordcloud from Tweets
---

Create a wordcloud from tweets.

Standard libraries

	library("twitteR")
	library('base64enc') #to correctly authenticate
	library("httpuv")
	setup_twitter_oauth("xxxxx","xxxxxxxx")

Additional libraries needed

	library(wordcloud)
	library(tm)
	library(RColorBrewer)

Search twitter

	mach_tweets = searchTwitter("#Hacktrafficking4good", n=1500, lang="en")

Extract text

	mach_text = sapply(mach_tweets, function(x) x$getText())

Fixes error

	mach_text <- iconv(mach_text,to="utf-8-mac")

Create corpus

	mach_corpus = Corpus(VectorSource(mach_text))

Create tdm

	tdm = TermDocumentMatrix(mach_corpus,control = list(removePunctuation = TRUE,stopwords = c("hack", "trafficking", stopwords("english")),removeNumbers = TRUE, tolower = TRUE))

Define tdm as matrix

	m = as.matrix(tdm)

Get word counts in decreasing order

	word_freqs = sort(rowSums(m), decreasing=TRUE) 

Create a data frame with words and their frequencies

	dm = data.frame(word=names(word_freqs), freq=word_freqs)

Keep 50 top words

	dm<-dm[1:50,]

Plot wordcloud

	wordcloud(dm$word, dm$freq, random.order=FALSE, colors=brewer.pal(8, "Dark2"))