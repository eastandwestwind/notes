---
title: Repeat items in vector
---

My vector:

	n<-c(362.156,260.475,883.575,326.012,249.444,796.299)

I want to repeat each item in vector 3 times.

	list<-1:length(n)
	f<-function(x){rep(n[x],3)}
	n<-unlist(lapply(list,f))

