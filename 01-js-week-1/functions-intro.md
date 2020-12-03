# Intro to Functions!

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=35e061a2-f926-4515-a3f8-ab8d014bd70e&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

- Learn and practice the syntax for defining and calling/invoking functions in JavaScript
- Learn and practice the syntax for using functions that have parameters
- Understand that JavaScript requires explicit `return` calls

## Functions in JavaScript are like Methods in Ruby

In JavaScript, we can use functions to define reusable behavior.

This should _feel_ similar to methods in Ruby. They're not the same, but we can get into those details later. For now, we'll use functions to name and structure sections of code.

Either way, the syntax for functions is a lot different in JavaScript than in Ruby.

## Functions Are Objects, So We Assign Variables to Them

### Declare

All functions in JavaScript are objects. For now, what that means to us is that we will make sure that variables hold onto these functions. You declare functions with the `let` or `const` keywords and a name.

### Assign

On the right-hand side of the assignment operator, you set the value to be a function, with the `function` keyword.

Let's make a function named `bark`, whose responsibility is to print to the terminal the sound a dog makes.

How do we do that? Let's declare a `const` variable named `bark`, and set its value to the function named `bark`. After we start the function with the words `function()`, we open up a block of code with curly braces, and put the inners of the function within the `{}`.

```javascript
const bark = function() {
  console.log('Woof!');
};
```

Open the `node` REPL and copy-and-paste in the following expressions. What do you get?

1.
    ```javascript
    const bark = function() {
      console.log('Woof!');
    };
    ```
1. `bark;`

<details style="max-width: 700px; margin: auto;">

  <summary>
    Compare your answers here
  </summary>

  1. `undefined`
  1. `[Function: bark]`
</details>

### Calling a Function

We've defined a function, so how do we call it?

Unlike in Ruby, JavaScript requires you to type in parentheses if you want to invoke a function:

```javascript
bark();
```

### The Finer Details About Defining Functions

When we defined the function, we gave it the variable keyword `const`. We could have used `let`, but in general, we don't need any variable named `bark` to be reassigned. Because we don't need `bark` to ever be reassigned, it makes sense to make it a constant.

### Exercise: Make An Animal Noise Function


<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: javascript
* id: 27a13d71-519f-4005-ba8c-408ed32e12e4
* title: Animal Noises!
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

Given the `bark` function as a model:

Create a script that does the following:

1. Create a `ribbit` function that prints a frog noise to the terminal
1. Call the `ribbit` function
1. Create an `oink` function that prints a pig noise to the terminal
1. Call the `oink` function
1. Create a third function that prints an animal noise to the terminal
1. Call that function 5 times!

##### !end-question

##### !placeholder

```js
const bark = function() {
  console.log('Woof!');
};
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

describe('testFunction', () => {
  let oldConsoleLog = console.log;

  // Mock console.log
  beforeEach(() => {
    console.log = fn();
  });

  // restore console.log
  afterEach(() => {
    console.log = oldConsoleLog;
  });

  it('ribbit() prints "Ribbit!" and oink() prints "Oink!"', () => {
    ribbit();
    oink();

    expect(console.log.mock.calls[0][0]).to.equal(`Ribbit!`);
    expect(console.log.mock.calls[1][0]).to.equal(`Oink!`);
  });
});

```

##### !end-tests

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Functions Can Have Parameters

Functions that can take in parameters are very similar to how parameters for methods work in Ruby. To define that a specific function takes in an argument, we define the name of that parameter when we define the function.

Observe the example below, which defines a function named `sayItTwice`. Its responsibility is to take in some input, and then print it to the console twice.

It takes in one argument named `text`. We can use `text` as a local variable within the function.

```javascript
const sayItTwice = function(text) {
  console.log(text);
  console.log(text);
};
```

When we invoke the function `sayItTwice`, we pass in an argument in the parentheses:

```javascript
sayItTwice('JS is OK!');
```

We can define a function with multiple parameters by comma-separating them:

```javascript
const sayCompoundWord = function(prefix, suffix) {
  console.log(`${prefix}-${suffix}`);
}

sayCompoundWord("jean", "shorts");
```

## JavaScript Requires Explicit `return`s

