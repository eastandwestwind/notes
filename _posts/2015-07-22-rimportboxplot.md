---
layout: post_page
title: Using R to import .csv and graph data
---

> getwd()
[1] "/Users/Catherine"
> setwd("/Users/Catherine/Dropbox/Docs") #this is where my .csv resides
> df<-read.csv("testtaking.csv",header=TRUE,row.names=NULL) #named by dataframe df
> head(df) #check data import
  Gender             Age Multiple.Choice Essay  X X.1
1 Female 18-24 years old             1.0    -1 NA  NA
2 Female 25-34 years old             2.0     1 NA  NA
3 Female 25-34 years old            -1.0     1 NA  NA
4 Female 18-24 years old             1.0     1 NA  NA
5 Female 25-34 years old             0.5     1 NA  NA
6 Female 18-24 years old             1.0    -1 NA  NA
> df$X<-NULL #clean up unnecessary columns				
> df$X.1<-NULL #clean up unnecessary columns
> df$Age<-NULL	#remove another unnecessary column
> df #list entire data fram to check for strange things
   Gender Multiple.Choice Essay
1  Female             1.0    -1
2  Female             2.0     1
3  Female            -1.0     1
. . .									#abbreviated for brevity here
50   Male             1.0     1
51   Male             2.0     2
52                     NA    NA
df<-na.omit(df) #omit the row with NA, in this case row 52
> library(reshape2)
> melt.df<-melt(df) #melt data so it is readable by ggplot2
Using Gender as id variables
> library(ggplot2)
> head(melt.df) #check column names for use in boxplot
  Gender        variable value
1 Female Multiple.Choice   1.0
2 Female Multiple.Choice   2.0
3 Female Multiple.Choice  -1.0
4 Female Multiple.Choice   1.0
5 Female Multiple.Choice   0.5
6 Female Multiple.Choice   1.0
> colnames(melt.df)<-c("Gender","Test.type","Difficulty") #change column names
> head(melt.df)
  Gender       Test.type Difficulty
1 Female Multiple.Choice        1.0
2 Female Multiple.Choice        2.0
3 Female Multiple.Choice       -1.0
4 Female Multiple.Choice        1.0
5 Female Multiple.Choice        0.5
6 Female Multiple.Choice        1.0
> ggplot(melt.df,aes(x=Test.type,y=Difficulty,fill=Gender)) + geom_boxplot() + scale_fill_manual(values=c("yellow","orange"))


![Boxplot](/Users/Catherine/Dropbox/Blog/images/boxplot_test_gender.pdf)