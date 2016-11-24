---
bg: "lightning.jpeg"
layout: post
title:  "Algorithmic Time Complexities"
crawlertitle: "Measuring Time Complexity"
summary: "Know how performant a solution is"
date:   2016-11-22
categories: posts
tags: ['Measuring efficiency']
author: Alex Leo
---

## Time Complexity ##

Algorithmic time complexity is used to describe the efficiency of a given function in terms of the time the function takes to complete. A standard for describing time complexity exists in the form of *Big O* notation, as indicated below the title for each corresponding section that follows. Big O looks like this: O(time), where time is the operations the function takes to complete calculating based on the input. Big O measures the upper bounds of efficiency, meaning that we are focusing on the worst-case scenario when calculating the efficiency. When calculating complexity, it helps to imagine how many times the entire input will need to be iterated over. Many variables exist as to how long a function will actually take to run, such as computer performance, so simply measuring runtime is not enough. This is akin to saying that two people may take different amounts of time to solve a problem, even if they are using the same algorithm.

## Constant ##

#### O(1) ####

Operations with a constant complexity always perform at a constant rate, regardless of their input size. This does not mean that they return instantly, though they generally return very quickly. Constant time operations are generally the most desirable and represent some of the fastest operations in Javascript. Retrieving a value from an array or object is considered a constant time operation. For example, if a function has a constant time complexity and takes about 100ms to run with an input of size 10, it will also take about 100ms to run if the input size is 1,000.

{% highlight js %}
function constantRetrieve(array, index) {
  return array[index];
}

{% endhighlight %}
*This function runs in constant time; regardless of input size, the function will always take about the same amount of time to look up a value in the array.*

## Amortized Constant ##

#### O(1) ####

An amortized constant time complexity is similar in operating time to a constant time complexity, however it has a seldom but reocurring step than takes far longer than all other constant iterations. Amortized constant is a representation of how long the average iteration will take, making note that one iteration may, in the worst case, take much longer, but only once within a large number of iterations. For example, we'll say brewing tea every day always takes me 2 minutes, but once a year (I buy a lot of tea) I have to go to the store and buy more tea before I can brew more, which would increase the brew time, on that day only, to 1 hour. It's safe to say brewing tea takes me 2 minutes, even though once a year it does take me an hour.

## Logarithmic ##

#### O(log n) ####

A function with a logarithmic time complexity will become more efficient on each iteration. Each iteration will take less time than the iteration before it. This usually means that the size of the input gets smaller on each iteration. For example, a binary search tree runs on a logarithmic time complexity when finding values, because it is halved in size on each iteration, until reaching its target value or the end of the tree. If input size is 24 on first iteration, it will be 12 on the next, then 6 and continuing to get smaller and faster until the function returns.

## Linear ##

#### O(n) ####

Linear time complexity operations grow at a constant rate directly with the size of the input. The bigger the input size, the longer the function will take. A simple for loop that must iterate over each value in an array once would be a linear operation. In the worst case for a linear time complexity function, each value in the input must be iterated over at most one time. Linear functions will grow at a constant rate, but do not operate in constant time.

{% highlight js %}
function printArray(array) {
  array.forEach(function(item) {
    console.log(item);
  })
}

{% endhighlight %}
*This function will always log every value inside of the provided array. In order to perform this task, the function must iterate over each item in the array once. The runtime of our function is directly related to the size of the input.*

## Quadratic ##

#### O(n^2) ####

A quadratic time operation grows with input size to the power of 2. This is usually because the input will have to be iterated over twice for each iteration. For example, if a function takes an input and iterates over each value in that input, and for each value in that input the function also must again iterate over each value on each iteration, it would have a quadratic complexity. Each value in the input must iterate over every other value in the input, in the worst cases.

{% highlight js %}
function combine(array) {
  var result = [];
  for (var i = 0; i < array.length; i++) {
    for (var j = 0; j < array.length; j++) {
      result.push([i, j])
    }
  }
  return result;
}

{% endhighlight %}
*This function is not entirely useful for much more than illustration purposes. The combine function will need to pass over every value in the array in the first for loop. Inside of each iteration on the outer for loop, an inner for loop will need to iterate over each item in the array. For every value in the first loop, we will iterate over every value in the collection.*

## Exponential ##

#### O(c^n) ####

Exponential are some of the most inefficient of time complexities. An exponential function's time complexity will grow rapidly (exponentially) with input size. Any relatively large input will generally make one of these functions time out or take an exceptionally long time to complete. A function might have an exponential time complexity if it has to iterate over every input value using a large amount of nested for loops, which also in turn iterate over every input value, again and again and again. Exponential time complexity is rare and generally best avoided.

## Trimming Calculations ##

Big O is used to describe the runtime in relation to the input agnostic of these smaller details and variables. Think of O as a filter that leaves behind only the most significant portion of the complexity. Big O notation is always described in terms of an end result, as depicted above in examples. Computers perform caluclations at very high speeds and the extra data that will be dropped is decreasignly signifcant as the input grows in size. Provided a complexity of: `O(3n + 100)`, this can be simplified to O(n) because constant values increase n at a predictable, steady, constant rate. Constant rates will have a diminishing effect as the size of n increases. Even a time complexity of `O(1000n^2 + 5000)` would reduce to simply O(n^2).

## Other Time Complexities ##

More time complexities exist beyond the ones covered in this post. These complexities will describe the majority of functions that programmers write, especially in Javascript. Be wary of simply counting `for` loops in code to determine the time complexity of a function. Not all `for` loops will iterate over an array of varying size. Be sure to check which collection a given `for` loop, or equivalent iterating function, is iterating over when calculating complexity.

## See Also ##

- [Four Semesters of CS](http://btholt.github.io/four-semesters-of-cs/)

- [Big O Cheat Sheet](http://bigocheatsheet.com/)

- [Algorithm's Orbit](http://mohalgorithmsorbit.blogspot.com/)





















