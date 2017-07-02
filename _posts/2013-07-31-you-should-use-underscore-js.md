---
layout: post
title:  "You should use Underscore.js"
date:   2013-07-31 13:32:32 +0300
categories: placeholder
permalink: "you-should-use-underscore-js/"
---
I must admit, the first time i encountered Underscore.js i didn’t get it. All I saw is a bunch of functions.
You want to use underscore.js, you might don’t know it yet but you do.

Underscore.js is exactly what it seems – it is bunch of functions. These collection of functions have one true goal – to make you put your attention on developing your logic and make some operations trivial. If you are familiar with jQuery, than you probably know the benefits of how it is simplifying the DOM manipulation, Underscore.js is similar to that in a manner that it is simplifying data manipulation in JavaScript.

Underscore give your JavaScript coding a turbo engine by giving you functions that let you sort and filter your data really easily.

The easiest way to understand Underscore.js is by an example:

Let’s say that you have a collection (an array of JavaScript objects of the same kind) of student grades and you want to give student id ‘15’ an extra 10 points.

In pure JavaScript it could look like this

{% highlight javascript %}
var counter,length;
for(counter=0, length=students.length ; counter<length ; ++counter){
	if( '15' == students[counter].id ){
		students[counter].grade += 10;
        // you could use "break" here when you find the object
        // but you have to be aware that you should
	}
}
{% endhighlight %}

In Underscore.js it will be much simpler:
{% highlight javascript %}
var student = _.findWhere( students, { id : ‘15’ } );
if( student ) student.grade +=10;
{% endhighlight %}

At first it looks a bit weird to use the ‘_’ as an object, but if you got used to the jquery ‘$’ you will get used to this one too.

The findWhere function will go over the collection and will return the first occurrence of the the student with an ‘id’ of ‘15’, this is really efficient because if you have 1,000,000 students – it does not have to go over all of them – as soon as it finds it – it will stop the search.

besides the performance boost and the fact that it was easier to write you can see that it is easier to read – that is an awesome bonus because six month from now when you want to add a cool feature to your code you can understand it better because it is more readable.

Another example is to create a function that returns how many students got a grade that is higher than 85:

{% highlight javascript %}
function higherThan85(students){
 var number = 0, student;
 for( student in students ){
  if( 85 < students[student].grade) ++number;
 }
 return number;
}
{% endhighlight %}

And the Underscore.js version:

{% highlight javascript %}
function higherThan85(students){
 var filtered = _.filter( students , function(el){
	return (85 < el.grade);
 });
 return filtered.length;
}
{% endhighlight %}

the function that is passed as a second parameter to the filter function is the actual filter function, that mean that each object that will return true from that function will be added to the filtered collection – in our case each object that has a grade that is higher than 85 will be in the filtered array collection.

We could use some other function called *countBy* to get a similar (yet different) solution:

{% highlight javascript %}
var resultObj = _.countBy( students, function(s){ 
 return (85 < el.grade) ‘higherThan85’ : ‘smallerThan86’;
}); 
console.log( resultObj.higherThan85 ); //will log the number of students higher than 85
console.log( resultObj.smallerThan86 ); //will log the number of students smaller than 86
{% endhighlight %}

As you can see – complex logic can become really easy with the power of Underscore.js functions – and I showed only a few of the more simple ones. You can use complex operations like ‘map’ and ‘reduce’. Reduce function could be used for summing operations over objects, for example:

Let’s say that we have a collection of family, and each object in the family have an income. We want to calculate the total income of the family members. So, that’s easy with reduce:

{% highlight javascript %}
var result = _.reduce(family, function(el, sum){return (el.income +sum);}, 0);
{% endhighlight %}

That’s it! If you wonder what is the third argument, it is the initialization of the sum var – but it can be practically anything.

Underscore has a lot more functions to handle objects and object collections – you can find out all the function reference API on [Underscore.js website][link1].

Underscore.js have more features except from from the previous functionality, it has a built in templating function, a simple one, but that is where it is powerful – it is also simple to use…

All Underscore functions are chane-able,  Another characteristic similar to jQuery.

Extending Underscore.js to your own use case:

It is very easy to extend Underscore.js and built on top of it – just use the mixin function to do that:

{% highlight javascript %}
_.mixin({
  capitalize : function(string) {
    return string.charAt(0).toUpperCase() + string.substring(1).toLowerCase();
  }
});
_("fabio").capitalize();
//=> "Fabio"
{% endhighlight %}

That example show a simple way to extend Underscore function base to your own, in this case we created a new function called capitalize which capitalize the first letter of the string and turning to lower case any other character.

Please note that in addition to all of the above Underscore also has a section on functions – this section can help you bind function and other helpful development workflow like ensuring a function could get called only once, delayed, run only after called X times and much more.

I want to end this post here, not because I don’t have anything else to add about Undescore functionality – it has a lot more power, that you can discover for yourself in the [project website][link1]. I encourage you to do so! go ahead and play around

[link1]: http://underscorejs.org/