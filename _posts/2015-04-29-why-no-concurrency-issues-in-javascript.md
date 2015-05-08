---
published: true
layout: post
title: "Ever wondered why there are no concurrency issues in javascript?"
description: ""
category: null
tags: []
---

Ever wondered why all the concurrency issues you were warned about in School don't apply to javascript?

Lets consider the code snippet:

{% highlight javascript linenos %}
var pending = [];

document.getElementById("submitBtn").addEventListener(function() {
    pending.push(document.getElementById("textBox").value);
});

setInterval(function() {
    processValues(pending);
    pending = [];
}, 3000);

{% endhighlight %}

Suppose line 8 `processValues(pending)` gets executed and processes the pending values but before preceeding to next line it gets pre-empted to process another event at line 4. It executes line 4 `pending.push(document.getElementById("textBox").value);` and adds another value to pending array which is supposed to be processed by `processValues()` function. Now the previous event is resumed from line 9 and empties the `pending` array loosing the recently inserted value.

There's a race condition, right? Well, that's true in many languages (C++, Java, etc) but not in javascript. Someone may have told you it's because javascript is single-threaded but that's not true either. 

#### That's because of a feature in javaascript called [Run-to-Completion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop.22Run-to-completion.22)