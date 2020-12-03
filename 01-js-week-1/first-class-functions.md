# Functions are First-Class

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=44656559-a879-47d2-9430-ac8500414bae&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

- Understand that first-class/higher-order functions allow us to attach functions to objects
- Practice creating objects that have functions as members
- Understand that first-class/higher-order functions allow us to use functions as objects
- Practice passing functions as arguments in other functions

## We Can Attach A Function to Objects

Recall our brief introductions to objects in JavaScript; objects are name/value pairs that can hold other pieces of data, including other objects.

```javascript
const testObj = {
  someNum: 5,
  someStr: 'this is a test string',
  someNestedObj: {
    someOtherNum: 4,
  }
};
```

We will be applying this idea of an object to much more realistic use-cases of organizing data:

```javascript
const task = {
  name: 'practice iteration in JavaScript',
  dueDate: 'end of the week',
  owner: 'simon',
  isComplete: false
}
```

And we access _members_ of this JavaScript object with bracket or dot notation:

```javascript
task.owner;
task.isComplete;
```

We can attach _behavior_ to an object by making it a member, using this syntax:

```javascript
const task = {
  name: 'practice iteration in JavaScript',
  dueDate: 'end of the week',
  owner: 'simon',
  isComplete: false,
  markComplete() {
    console.log('Wow...');
    console.log('This task is complete!');
    console.log('Congratulations! You won!');
  },
}
```

We have given the object `task` the **method** `markComplete()` by:
- continuing to comma-separate it on the same level as the other members of the object
- not following the `name: value` pattern
- giving it the name `markComplete` and with the `() { ... }` syntax
    - Note: The syntax _inside_ the function is the same as regular JavaScript syntax-- nothing special here, still semi-colons and all
    - If I need to add something after the `markComplete()` function inside the `task` object, I'll need to continue to comma-separate

Now, with `markComplete()` defined, we can call this behavior off of `task` with the following syntax:

```javascript
task.markComplete();
```

### A Function Accesses Other Members With `this`

Our new `task` object with the `markComplete()` behavior is cool, but doesn't make sense. Our next step is for the `task` object's value of `isComplete` to change from `false` to `true`. But how do we access the other member of the object?

Within an object itself, other members (such as properties) can be accessed through the `this` keyword, similar to Ruby's `self`.

```javascript
const task = {
  name: 'practice iteration in JavaScript',
  dueDate: 'end of the week',
  owner: 'simon',
  isComplete: false,
  markComplete() {
    console.log('Wow...');
    console.log(`The task "${this.name}" is complete!`);
    console.log('Congratulations! You won!');
    this.isComplete = true;
    return true;
  },
}

console.log(task.isComplete);
task.markComplete();
console.log(task.isComplete);
```

#### Exercise: Write More Behavior for the `task` Object
<!--BEGIN CHALLENGE-->

### !challenge

* type: local-snippet
* language: javascript
* id: 4aa93a1e-2313-4401-a479-6d3eeb0ad4cf
* title: Code Challenge
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

Given this base code for an object named `task`, make another method on it:

1. Name the method `describe`
2. The method should print out the text `"The task name is"` and then the task name
3. Then it should print out the text `"The task owner is"` and then the task owner
4. It should return `true` (Why? Just to practice returning things.)
5. At the end of the script, call the method with `task.describe();` and verify

##### !end-question

##### !placeholder

```js
  const task = {
    name: 'practice iteration in JavaScript',
    dueDate: 'end of the week',
    owner: 'simon',
    isComplete: false,
    markComplete() {
      console.log('Wow...');
      console.log(`The task "${this.name}" is complete!`);
      console.log('Congratulations! You won!');
      this.isComplete = true;
      return true;
    },
    // your code here, then call the new method
  }
```

##### !end-placeholder

##### !tests

```js

/**
 * Blatantly stolen from Jest (I hate mocha/chai with an irrational passion).
 * 
 * This basically lets me mock a function (console.log) so I can see what they printed
 * and how many times they did so.
 * 
 * @param impl - What the real function is supposed to do.
 */
function fn (impl = () => { }) {
  const mockFn = function (...args) {
    mockFn.mock.calls.push(args);
    mockFn.mock.instances.push(this);
    try {
      const value = impl.apply(this, args); // call impl, passing the right this

      mockFn.mock.results.push({ type: 'return', value });
      return value; // return the value
    } catch (value) {
      mockFn.mock.results.push({ type: 'throw', value });
      throw value; // re-throw the error
    }
  }

  mockFn.mock = { calls: [], instances: [], results: [] };
  return mockFn;
}

describe('describe', () => {
  let oldConsoleLog = console.log;

  // Mock console.log
  beforeEach(() => {
    console.log = fn();
  });

  // restore console.log
  afterEach(() => {
    console.log = oldConsoleLog;
  });

  it('returns true', () => {
    const answer = task.describe();
    expect(answer).to.be.equal(true);
  });

  it('prints the strings requested, capitalization and spaces correct', () => {
    const answer = task.describe();

    expect(console.log.mock.calls[0][0]).to.equal(`The task name is ${ task.name }`);
    expect(console.log.mock.calls[1][0]).to.equal(`The task owner is ${ task.owner }`);
  });
});

  ```

##### !end-tests

