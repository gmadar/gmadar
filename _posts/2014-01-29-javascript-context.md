---
layout: post
title:  "JavaScript Context is Actually Easy to Understand"
date:   2014-01-29 13:35:32 +0300
categories: placeholder
permalink: "javascript-context-is-actually-easy-to-understand/"
---

One of the most misunderstood concepts of JavaScript is the context topic. When saying context I’m referring to the ‘this’ keyword inside a function.
Now let’s break that down:

If it is a constructor than the ‘this’ keyword will refer to the newly created object.
So when creating an object with the ‘new’ keyword the context of the ‘this’ keyword is the new object that was created. But if the function would have been called without the ‘new’ keyword than the context would be the global context meaning the global ‘window’ object

{% highlight javascript %}
function Doo(){
 this.try = true;
}

var dooObj = new Doo();
// dooObj.try = true!

var dooObj2 = Doo();
// dooObj2.try = undefined
// window.try = true
{% endhighlight %}

On an object the context is the object the function is executed on. Sounds confusing? A simple example will clear that out:

{% highlight javascript %}
var foo = {
 bar : function(){
  this.try = true;
 }
};

// foo.try = undefined

foo.bar();
// foo.try = true
{% endhighlight %}

This is it! It is simple as it seems. Why there is so muxh confusion? Things can go a bit more complex when we want to use a different context than the current one. Let’s look at another example:

{% highlight javascript %}
var obj = {
 counter : 0,
 doo: function(){
  var context = this;
  this.doo.dat = function(){
   ++context.counter;
  }
  this.doo.dat(); 
 }
};

obj.doo();
// obj.counter = 1
obj.doo();
// obj.counter = 2
{% endhighlight %}

The context var is used here because inside the ‘dat’ function we have a different context so if we used the this keyword instead of the context variable then it would refer to ‘obj.doo’ instead of just ‘obj’

Another exception of context is the ability to control the context inside a function. Using JavaScript's *call* and *apply* methods we can set the context as we wish:

{% highlight javascript %}
var dooObj = {};

function Doo(){
 this.try = true;
}

Doo.call( dooObj );
// dooObj.try = true
{% endhighlight %}

The *call* function first parameter is the context that will be available as the this keyword inside the called function. the rest of the parameters – will be the original function parameters:

{% highlight javascript %}
function func(param1, param2, param3){
 console.log(param1, param2, param3);
}

func.call(context, "a", "b", "c");
// "a", "b", "c"
{% endhighlight %}

The difference between call and apply is the way the parameters are passed:

{% highlight javascript %}
function func(param1, param2, param3){
 console.log(param1, param2, param3);
}

func.call(context, "a", "b", "c");
// "a", "b", "c"
func.apply(context, ["a", "b", "c"]);
// "a", "b", "c"
{% endhighlight %}

These two calls are equivalent, the *apply* function parameters are just passed as an array. Why do we need that? well, sometimes we have the data as an array and this will save as the conversion, no other difference besides that.