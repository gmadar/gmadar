---
layout: post
title:  "Getting to Know JavaScript Scoping"
date:   2013-10-14 13:33:32 +0300
categories: placeholder
permalink: "getting-to-know-javascript-scoping/"
---

Becoming a Pro in JavaScript requires a few capabilities, one of the most important ones, is understanding JavaScript variable scoping. A lot of developers that came from a different programming language bang their head in the wall until they fully understand JavaScript scoping mechanism. Let’s start:

# What is Scoping?

Access everything from anywhere is not a good thing when it comes to software development. You want your code to be predictable and if anyone can change a variable value - it will cause trouble. Each function and variable in JavaScript has a scope, you may have not been aware to the existence of that scope, but it does exist. A scope is basically an access mechanism to an object, function or variable. if you can access an object than you are in the object scope, and If you have no access, you are out of scope. There is a scope that is accessible from anywhere – the global scope. but let’s first start with the simple scope mechanism – the function scope.

# Function Scope

In JavaScript – the scope is changed only in functions and not in any curly braces {..} like in a lot of other languages. If we'll take a look at the next example we can see that we can’t access the ‘bar’ variable. Since we're trying to access it from outside the function, we try to access a variable out of the scope and that is not possible. The alert will throw a “ReferenceError: bar is not defined”.

{% highlight javascript %}
function bar(){
	var baz = “world”;
}
alert(baz); // throws - ReferenceError: baz is not defined
{% endhighlight %}

The function ‘bar’ has it’s own scope and anything that will be defined in the function could not be accessed outside of the function.

# Global Scope

The global scope can be accessed from everywhere, as a rule of thumb there should be as little global scope variable as possible. A lot of global variables can cause conflicts in complex applications.

Access from everywhere means that you can access the global scope from any portion of your code, at any time. When a variable is scoped globally it can also be accessed through the ‘window’ object, I mention that because of the next example:

{% highlight javascript %}
//global scope
var foo = “world”;
function bar(){
	//function scope
	var foo = “hello”;
	alert( foo ); //alerts “hello”
	alert( window.foo ); //alerts “world”
}
{% endhighlight %}

There are mainly 3 ways to declare a variable in the global scope:

* Each variable that will be declared in the main script, that means not inside a function will be scoped in the global scope

* Declaring a variable without using the ‘var’ keyword will cause the variable to be scoped globally, no matter where it was declared. This is a huge pitfall for a lot of beginners.

* Adding a property directly to the ‘window’ object - window.foo = “hello” (like the example above)

From the above example we can learn that although the scoped var foo in the function is now “hello” the original foo variable is still accessible through the window object who holds all the global variables.

As I said before, any variable or function that is declared outside a function or object will be scoped automatically in the global scope.

# Always Declare your Variables

When declaring a variable – it should always be prepended with “var”, not doing this will cause the variable to be scoped globally. that can cause an unexpected behavior.

Look at the next example in order to understand how forgetting to prepend a variable with the ‘var’ keyword will cause the ‘bar’ variable to be scoped globally :

{% highlight javascript %}
//global scope
function bar(){
	//function scope
	bar = “world”; // ‘var’ is missing
}
alert(bar); // alerts “world”
{% endhighlight %}

To understand the problem that could arise from this, take a look at the next example:

{% highlight javascript %}
//global scope
var i=true;

// => i = true;
foo();
// => i = 0;

if( i ){
 console.log(“i is true”);
}

function foo(){
 for(i=10; i>0 ; --i){
  console.log(i);
 }
}
{% endhighlight %}

The ‘var’ keyword was not used in the for loop. Variable ‘i’ is used in the global scope. The console will not say that “i is true” because ‘i’ is actually equals to zero. we called the foo() function before our if.

So to summarize how you should use any var in a function, don’t use it in a global scope like that:

{% highlight javascript %}
function foo(){
 for(i=0; i<50; ++i){
  //do something
 }
}
{% endhighlight %}

You might think it is better to do it like this:

{% highlight javascript %}
function foo(){
 for(var i=0; i<50; ++i){
  //do something
 }
}
{% endhighlight %}

But you will be wrong, well, at least not 100% right..
The best way is to declare it at the beginning of the scope:

{% highlight javascript %}
function foo(){
 var i;
 for(i=0; i<50; ++i){
  //do something
 }
}
{% endhighlight %}

Why? well, it is the preferred way because of what is called Hoisting.

# JavaScript Hoisting

Hoisting is a strange behavior when you first hearing about it, what it means is that any variables / function that belong to the current scope will be declared at the beginning of the scope. the difference between a variable and a function hoisting is that the function will have a value in the beginning of the scope while a variable will be undefined.

Why is that something that is important to know? take a look at the next example:

{% highlight javascript %}
//global scope
var foo = ‘hello’;
bar();

function bar(){
 console.log(foo);
 var foo = ‘world’;
 console.log(foo);
}
{% endhighlight %}

you would think that the output will first log ‘hello’ and ‘world’ but it will actually will log ‘undefined’ and ‘world’.
why? Hoisting! that is why… with hoisting your code will actually be interpreted as:

{% highlight javascript %}
//global scope
var foo = ‘hello’;
bar();

function bar(){
 var foo;
 console.log(foo);
 foo = ‘world’;
 console.log(foo);
}
{% endhighlight %}

So in order to not be surprised with unexpected behavior – it will be a good idea to always declare any variable that is used in the scope at the beginning of the scope.

Unlike variables, functions have their value when called before their declaration. You can see that from the last example where we called the ‘bar’ function before it was declared, That was possible because of hoisting that was interpreted into:

{% highlight javascript %}
//global scope
function bar(){
 var foo;
 console.log(foo);
 foo = ‘world’;
 console.log(foo);
}

var foo = ‘hello’;
bar();
{% endhighlight %}

# Conclusion
Scoping in JavaScript can be tricky. but all the common pitfalls can be avoided with the coding conventions I presented – declare all scoped variable at the beginning of the scope and prepend all variable declaration with the ‘var’ keyword.