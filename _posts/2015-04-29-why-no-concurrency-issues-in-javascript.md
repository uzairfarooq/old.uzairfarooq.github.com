---
published: true
layout: post
title: "Every wondered why there are no concurrency issues in javascript?"
description: ""
category: null
tags: []
---

Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.

{% highlight ruby %}
1  var pending = [];

2  document.getElementById("submitBtn").addEventListener(function() {
3      var val = document.getElementById("textBox").value;
4      pending.push(val);
5  });

6  setInterval(function() {
7     processValues(pending);
8     pending = [];
9  }, 3000);

{% endhighlight %}
