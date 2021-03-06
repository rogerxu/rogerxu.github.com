---
layout: post
title: JavaScript Tips
---

## Introduction

JavaScript is a language that almost every developer can use to accomplish little tasks, but very few developers really understand the scope of its power, or how to take advantage of everything it can do.

## Objects

### Object Usage and Properties

### The Prototype

### `hasOwnProperty`

### The `for in` Loop

## Functions

### Function Declarations and Expressions

### How `this` Works

### Closures and References

### The `arguments` Object

### Constructors

### Scopes and Namespaces

## Arrays

### Array Iteration and Properties

### The `Array` Constructor

## Types

### Equality and Comparisons

### The `typeof` Operator

The `typeof` operator (together with `instanceof`) is probably the biggest design flaw of JavaScript, as it is almost *completely broken*.

Although `instanceof` still has limited uses, `typeof` really has only one practical use case, which does *not* happen to be checking the type of an object.

#### The Class of an Object

The specification gives exactly one way of accessing the `[[Class]]` value, with the use of `Object.prototype.toString`.

    function is(type, obj) {
        var clas = Object.prototype.toString.call(obj).slice(8, -1);
        return obj !== undefined && obj !== null && clas === type;
    }

    is('String', 'test'); // true
    is('String', new String('test')); // true

In the above example, `Object.prototype.toString` gets called with the value of this being set to the object whose `[[Class]]` value should be retrieved.

### The `instanceof` Operator

### Type Casting

## Core

### Why Not to Use `eval`

### `undefined` and `null`

### Automatic Semicolon Insertion

### The `delete` Operator

## Other

## Useful Code Snippets

### Initialization

Use function block to avoid global variables.

    (function(window, document, $, undefined) {
        // insert code here
    })(this, document, jQuery);

### Replacement for setInterval()

    (function loops() {
        doStuff();

        $("#update").load("abc.php", function() {
            loops();
        });

        setTimeout(loops, 100);
    })();


## Array

### Empty array

