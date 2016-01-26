---
title: R- Wordcloud
---

Takes a vector and creates a fun wordcloud visualization based on most frequently used words in vector.

	library(wordcloud)
	library(tm)
	library(RColorBrewer)

	#convert vector to utf 8
	mach_text <- iconv(vector,to="utf-8-mac")
	mach_corpus = Corpus(VectorSource(mach_text))
	tdm = TermDocumentMatrix(mach_corpus,control = list(removePunctuation = TRUE,stopwords = c("", "", stopwords("english")),removeNumbers = TRUE, tolower = TRUE))
	# define tdm as matrix
	m = as.matrix(tdm)
	# get word counts in decreasing order
	word_freqs = sort(rowSums(m), decreasing=TRUE) 
	# create a data frame with words and their frequencies
	dm = data.frame(word=names(word_freqs), freq=word_freqs)
	# keep 50 top words
	dm<-dm[1:50,]
	# plot wordcloud
	wordcloud(dm$word, dm$freq, random.order=FALSE, colors=brewer.pal(8, "Dark2"))