<!--optional-->
##### !hint
``` javascript
const task = {
    name: 'practice iteration in JavaScript',
    dueDate: 'end of the week',
    owner: 'simon',
    isComplete: false,
    markComplete() {
      console.log('Wow...');
      console.log(`The task "${this.name}" is complete!`);
      console.log('Congratulations! You won!');
      this.isComplete = true;
      return true;
    },
    describe() {
      console.log(`The task name is ${this.name}`);
      console.log(`The task owner is ${this.owner}`);
      return true;
    }
  }

  task.describe();
```
##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->

Is there bonus time? If there is, add a new member named `daysExtended` with a value of `0`. Then, add a new member that is a function named `extendDueDate`. The function `extendDueDate` takes in one parameter: a number of days to increment `daysExtended` by.

#### Notable Things About Syntax

   style="max-width: 700px; margin: auto;">

  <summary>
    As with much of JavaScript, there's two versions of the syntax to define a function inside an object. Click here to expand and view the old (pre-2015) syntax.
  </summary>

  ```javascript
  // Old syntax for defining a function inside an object
  const animal = {
    // ...
    describe: function() {
      console.log(`A ${this.species} goes ${this.sound}`);
    }
  };
  ```

  It's just different enough to trip you up if you see it on Stack Overflow. In this course we'll be using the new-style syntax (the first example).

</details>
<br/>

Be aware that JavaScript's `this` keyword has some strange behavior. Many times it won't refer to quite what you'd expect. This can be one of the most frustrating things about JavaScript, especially for a beginner, and we'll have more to say about it later. For now, just know that it's a thing that might come up.

## We Can Pass Functions as Arguments

Remember how functions can take in arguments? We can define parameters, which is our way of defining inputs. Those arguments can be numbers, strings, other objects, and so on. We can read them, modify them, and return them as output.

In JavaScript, functions are objects. That means **you can pass functions as arguments to _other functions_.**

Let's look at the following example:

We are defining two functions:
1. A function named `doMath` whose responsibility is to do some generic math operation 10 times, with the numbers 0 through 9
1. A function named `doubleNum` whose responsibility is to represent a specific math operation: doubling a number

`doubleNum` is written so that it takes in a number as an argument. For any given input number, it will double it and return that value.

`doMath` is written so that it takes in a function as an argument. This function it takes in will be the generic math operation. No matter what the generic math operation function is, it will do that operation 10 times, with the numbers 0 through 9.

```javascript
const doMath = function(operation) {
  for (let i = 0; i < 10; i += 1) {
    const result = operation(i);
    console.log(`${i}: ${result}`);
  }
};

const doubleNum = function(num) {
  return num * 2;
};

doMath(doubleNum);
```

Answer the following questions:
<!--BEGIN CHALLENGE-->

### !challenge

* type: short-answer
* id: 54f29def-b5d1-4908-a0b0-8123e39f44e6
* title: Short Answer
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

For the `doubleNum` function, how many parameters does it take in, what are the names of the parameters, and what data type are we expecting for each parameters?

##### !end-question

##### !answer

/.+/

##### !end-answer

##### !placeholder

Your answer here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

1 parameter named `num` that is a number

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: short-answer
* id: 897b4824-f16d-42f7-b3a1-82609b7f1705
* title: Short Answer
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

For the `doMath` function, how many parameters does it take in, what are the names of the parameters, and what data type are we expecting for each parameters?

##### !end-question

##### !answer

/.+/

##### !end-answer

##### !placeholder

Your answer here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

1 parameter named `operation` that is a function

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: short-answer
* id: 972e4dd0-f5c8-4539-8d17-f92195421ccc
* title: Short Answer
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

What line _invokes_ the `doMath` function? What do we pass in as an argument? What data type is that argument?

##### !end-question

##### !answer

/.+/

##### !end-answer

##### !placeholder

Your answer here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

`doMath(doubleNum)`. We pass in the `doubleNum` function as an argument.

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: short-answer
* id: 5ba5c8b3-6ea5-4c3a-a3a9-fe1ba8f31c0b
* title: Short Answer
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

In the `doMath` function, how do we use the variable `operation`?

##### !end-question

##### !answer

/.+/

##### !end-answer

##### !placeholder

Your answer here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

Because `operation` is a function, we _invoke_ the `operation` function with `let result = operation(i);`

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: short-answer
* id: 4dcc9ac6-a9b5-45b8-a277-a7e7d2efea34
* title: Predict the Output
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

What is the output of the code?

##### !end-question

##### !answer

/.+/

##### !end-answer

##### !placeholder

Your output here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

```
0: 0
1: 2
2: 4
3: 6
4: 8
5: 10
6: 12
7: 14
8: 16
9: 18
```

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->

A function that is passed as an argument is often referred to as a _callback function_, or sometimes just a _callback_.

In this case, we can colloquially refer to the variable `operation` as a callback function.

## Summary

Objects can have functions in them. Within an object, we can reference other members of the object with `this`. `this` will end up being a very complex subject; for now, our one use of `this` will be in this context!


A programming language that allows you to pass functions around like this is said to support _higher order_ or _first-class_ functions. C, JavaScript and Python are examples of languages that support first-class functions; Ruby and Java are examples of languages that do not.