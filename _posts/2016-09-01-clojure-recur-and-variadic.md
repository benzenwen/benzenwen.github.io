---
layout: post
title:  "Clojure recur and variadic functions"
categories: programming
tags: clojure wtf programming venting 
date:   2016-09-01
comments: True
---

tl;dr: for a `recur` call to a variadic function, wrap the variadic
parameters in a `(list ..)`

-----

I am writing this for my future self because I'll stub my toe on this
again if I don't.  Future self, you're welcome.

So, I was editing a function to use `recur`.  It was my first time
using `recur` with a variadic parameter.

WTF. The `recur` invocation threw an error.  Walking in the debugger
confused me further. What saved me from frustration was this in the middle of the community documentation for
[recur](http://clojuredocs.org/clojure.core/recur#example-55ff3cd4e4b08e404b6c1c7f).

> ; Note that recur can be surprising when using variadic functions.

And in the official [docs](http://clojure.org/reference/special_forms#recur)

> The recur expression must match the arity of the recursion point exactly. In particular, if the recursion point was the top of a variadic fn method, there is no gathering of rest args - a single seq (or null) should be passed.

Well, good to know. 

And here's the function I was refactoring.

```clojure
(defn cleave-repeat
  "Finds a repeating pattern in string s using r as the next attempt to try."
  [s & [r]]               ; http://clojuredocs.org/clojure.core/recur 
                          ; recur with variadic does not wrap r in
                          ; a list. So a normal function call and recur'd one will otherwise differ.
  (if (empty? s)
    r
    (if (empty? r)
      (cleave-repeat (apply str (rest s)) (str (first s))) ; This calls the variadic "normally"
      (if (empty?                       ; We have the pattern in r if this is true
           (clojure.string/split
             (apply str (drop-last (mod (count s) (count r)) s))
             (re-pattern r)))
        r                            ; Return the pattern
        ; 'recur' calls with varadic not wrapped by a list, so (list ...) is needed.
        (recur (apply str (rest s))
          (list (clojure.string/join [r (str (first s))])))))))

```
Damn you JVM.
