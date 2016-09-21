---
bg: "loops.jpg"
layout: post
title:  "Recursive Functions"
crawlertitle: "Like that one movie with the dreams"
summary: "Not some future cereal"
date:   2016-09-21
categories: posts
tags: ['infinite loops']
author: Alex Leo
---

# What is recursion?

Recursion is a computer science method where a solution can be derived from some amount of smaller solutions. This often means that a function will have to call upon itself with some sort of reduction until it reaches a base case. The base case is when the desired result can be found without another call to the function. This base case will keep the function from continually calling upon itself infinitely. Recursion can almost always be used in place of iteration and also save some time and add elegance to your code. Some examples of functions you could write using recursion are exponent and greatest common divisor. You could also implement a function that takes a given number of rounds and returns all possible moves for a rock paper scissors match or all possible combinations of change for a given dollar amount.

# Recursive Functions in Javascript

There are a few iterative functions that you may already know how to solve with a `for` loop or even a call to `.forEach()` that are great practice problems to get started on your way to understanding recursion. Recursion is not a concept that most people will pick up overnight, or in a short span of time; recursion will most likely take you some time to master and that's OK. I'm here to help you get started on your way to mastering recursion.

###### Countdown

This function is a pretty simple one that we are going to use for illustrative purposes. Countdown is a function that will log numbers to the console until it reaches 0. Take a moment to think about how you would solve this using an iterative `for` or `while` loop. We're going to be solving this using recursion, but it helps to have an illustration in your mind for comparison. What do you think the base case will be? Hint: I gave you the answer already inside this section; recursively read this paragraph until you figure out the base case. If you said our base case will be when the number passed in is equal to 0, you are correct! Our base case is when we want our recursive function to terminate, and start moving back up the call stack. Countdown(5) would look something like this:

{% highlight js %}
var countdown = function(number) {
  if (number === 0) {
    return;
  } else {
    console.log(number);
    countdown(number - 1);
  }
};
{% endhighlight %}

Our function is going to continue logging `number` to the console until `number` is 0, in which case it will finally return and stop calling itself. Please note that alternatively, you *could* make your base case 1 and call `console.log(number)` one last time before returing, in order to eliminate one step from the process for optimization, but I felt the current implementation was clearer. If this base case was omitted, your computer would continue logging `number` to the console until it ran out of memory or the interpreter is shut down. I highly recommend not trying this, or at least saving your work first.

###### Factorial

A factorial of a number is the total sum of that number multiplied by every number between itself and 1, represented by `n!`. For example 5! is 120, found by multiplying 5 * 4 * 3 * 2 * 1. Let's break this out into some code and visualize this in Javascript.

{% highlight js %}
var factorial = function(number) {
  return (number < 0) ? null : (number === 0) ? 1 : number * factorial(number - 1);
};
{% endhighlight %}

Let's examine each element of this [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) and see what our function is doing on each step. You might have noticed that we have an extra case specified besides our base case. This error case is checking if the number we are passing into our function is a negative, and returning null if it is, because factorials only apply to positive integers. The next case is our base case. We'll come back to that in just a second, can you think of how we can get our number value to reach our base case?

By passing in `number - 1` to our factorial function, we make another call to our factorial function with a number one value lower than the prevous iteration's. We are also multiplying the result of that new function's call by the current number. This will utilize what is known as the "call stack." The call stack is a stack based data structure - last in, first out - that allows a function to keep track of where it was called from. The call stack will stand by, waiting for the bottom return value to return and move back up the chain. Finally, once 0 is passed in to our factorial function, we hit our base case, return the value 1.

The interpreter will then travel back up the call stack, and eventually return the amount:

**120** once the 5 is multiplied by the return value of `factorial(4)`, which was 24.

24 was returned when 4 was multiplied by the value of `factorial(3)`, which was 6.

6 was returned when 3 was multiplied by the value of `factorial(2)`, which was 2.

2 was returned when 2 was multiplied by the value of `factorial(1)`, was was 1.

1 was returned when 1 was multiplied by the value of `factorial(0)`, which was 1.

This time our result does not have another call to factorial because we have hit our base case and simply returned 1. If you follow this stack backwards you should see how one can get from 1 to 120 using the call to `factorial(5)`.

# Summary

To understand recursion, one must first understand recursion. For another excellent blog post on recursion, [please see here.](https://aleo23.github.io/posts/recursive-functions/) A recursive function calls upon itself until it reaches the specified base case. Always remember to specify a base case and get one step closer to the base case on each iteration. Otherwise your recursive function becomes a resource eating glutton and [all your base](https://www.youtube.com/watch?v=8fvTxv46ano) are belong to us. Many problems can be solved through recursion, and practice will achieve mastery. Try refactoring some of your currently implemented iterative functions in recursion and feel the power!

## See Also

-[Recursion Prompts](https://github.com/JS-Challenges/recursion-prompts)

-[funfunfunction's video all about Recursion, as part of his series on Functional programming in Javascript.](https://www.youtube.com/watch?v=k7-N8R0-KY4)

-[Codecademy's Recursion in Javascript Course](http://www.codecademy.com/courses/javascript-lesson-205)


