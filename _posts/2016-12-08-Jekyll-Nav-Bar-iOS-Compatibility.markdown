---
layout: post
title:  "Jekyll Nav Bar iOS Compatibility Study"
date:   2016-12-08
categories: 
---

To check the context of this post, see [this thread](https://github.com/jekyll/minima/issues/80) on GitHub.
Follow [here](https://www.nczonline.net/blog/2012/07/05/ios-has-a-hover-problem/){:target="_blank"}.

<style>
p:hover a {
    color: red;
}
</style>
<p><a href="#">Test me</a></p>

<style>
    p span {
        display: none;
    }

    p:hover span {
        display: inline;
    }
</style>
<p><a href="/">Tap me</a><span>You tapped!</span></p>


Solution to the original problem.
Add attribute `onclick = "void(0)"` to `span` and also `header` elements. See [Apple Doc](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/HandlingEvents/HandlingEvents.html){:target="_blank"} for more.
