---
published: true
layout: post
title: "Every wondered why there are no concurrency issues in javascript?"
description: ""
category: null
tags: []
---

Consider the code snippet:

{% highlight javascript %}
var pending = [];

document.getElementById("submitBtn").addEventListener(function() {
    var val = document.getElementById("textBox").value;
    pending.push(val);
});

setInterval(function() {
    processValues(pending);
    pending = [];
}, 3000);

{% endhighlight %}
