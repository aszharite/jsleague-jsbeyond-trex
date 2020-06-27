# JS Beyond the Basics (Game Edition)

Throught this guide, we are going to be referencing and going back to the source code as the scope of this workshop is to understand javascript concepts that are a bit more advanced by looking at the popular game that Google Chrome throws to keep us busy in the dire time when internet is down.

When we see a reference in the form of `L200`, this means that we can find the example at line 200 in the source code, which will be referencing the `dist/index.js` unless specified otherwise. 

I would like to give special thanks to Google for not being border to death at work when we didn't have internet.

There are a lot of developers that have tweaked the game over the years but today we are going to use [Wayou](https://github.com/wayou)'s version of the TRex runner as it is closer to the Chromium implementation of it.

## Types and coercion

### Data types

We talked about types and the two major categories in javascript: `primitives` and `objects` and let see a bit how they are used in our game.

Looking at the `primitives` first, we are going to see a heavy use of primitives throught for configurations, a lot of identifiers for events and state. We can see this at `L105` to `L228` best when we are configuring the `Runner` class.

Everything else is an `object` in js. This means even `functions` and the most simplest way to check this is to look at the instance of `Runner` for example.

If we look at `L14` we can see that `Runner` is declared as a function, so what we can do in the console is:

```javascript 
Runner instanceof Function
```

and this should show us that indeed, `Runner` is a function. But what is more interesting is that we can check the instance of the `Function`

```javascript
Function instanceof Object
```

and this is going to confirm that indeed, functions are objects in javascript.

### Type coercion

In the app we are `implicitly` coercing types mostly when we want to concatenate strings that we use for css purposes.

It can either be a class that we need (`L351`, `L959`) or it can be css values (`L440`) and interestingly enough, even animations (`L466`).

`Explicit` coercion is loosly used in the app as we only do some small conversion to fetch and reuse some css value in `L421`.

### Loose vs. Strict Equality

So the main reason for using `loose` and `strict` equality is to avoid side effects from false possitives that might occure because of type coercion.

We can see a lot of `loose` checking when comparing events (`L674`, `L715`) and `strict` when checking for values and trying to aviod false positives (`L590`)

## Scope and the "this" keyword

Scope is very interesting in javascript as it changes lightning fast depending on the context. 

Let's look at the scope from 3 perspectives:

1. Let's go to the console and just check out what `this` referrences.

2. Next, let's put a breakpoint inside the `init` function of the `Cloud` and check what `this` has become now.

3. The last type of scope we can't really see in our application but the example that I like to give the most is the `for...of` loop.

```javascript
  const values = [1,2,3,4,5];

  // using let
  for(let value of values) {
    console.log(`value in step of loop: ${value}`);
  }
  console.log(`final value: ${value}`);
```

### Exercise time!!!

Once we have game over, the user needs to start again. This can be easily done by left clicking on the canvas. At `L746` we have the function `isLeftClickOnCanvas` that helps achieve this but it's incomplete. Let's help finish it!

<details>
  <summary>Click here for solution</summary>

  ```javascript
  /**
   * Returns whether the event was a left click on canvas.
   * On Windows right click is registered as a click.
   * @param {Event} e
   * @return {boolean}
   */
  isLeftClickOnCanvas: function (e) {
      return e.button != null && e.button < 2 &&
          e.type == Runner.events.MOUSEUP && e.target == this.canvas;
  },
  ```
</details>

## Closures

### Excercise!!

Unfortunately closures are the 2nd feature that we can't see in our game, but I have a fun exercise that we can do. When recruting developers I like to give a problem that states closures best:

`Write the sum of numbers as a closure. For testing purposes you can use sum(3)(2) that should yield the result 5.`

## Objects and prototypes

Earlier we talked about how functions are objects and that has been the foundation for javascript for a long time. Before ES6 and Classes we had prototypes and we can see it is the foundation of the TRex Runner game.

Let's take a look at how prototypes are used and defined in the game.

## Functional Programming

For this step I challenge you to find pure functions in the game.

## Challenge (accept it!)

### Fullscreen

Games are more fun when they are played in fullscreen. What we can do is start the game as a fullscreen to enjoy it to the fullest.

As an example we can see [chrome://dino/](chrome://dino/).

### Dark mode

One of the more popular features that UI has seen in the coming years was the adaptation to `Dark Mode` and the game itself has it in the form of `NightMode`. 

The challenge is to first, enable it and then try to adapt it so that when it's night outside, you play in `NightMode`.