[Emptying an array](http://jsperf.com/emptying-arrays)

    arr.length = 0;

### Remove items in array

    var arr = [1, 2, 3, 4, 5];
    var selectedIndices = [0, 2, 4];

    // walk arrays backwards to avoid skipping elements on delete
    for (var j = selectedIndices.length - 1; j >= 0; j--) {
        var selectedIndex = selectedIndices[j];
        arr.splice(selectedIndex, 1);
    }


### Array.reduce

Apply a function against an accumulator and each value of the array (from left to right) as to reduce it to a single value.

Syntax: `array.reduce(callback[, initialValue])`

Example:

    var result = [1, 2, 3, 4].reduce(function(previousValue, currentValue, index, array) {
        return previousValue + currentValue;
    });
    console.log(result); // 10

### jQuery.merge

    var arr1 = [1, 2, 3];
    jQuery.merge(arr1, [4, 5]);
    console.log(arr1); // [1, 2, 3, 4, 5]

### jQuery.makeArray

    jQuery.makeArray("a"); // ["a"]
    jQuery.makeArray(["a"]); // ["a"]

## Object

### Equality

Underscore:

    _.isEqual(object, other)

[Object.identical.js](https://github.com/prettycode/Object.identical.js)


## Questions

_Q: How do you implement an extend function that takes an object and extends it with new properties? Basically, duplicating a jQuery extend._

_Q: What is the concept of "functions as objects" and how does this affect variable scope?_

_Q: What modern JavaScript frameworks and utilities excite you right now from an approach and code point of view, even if they're not yet stable enough for client work?_

> I am more concerned with knowing that they keep up to date on the latest thinking around JavaScript.
> 
> I am also concerned about the flood of "copy-and-paste" JavaScript solutions.
> 
> jQuery and its plug-in system are so popular that many developers only know JavaScript in that context, and have trouble understanding how to create new functionality. While this is fine for many websites, which only need a dynamic menu or homepage carousel, as the emerging web becomes more "stateful" – (he points to USA Today's redesign as an example of pages that users navigate without loading a new page) – this knowledge becomes crucial to developing robust and maintainable applications.

_Q: What is the different between `.call()` and `.apply()`?_

_Q: Can you explain how inheritance works in JavaScript?_

JavaScript has a somewhat unique inheritance model and a good understanding of it is crucial to using JavaScript in larger applications.

> We are looking for the applicant to discuss not only prototypes, and how that affects inheritance, but in what ways this can be more flexible than classical inheritance models seen in Java and C#.

_Q: What is event bubbling in the DOM?_

_Q: Difference between `window.onload` and `onDocumentReady`?_

The `onload` event does not fire until every last piece of the page is loaded, this includes CSS and images, which means there's a huge delay before any code is executed.
That isn't what we want. We just want to wait until the DOM is loaded and is able to be manipulated. `onDocumentReady` allows the programmer to do that.

_Q: What is the difference between `==` and `===` ?_

The `==` checks for value equality, but `===` checks for both type and value.

_Q: What is the difference between undefined value and null value?_

`undefined` means a variable has been declared but has not yet been assigned a value. On the other hand, `null` is an assignment value. It can be assigned to a variable as a representation of no value.

Also, `undefined` and `null` are two distinct types: `undefined` is a type itself (undefined) while `null` is an object.

Unassigned variables are initialized by JavaScript with a default value of undefined. JavaScript never sets a value to `null`. That must be done programmatically.

_Q: What are JavaScript closures? When would you use them?_

Two one sentence summaries:

* a closure is the local variables for a function – kept alive after the function has returned, or
* a closure is a stack-frame which is not deallocated when the function returns.

A closure takes place when a function creates an environment that binds local variables to it in such a way that they are kept alive after the function has returned. A closure is a special kind of object that combines two things: a function, and any local variables that were in-scope at the time that the closure was created.

The following code returns a reference to a function:

    function sayHello2(name) {
        var text = "Hello " + name; // local variable
        var sayAlert = function() { alert(text); };
        return sayAlert;
    }

Closures reduce the need to pass state around the application. The inner function has access to the variables in the outer function so there is no need to store the information somewhere that the inner function can get it.

This is important when the inner function will be called after the outer function has exited. The most common example of this is when the inner function is being used to handle an event. In this case you get no control over the arguments that are passed to the function so using a closure to keep track of state can be very convenient.

_Q: What is unobtrusive JavaScript? How to add behavior to an element using JavaScript?_

Unobtrusive JavaScript refers to the argument that the purpose of markup is to describe a document's structure, not its programmatic behavior and that combining the two negatively impacts a site's maintainability. Inline event handlers are harder to use and maintain, when one needs to set several events on a single element or when one is using event delegation.

_Q: What is JavaScript namespacing? How and where is it used?_

Using global variables in JavaScript is evil and a bad practice. That being said, namespacing is used to bundle up all your functionality using a unique name. In JavaScript, a namespace is really just an object that you've attached all further methods, properties and objects. It promotes modularity and code reuse in the application.

_Q: What is the difference between `innerHTML` and `append()` in JavaScript?_

InnerHTML is not standard, and it's a String. The DOM is not, and although innerHTML is faster and less verbose, its better to use the DOM methods like `appendChild()`, `firstChild.nodeValue`, etc. to alter innerHTML content.

_Q: Are objects passed by value or by reference? Does the type of object matter?_

_Q: What does it mean to chain functions in jQuery?_

_Q: How do JavaScript timers work? What is a drawback of JavaScript timers?_

Timers allow you to execute code at a set time or repeatedly using an interval. This is accomplished with the `setTimeout`, `setInterval`, and `clearInterval` functions. The `setTimeout(function, delay)` function initiates a timer that calls a specific function after the delay; it returns an id value that can be used to access it later. The `setInterval(function, delay)` function is similar to the `setTimeout` function except that it executes repeatedly on the delay and only stops when cancelled. The `clearInterval(id)` function is used to stop a timer. Timers can be tricky to use since they operate within a single thread, thus events queue up waiting to execute.

_Q: How do you organize your JavaScript code?_

The key concept here is to get an idea of how the candidate maintains and designs code. Do they design code that is specific to an application with no possible reuse? Do they use class inheritance or the module pattern to build reusable code? These approaches allow multiple developers to work on a project without stepping on their coworkers' toes. In addition, testing modular code or classes is easier to approach than a jumbled mess of code thrown together (look around the Web, and you’ll find plenty of examples).

