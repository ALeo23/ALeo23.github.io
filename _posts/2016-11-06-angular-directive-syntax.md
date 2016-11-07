---
bg: "glasses.jpg"
layout: post
title:  "Angular Directive Syntax"
crawlertitle: "Angular Directives"
summary: "More Power."
date:   2016-11-06
categories: posts
tags: ['Custom Elements.']
author: Alex Leo
---

## Angular Directives

*For the purposes of this article, we'll be discussing Angular 1 and not Angular 2.*

[Angular directives](https://docs.angularjs.org/guide/directive) are powerful markers placed on or in DOM elements that associate behavior with the marked element. When the DOM is loaded, Angular uses an HTML compiler to create the element needed into a template. A template function is also produced which links the scope to the template, to create data binding. Angular allows users to create custom directives in addition to the out of the box directives included with Angular.

Some of the commonly used directives  are `ngModel` and `ngIf`. Angular also provides the ability to create custom directives, which can be defined as attributes, elements, classes, and comments. Angular recommends using attributes and elements directives over classes and comments, as it is easier to determine the element that the directive matches.

## Attribute and Element directives

Attribute directives are placed onto an HTML element to provide that element with the defined behavior. For example, the directives `ngShow` and `ngIf` are both attribute directives. The key difference between `ngShow` and `ngIf` is that `ngIf` removes and recreates a DOM element, whereas `ngShow` will toggle the element's display property, but not remove the element from the DOM.

{% highlight html %}

<img ng-show="!DetailsVm.poster_path" src="http://s2.dmcdn.net/Ub1O8/1280x720-mCQ.jpg" alt="">

<img ng-if="!DetailsVm.poster_path" src="https://i.ytimg.com/vi/MveqXxB12YA/hqdefault.jpg" alt="">

{% endhighlight %}
*This is how one might use `ngShow` and `ngIf` in their own code.*

The attribute directives above augment an existing HTML element and give that element a certain expected behavior. Element directives have many of the same powers and can be used in ways similar to templates in keeping code concise and modular.

{% highlight html %}

<funny-cat ng-show="!DetailsVm.poster_path" src="http://s2.dmcdn.net/Ub1O8/1280x720-mCQ.jpg" alt=""></funny-cat>

<funny-dog ng-if="!DetailsVm.poster_path" src="https://i.ytimg.com/vi/MveqXxB12YA/hqdefault.jpg" alt=""></funny-dog>

{% endhighlight %}
*`funny-cat` and `funny-dog` are examples of custom element directives.*



## Creating a Custom Directive

The current project is a movie website that contains details about movies and TV shows accompanied by a robust search engine. A user can enter a search query and be taken to a results page, where a list of movies and TV shows awaits. In Angular, one solution would be to create an unordered list, and use `ngRepeat` to fill that list with list item elements. This approach works, but can become extremely messy, depending on how much data is displayed on each search result. In an effort to develop modular, beautiful code, a custom directive can be used to inject HTML into a document from a template's URL.

The program will first require a directive to be created on the accompanying controller. Using the search results example, the controller in question might be called ResultsController. Directives can take a few different options when created which define the behaviors bound to that DOM element. Angular's `.directive` takes two arguments by default; the first argument is the name of the directive, a string. A callback function is passed in as the second argument, which returns an object with configuration options for the directive.

{% highlight html %}
<!--restrict types-->
<!-- 'A' -->
<div search-result></div>
<!-- 'E' -->
<search-result></search-result>
<!-- 'A' -->
<span class="search-result"></span>
{% endhighlight %}

* `restrict` - Restricts how a directive can be used
    * 'A' - Directive can be used as an attribute on an HTML element
    * 'E' - Directive can be used as an HTML element
    * 'C' - Directive can be used as a class on an HTML element
    * 'M' - Directive can be used as a comment within the HTML
      * Comment directives are somewhat deprecated and `ng-repeat-start` and `ng-repeat-end` should be used instead to populate `<table>` elements
* `replace` - Determines whether HTML element declared on will be replaced
    * Takes a boolean value
    * Ex. If an attribute directive is on a div, true would replace the div, and false would nest the directive inside the div
* `scope` - Create an isolate scope for the directive to separate the scopes
    * Allows the outer scope to be mapped to the inner scope
    * Makes results more dynamic so code is more DRY
    * Scope can take a scope object as well to create a new scope for the directive
* `templateUrl` - Defines path to the HTML file that contains HTML to insert

{% highlight js %}
//Results is a factory defined in another file
angular.module('reviews.results', [])
//ResultsVm is defined inside the collapsed controller block
//and mostly contains data to be inserted into the DOM
.controller('ResultsController', function(Results) { ... })
.directive('searchResult', function() {
  return {
    restrict: 'AE',
    replace: true,
    scope: true,
    templateUrl: 'app/results/searchResult.html'
  };
});
{% endhighlight %}


The custom behavior has been defined in the Javascript files and the HTML will need to be edited to reflect the new behvaior. Here's the program without any custom directives:


{% highlight html %}
  <div class="container">
    <!--Displays number of total results found from query. -->
    <h4>Your search returned {{ ResultsVm.totalResults }} results.</h4>
    <a ng-repeat="result in ResultsVm.results" href="/#/details/{{ result.media_type }}/{{ result.id }}">
      <!--ng-if Hides results which are generally less useful -->
      <div class="result" ng-if="result.poster_path !== null">
        <div class="resultPoster">
          <!-- If invalid poster_path or profile_path, don't display the image -->
          <img ng-hide="!result.poster_path" src="http://image.tmdb.org/t/p/w185/{{ result.poster_path }}" alt="">
          <img ng-hide="!result.profile_path" src="http://image.tmdb.org/t/p/w185/{{ result.profile_path }}" alt="">
        </div>
      </div>
    </a>
  </div>
{% endhighlight %}
*If you're not sure what ResultsVm means, go check out my blog post on using controllerAs!*

Ideally, we could re-factor this code to be two separate files, since we really have two separate intents here. One intent is that the program will need to display a list of search results. The other intent for the results page is that each search result will need to display details for one result. Creating a directive involves modifying the controller and creating a new HTML file to hold our directive.

{% highlight html %}
<!--app/results/searchResult.html-->
<!--This code represents our list of search results. -->
<div class="container">
  <div>
    <h4>Your search returned {{ ResultsVm.totalResults }} results.</h4>
    <!--Element directive is inserted here. -->
    <search-result ng-repeat="result in ResultsVm.results"></search-result>
  </div>
</div>
{% endhighlight %}

There is a separation of concerns between displaying results and displaying details.These two files have been separated to reflect each concern, the above displaying all results, while the below displays the details of each result.

{% highlight html %}
<!--app/results/results.html-->
<!--We can factor out this code as this will represent our search result. -->
<a href="/#/details/{{ result.media_type }}/{{ result.id }}">
  <div class="result" ng-if="result.poster_path !== null">
    <div class="resultPoster">
      <img ng-hide="!result.poster_path" src="http://image.tmdb.org/t/p/w185/{{ result.poster_path }}" alt="">
      <img ng-hide="!result.profile_path" src="http://image.tmdb.org/t/p/w185/{{ result.profile_path }}" alt="">
      <img ng-show="!result.poster_path && !result.profile_path" src="http://dummyimage.com/185x275/000/fff&text={{result.name}}" alt="">
    </div>
</a>

{% endhighlight %}
*Take notice that the ng-repeat goes on the directive, as this is the item that needs to be repeated, for each result.*

Above is an example of two different HTML files being used together to make up a primitive search results page. The difference is that we have refactored the code based on intent. The intention to display a list of search results has been placed into the first file. Using directives, the HTML compiler is instructed that this first file will need the contents of the second file. An element tag is created where the content will need to be injected, using the contents of the second file, and the `ngRepeat` tells the compiler that this will happen more than once.

## One More Time

Angular provides directives as a powerful way to define custom behavior within a program. Directives enforce clean, modular code that is more maintainable. The controller file is usually where directives are written and stored. The HTML will then need to be re-factored, or freshly written, to use the newly defined directives. Element and attribute directives are considered best practice and directive templateUrls should be used to keep the codebase concise and maintainable.

Below are some additional resources for Angular and this style, happy coding!

As always, I'd love to hear your feedback via [email](mailto:aleo1337@gmail.com)!

## See Also

-[Angular JS](https://angularjs.org/)

-[Angular JS Directives](https://docs.angularjs.org/guide/directive)

-[A Practical Guide to Using AngularJS Directives](https://www.sitepoint.com/practical-guide-angularjs-directives/)

-[John Papa's Style Guide - Directives](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#directives)


