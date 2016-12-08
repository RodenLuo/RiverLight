---
layout: post
title:  "Jekyll Nav Bar iOS Compatibility Study"
date:   2016-12-08
categories: 
---

Follow [here](https://www.nczonline.net/blog/2012/07/05/ios-has-a-hover-problem/).

<style>
a:hover {
    color: red;
}
</style>
<p><a href="/">Test me</a></p>

<style>
p:hover a {
    color: red;
}
</style>
<p><a>Test me</a></p>

<style>
    p span {
        display: none;
    }

    p:hover span {
        display: inline;
    }
</style>
<p><a href="/">Tap me</a><span>You tapped!</span></p>
