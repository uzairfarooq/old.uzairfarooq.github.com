---
published: true
layout: post
title: "Ever wondered why there are no concurrency issues in javascript?"
description: ""
category: null
tags: []
---

Ever wondered all the concurrency issues you were warned about in School don't apply to javascript?

Lets consider the code snippet:

{% highlight javascript linenos %}
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

Suppose line 7 gets executed and suddenly the event gets pre-empted to process the event at line 3. After executing line 3 & 4, the previous event is resumed from line 8. Now when line 8 gets executed, the newly added value in pending will be lost because it's neither processed by processValues function not it's in the pending array.

There's a race condition in it, right? 

Well, that might be true in C++ or some other language but not in javascript. Someone may have told you it's because javascript is single-threaded but that's not true. 