---
layout: post
title:  "Clojure Conditional Breakpoint on Passed Function Name"
categories: programming
tags: clojure programming 
date:   2017-06-07
comments: True
---
Conditional breakpoint in Clojure to match a passed function's
name/class, using Emacs and Cider.  Clojure 1.8.0. CIDER 0.13.0.

Insert this in front of the expression you want to break on.


```
      #dbg ^{:break/when (re-find #"draw_row" (str (class f)))}
```
