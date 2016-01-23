---
title: R- TwitteR API Part 1
---

Add app to twitter account.
Set callback url to http://127.0.0.1:1410
Grab api key and api secret.

	library("twitteR")
	library('base64enc') #to correctly authenticate
	library("httpuv")
	setup_twitter_oauth("xxxxx","xxxxxxxx") 


Send DM to users
	
	dmSend("hihihi","user") 

View available locations

	availableTrendLocations() 

View trends in boston

	getTrends(2367105,exclude=NULL)

View worldwide trends

	getTrends(1,exclude=NULL)

Search twitter

	tweets<-searchTwitter("cats", n=500, lang="en")

To extract the text:
	
	text<-sapply(mach_tweets, function(x) x$getText())

To extract entire data to data frame:
	
	df<-twListToDF(text)

To order data by highest retweets
	
	test<-sqldf("select text,screenName,favoriteCount,retweetCount from df order by retweetCount desc, favoriteCount desc")

