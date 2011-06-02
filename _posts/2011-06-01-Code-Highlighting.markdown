---
layout: post
title: Code Highlighting
published: false
---

Anscheinend soll mit jekyll Code Highlighting gut gehen:

{% highlight python %}
import pprint

def fun(a):
    print "Hello jekyll world"
    filtered = [c.first for c in a if c.last < 6]
    pprint.pprint(filtered)

{% endhighlight %}
