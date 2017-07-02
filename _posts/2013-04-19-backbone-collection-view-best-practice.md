---
layout: post
title:  "Best Practice – Implementing a Collection View In Backbone.js"
date:   2013-04-19 13:31:32 +0300
categories: placeholder
permalink: "best-practice-implementing-a-collection-view-in-backbone-js/"
---
Backbone.js is a tool, not a framework. As a tool you can implement your solution in a lot of different ways. In this post I will discuss about how I implement a collection view in Backbone.js. It is a best practice I acquired during my exploration and development in Backbone.js.

As I see it there is mainly two ways to approach this:

* Implement the model with a model view and the collection view will just be the container that contain all the model views.
* Implement the collection view to render also the models in it.

Each of these approaches has strengths and weaknesses. And the difference is really the question of where to render the model? in the model view? or in the collection view? the intuition is to do it in the model view – but that is making a few disadvantages of interaction between the models.

The downside I have with the 2nd approach is that for any addition / subtraction from the collection the entire collection view (with all the models) will need to re-render, in a collection with thousands of models – that is a huge problem! But it has an upside too – if the models have some kind of interaction between them (sorting, filtering) it is much more easy to implement it in the 2nd approach.

The downside of the 1st approach is the upside of the 2nd and vice a versa. So I could say that I should select the solution according to my needs, and that is what I did until now. Until the day that I needed both upsides…

So the question is – is there a way to implement the 1st approach but to also have the ability to have sorting and filtering on the UI? The only way I could think about that happening is that the collection view will also hold all of the model views but that just does not sounds right.

# Go with the Model-View approach

Well, it is the combination of both that solves this problem. How can it be both? it is actually the first approach, each model has it’s own model view, so adding to the collection will not need to render the entire collection view. Only when we want to sort / filter – the entire collection view will be re-render.

# Encapsulation

This solution is really a best practice since the models does not know about the sorting / filtering that can be made to them – this will be implemented in the collection. The final visual result will be rendered in the collection view.

So when we want to render all the models that a ‘filter’ function returned us. we will run our filter function and create a model view only for those and then we will append all the model views to the collection view.

Hope that make sense.

