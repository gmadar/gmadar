---
layout: post
title:  "Mini Review of “Secrets of the JavaScript Ninja” By John Resig & Bear Bibeault"
date:   2013-04-19 13:31:32 +0300
categories: placeholder
permalink: "mini-review-of-secrets-of-the-javascript-ninja-by-john-resig-bear-bibeault/"
---
I have started reading the new book of John Resig, the creator of jQuery. I’m just in the beginning (page ~60) – but i still have a few insights that I would like to share:

# A free e-book!

When you buy the book, inside of it you get a code which you can use to get the e-book version for free. That was a very nice gesture from Manning that i really like. That way i don’t need to choose, I get both. and it is a great surprise since I was not aware of that.

# About the book

I really like how the book is organized, it is well structured, written clear and simple. The book addresses the reader in a way that reminded me a private tooter. It does not uses high language and it is very easy to follow, both the text and also the examples.

# Who the book is for?

This book is not for a novice developer. If you have a good grasp of JavaScript then this book is for you, it will uncover some of Javascript black magic, with a fun approach. if you are a newbie in Javascript – this book is probably not for you. you should start with a more basic material and only then read this book. I think every front end developer should read this book – but if you just beginning – read some more basic stuff and only then return to this book.

# Scoping – A small point that was overseen

When the writer is explaining about scoping, he wrote that the function scope is within the entire current scope even if it is defined at the end of the current scope. And in the example that was given it was implied that a variable is not acting like that. But it is! It is available. It is only that the assigned value is available after the assignment, but the variable itself exist in the scope. That maybe sounds like an unimportant point but it could cause an unexpected bugs like in this example:

{% highlight javascript %}
var test = "I'm out";

function func(){
 alert( test );
 var test = "I'm in";
}

// alerts undefined
{% endhighlight %}

You would think that the value of ‘test’ will be “I’m out” according to the book explanation, but because of the hoisting nature of Javascript it is actually will be ‘undefined’, hoisting is not only for functions it is also for variables. The only difference is that functions will be defined even if the declaration is after the function call while in variables it is not.

So we can actually say that the above code will actually behave like the next one:

{% highlight javascript %}
var test = "I'm out";

function func(){
 var test;

 alert( test );
 test = "I'm in";
}
{% endhighlight %}