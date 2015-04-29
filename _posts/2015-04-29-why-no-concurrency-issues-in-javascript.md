---
published: true
layout: post
title: "Every wondered why there are no concurrency issues in javascript?"
description: ""
category: null
tags: []
---

Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.

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
