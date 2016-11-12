---
bg: "typewriter.jpeg"
layout: post
title:  "What is TypeScript?"
crawlertitle: "Type + Javascript = ??"
summary: "For Simpler Debugging"
date:   2016-11-06
categories: posts
tags: ['Strictly Typed']
author: Alex Leo
---

## TypeScript

TypeScript is a strictly typed superset of Javascript. Typescript is developed by Microsoft, and introduces static typing into Javascript. In addition to static typing, TypeScript also adds class based object oriented programming, making use of ES6 classes. TypeScript transcompiles into Javascript before it can be run, and this is where most of the magic happens. When transcompiling the code, TypeScript will fire any errors it finds with assigned typing into the terminal. Note that the code will still be built, and can be run, though probably not as expected, with the incorrect types being used or applied. The warnings provided indicate that there is a problem, but this does not halt program execution. TypeScript also lends to an organzied code base, enforcing modularity with the use of code modules. It's also worth mentioning that [Visual Studio Code](https://code.visualstudio.com/) is free, open source software that comes built in with robust support for TypeScript. If you'd still prefer to use Sublime Text, they've got a [few plugins](https://packagecontrol.io/search/typescript) for TypeScript support as well!

## Static Typing

Static Typing is used in many programming languages, but Javascript is not one of them. Static typing is typically used in both functional programming as well as object oriented programming and provides programmers with a layer of logic checking during development. When the source code is written, variables, properties, methods, a function's input and output values, and other data will be assigned a type. Primitive data types include number, string, boolean, undefined, and null. Other data values include object and array, along with more special objects like Promises. Static typing is technically optional, and does not need to be provided for every single variable in the code base. A variable is statically typed when it is declared using a `: type` syntax, with any assignments(`=`) coming after the type declaration. Similarly, a return value's static typing will go after the parameter declarations, before the function body. Some annotated example code should clarify on the positioning of where to define static types.

{% highlight js %}
// Inside our TypeScript file (`.ts`)
// Static types are defined when the variable is initialized
// To the left of the '=' if the variable is being assigned to a value
var food: string = 'Pasta';
var customersPerDay: number = 100000;
var happy: boolean = true;
var declaration: string;
{% endhighlight %}

Note that the code above would look different once transcompiled into a Javascript(`.js`) file and would not have the static typing definitions within the code. TypeScript also includes "interfaces" which are like blueprints for an object. An `interface` defines the structure of an object, i.e. the properties that it should contain and their corresponding types. Static typing is pretty straightforward with a simple variable declaration, but it can get a little more complicated once combined with ES6 classes, especially for the unfamilar.

{% highlight js %}
// Inside our TypeScript file (`.ts`)
// Static types are defined when the property/method is created on the object

// This is an import statement specifically from Angular 2
// Don't worry too much about what we're importing so much as how we're doing it
import { OnInit } from '@angular/core';

// Create a Hero class that can be exported and used in other code modules
export class Hero {
  // Heroes have an id, which is an identifying number
  id: number;
  // The hero's name will be stored as a string
  name: string;
}

//an interface for our Hero, for illustration purposes
interface Hero {
  // this provides type checking for an object, defining its expected properties
  id: number;
  name: string;
}

export class HeroesComponent implements OnInit {
  // declare a heroes property for our HeroesComponent - `HeroesComponent.heroes`

  // `: Hero[]` - This is a static type that says "This will be an array of Hero objects"
    //there is no value being assigned to heroes before `ngOnInit` executes

  heroes: Hero[];

  // `: Hero` - This is a static type that says "This will be an instance of a Hero object"

  selectedHero: Hero;

  // private properties are declared inside the constructor to make available to methods
  // public properties can also be declared by using `public` in a similar fashion

  constructor(
    private heroService: HeroService
    // initialize properties using `public` here inside the constructor
  ) { }

  // `: void` - indicates that the function will have no return value

  ngOnInit(): void {
    this.getHeroes();
  }
  getHeroes(): void {
    this.heroService.getHeroes().then(heroes => this.heroes = heroes);
  }

  // provide static typing for a function/method parameter within the declaration
  gotoDetail(hero: Hero): void {
    let link = ['/detail', hero.id];
    this.router.navigate(link);
  }

  // `: any` can also be used for a variable or other value that can have any type
  var foo: any = 'Anything!';
}
{% endhighlight %}
*This code is an excerpt from the Angular Tour of Heroes tutorial, available [here](https://angular.io/docs/ts/latest/tutorial/).*

The code above uses an import statement to import a core module from Angular 2. This post is about TypeScript, and I will not go further into the details of Angular 2. This import illustrates how a module can be imported into a file using ES6 Modules. `HeroComponent` is defined with 'implements `OnInit`' which makes the `OnInit` module available to `HeroComponent`. Functions can expect a return value of `Promise` or `Observable` attached to a data type, throwing an error if an object is not being wrapped correctly. TypeScript will check a function's output to make sure a Promise is being returned, if assigned, like below. `: Promise<Hero[]>` below is telling our function that it should expect a Promise object that contains the array of Heroes. The function is turning the response from the GET request into a Promise object, to keep asynchronous functionality. The function will need to be updated accordingly from expecting just `Hero[]`, an array of Heroes, to `Promise<Hero[]>` to indicate that the desired result will be wrapped in a Promise.

{% highlight js %}
getHeroes(): Promise<Hero[]> {
  return this.http.get(this.heroesUrl)
             .toPromise()
             .then(response => response.json().data as Hero[])
             .catch(this.handleError);
}
{% endhighlight %}
*Another code sample from the Tour of Heroes tutorial; the function above expects a promisified version of a Hero array as an output.*

## Modules

TypeScript expresses a great concern for modularity. Modular code is effective, because it is easier to maintain, especially at large scale. Modularity also enforces DRY (Don't Repeat Yourself) code by creating reusable components that can be used multiple places in a code base without being repeated. TypeScript accomplishes this using import/export (ES6 Modules), similar to using `require()` and `module.exports` in Node. Functions, objects, and other variables can be exported from one file, and imported into one or many other files to be used. Long module names can also be shortened when exported using the `as` syntax pictured below.

[![exportAs]({{ site.images }}/exportAs.png)]({{ site.images }}/exportAs.png)
*Above the accompanying import would just have to import sleepCheck and not ReallyLongExportedInconvenientButNecessaryFunctionName.*

## Start Using TypeScript

TypeScript uses a CLI to compile code, which can be obtained using npm. The TypeScript CLI uses a command `tsc` to compile the data and also has support for a watch command that will compile whenever it detects a change in the files. Static typing is optional in TypeScript, so not every piece of data declared will need to be assigned a type. The file extension associated with TypeScript is `.ts` and these files compile to `.js` files, because TypeScript is a superset of Javascript. To use a static type, place a colon after the piece of data to be assigned a type, and declare the type after the colon. Primitive and non-primitive data types can be statically typed, including [Promises](https://basarat.gitbooks.io/typescript/content/docs/promise.html) and [Observables](https://scotch.io/tutorials/angular-2-http-requests-with-observables). To get started without a local install, there is a [TypeScript Playground](http://www.typescriptlang.org/play/) available, which is great for seeing how the code will compile. To install on a local machine, just use `npm install -g typescript` and compile code locally!

## See Also

-

- [TypeScript Getting Started](http://www.typescriptlang.org/docs/tutorial.html)

- [ES6 Classes in TypeScript](http://www.typescriptlang.org/docs/handbook/classes.html)