Ruby had something called the _implicit_ return, and our best practice was to always explicitly return something with the `return` keyword.

Functions in JavaScript can return things too using the `return` keyword. We'll be using `return` a lot in JavaScript still!

However, **JavaScript requires explicit `return` statements.** If you need to return something out of a function, you must explicitly say `return`.

Open the `node` REPL and copy-and-paste in the following expressions. What do you get?

1.
    ```javascript
    const meow = function() {
      return 'mmMMMME-OW!';
    }
    ```
1. `let catNoise;`
1. `meow();`
1. `catNoise;`
1. `catNoise = meow();`
1. `catNoise;`

<details style="max-width: 700px; margin: auto;">

  <summary>
    Compare your answers here
  </summary>

  1. `undefined`
  1. `undefined`
  1. `'mmMMMME-OW!'`
  1. `undefined`
  1. `'mmMMMME-OW!'`
  1. `'mmMMMME-OW!'`
</details>


## Exercise: Make Calculator Functions

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: javascript
* id: c06055a9-5d82-4aa9-beaf-bc4cbc636c12
* title: Calculator kick-starter!
* points: 1 
* topics: javascript, js-functions

##### !question

Create a script that does the following:

1. Create a `addNums` function that takes in two parameters (`a` and `b` are decent variable names here).
    - It prints out `"The value of a is: ${a}"`
    - It prints out `"The value of b is: ${b}"`
    - It `return`s the two parameters added together
1. Outside of the function, create a `const` variable named `sum` and set it to equal the result of `addNums(3, 5);`
1. After that, print the variable `sum` with the line `console.log(sum);`. Run the script to confirm it runs, and runs as expected.
1. Create a `subtractNums` function that takes in two parameters.
    - It prints out `"The value of a is: ${a}"`
    - It prints out `"The value of b is: ${b}"`
    - It `return`s the result of `a - b`
1. Outside of the function, create a `const` variable named `difference` and set it to equal the result of `subtractNums(3, 5);`
1. After that, print the variable `difference` with the line `console.log(difference);`. Run the script to confirm it runs, and runs as expected.
1. Create a `multiplyNums` function that takes in two parameters.
    - It prints out `"The value of a is: ${a}"`
    - It prints out `"The value of b is: ${b}"`
    - It `return`s the result of a and b multiplied together
1. Outside of the function, create a `const` variable named `product` and set it to equal the result of `multiplyNums(3, 5);`
1. After that, print the variable `product`
1. Run the script to confirm it runs, and runs as expected


##### !end-question

##### !placeholder

```js

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

describe('testFunction', () => {
  let oldConsoleLog = console.log;

  // Mock console.log
  beforeEach(() => {
    console.log = fn();
  });

  // restore console.log
  afterEach(() => {
    console.log = oldConsoleLog;
  });

  it('prints the strings requested, capitalization and spaces correct', () => {
    console.log(addNums(3, 5));
    console.log(subtractNums(3, 5));
    console.log(multiplyNums(3, 5));

    expect(console.log.mock.calls[0][0]).to.equal("The value of a is: 3");
    expect(console.log.mock.calls[1][0]).to.equal("The value of b is: 5");
    expect(console.log.mock.calls[2][0]).to.equal(8);
    expect(console.log.mock.calls[3][0]).to.equal("The value of a is: 3");
    expect(console.log.mock.calls[4][0]).to.equal("The value of b is: 5");
    expect(console.log.mock.calls[5][0]).to.equal(-2);
    expect(console.log.mock.calls[6][0]).to.equal("The value of a is: 3");
    expect(console.log.mock.calls[7][0]).to.equal("The value of b is: 5");
    expect(console.log.mock.calls[8][0]).to.equal(15);
  });
});

```

##### !end-tests

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->





Once you've completed the exercise above, let's DRY up the code a little!

1. Create a `printInputs` that takes in two parameters. It prints out `"The value of a is: ${a}"`. It prints out `"The value of b is: ${b}"`. It returns `null`.
1. Refactor the `addNums`, `subtractNums`, and `multiplyNums` functions to call `printInputs()` inside of it.
1. Delete any redundant code!

If you've done it correctly, the tests should still pass and there will be significantly less redundant code :D

## Additional Resources
* [MDN on Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
