---
layout: post_page
title: R merge multiple files
---

I've got email marketing data in 6 separate files, one for each email campain. I need to merge these together to find general stats.

	>setwd("/Users/csmith/Dropbox/emails")
	>df1<-read.csv("email1.csv",header=TRUE,row.names=NULL)
	>df2<-read.csv("email2.csv",header=TRUE,row.names=NULL)
	>df3<-read.csv("email3.csv",header=TRUE,row.names=NULL)
	>df4<-read.csv("email4.csv",header=TRUE,row.names=NULL)
	>df5<-read.csv("email5.csv",header=TRUE,row.names=NULL)
	>df6<-read.csv("email6.csv",header=TRUE,row.names=NULL)

Now that I've read in all 6 files, I merge them together.

	>dfmerge<-Reduce(function(x, y) merge(x, y, all=TRUE), list(df1, df2, df3,df4,df5,df6))
	>write.csv(dfmerge,file="merge.csv",row.names=FALSE)

I have a couple entries to exclude, so I do this:

	>excludeid<-c(31277656065,31349627905,32293885953,32316235777,32378504193,32895147009,32982722561,33025049601,33489939457)
	>dfmerge<-lapply(excludeid,function(i){
	+	dfmerge[!grepl(i,dfmerge$SharpSpringID),]
	+})

To retreive general stats about the email campaigns as a whole:

	>sent<-nrow(dfmerge)
	>sent
	>opens<-sum(dfmerge$Open.Date!="")
	>opens
	>openrate<-opens/sent
	>openrate
	>clicks<-sum(dfmerge$Click.Date!="",na.rm=TRUE)
	>clicks
	>clicktoopen<-clicks/opens
	>clicktoopen
	>clicktosent<-clicks/sent
	>clicktosent