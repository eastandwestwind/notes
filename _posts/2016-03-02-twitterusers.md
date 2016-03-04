---
title: TwitteR User calls 
---

Within the R TwitteR package is the ability to getUser() or lookupUsers(). This returns an object of class user, and requires certain calls to return information about that user. Here's how to extract followers and location from a list of users. Note that due to the [API rate limit](https://dev.twitter.com/rest/reference/get/users/lookup) for the GET users/lookup method, only max 100 users can be returned by each request, and only 60 requests per 15-min window for app auth (180 for user auth). Plan accordingly.

	y<-lookupUsers(c('eastandwestwind', 'stephenleesmith'))

Or if you have a data frame of tweets and usernames

	y<-lookupUsers(df$screenName)

This function gets number of followers

	followers<-function(i){
		return(length(i$getFollowerIDs()))
	}

Lapply the function over the users

	lapply(y,followers)


You can do the same for extracting location data from the users.

	getLocation<-function(x){
		y<-getUser(x)
	    return(y$location)
	}

	locations <- lapply(df$screenName, function(x) getLocation(x))