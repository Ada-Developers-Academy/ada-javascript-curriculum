# Arrow Functions: as Anonymous Functions, and `this`

## Learning Goals

By the end of this lesson we will be able to...

- Recognize using arrow functions as anonymous functions
- Practice refactoring anonymous functions as arrow functions
- Explain how `this` works in an arrow function

## Arrow Functions as Anonymous Functions

Arrow functions work well with collection functions like `map`, `select`, and `sort`.

```javascript
let numbers = [3, 4, 5, 6];

let doubled = numbers.map(function(num) {
  return num + num;  
});

// as an arrow function

let doubled = numbers.map(num => num + num);
```

In the above example we map an array to one where each element is doubled.  Looking at the two examples the arrow function, once you adjust to the new syntax, is more compact and visually conveys the concept that we're mapping each number (`num`) to twice it's value.

## Arrow functions do not have their own `this`

There are additional benefits to using arrow functions beyond minimized syntax.  

### Traditionally, `this` is an Interesting Problem

```javascript
const numberHaver = {
  value: 0,
  increment() {
    [1,2,3].forEach(function(num) {
      this.value += num;
    });
  }
}

console.log(numberHaver.value); // 0
numberHaver.increment();
console.log(numberHaver.value); // Expected 6, but prints 0
```

The code above is **supposed** to add each element of the array and store the result in `value`, but...anonymous functions written this way don't preserve the context they are within. Because of that, a reference to `this` will not be referring to the object we want. (If we do some debugging, we learn it will be the "global object".)

The traditional work-around to this situation is to save the context (`this`) into another variable and use that variable instead of `this`.

```javascript
const numberHaver = {
  value: 0,
  increment() {
    const that = this;
    [1,2,3].forEach(function(num) {
      that.value += num;
    });
  }
}

console.log(numberHaver.value); // 0
numberHaver.increment();
console.log(numberHaver.value); // Expected 6, and prints 6
```

Notice the line `let that = this;`  saving the current context in `that` allows the anonymous function to access `value` without the confusion surrounding `this`. Whew!  What a work-around!

### Arrow Functions Inherit `this`

**Arrow functions do not have their own `this` context**, instead they inherit `this` from the surrounding block.  So using an arrow function makes the resulting code less confusing and error-prone.

```javascript
const numberHaver = {
  value: 0,
  increment() {
    [1, 2, 3].forEach((num) => {
      this.value += num;
    });
  },
};

console.log(numberHaver.value); // 0
numberHaver.increment();
console.log(numberHaver.value); // Expected 6, and prints 6
```

Because arrow functions do not have their own context (`this`), they make excellent anonymous callback functions.  

## Places **Not** To Use Arrow Functions

Arrow functions are great for callbacks, and are great shortcuts for regular functions, but there are a couple of places you don't want to use them.

### As Methods Inside Objects

Arrow functions make poor methods for objects.  Because they do not contain a reference to `this`, you cannot access an object's instance variables.

```javascript
let fido = {
  name: 'Fido',
  age: 3,
  toString: () => {
    return `${this.name} is ${this.age} years old`; // error!
  },
};
```

The above example will return 'undefined is undefined years old' because the toString method doesn't have a `this` reference.

### As Constructors for Prototype-based Objects

We haven't closely looked at what prototype-based objects are in JavaScript, and it's likely we won't. However, for the sake of thoroughness, it's good to know that arrow functions do not work well with prototype-based objects. An Arrow function will give you an error if you use it as a constructor.  **Why?**  What does the example below use, that arrow functions don't have?

```javascript
const Dog = (name, age) => {
  this.name = name;
  this.age = age;
};

let fido = new Dog('Fido', 3); // <-- TypeError!
```

**Answer:** `this!` We know that arrow functions take the value of this from the context in which they are defined. Since our constructor is defined outside any other object, `this` doesn't make any sense, and our code does the wrong thing.  Further, arrow functions do not have a **prototype** attribute, so `Dog.prototype` will generate an error.
## Learning Comprehension

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: javascript
* id: 46a96161-fcfe-4b64-9c5c-f32f37613188
* title: [text, a short question title]
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
* topics: javascript, arrow-functions

##### !question

Refactor the following to use an Arrow function.  It already passes the tests, but make it do so using an arrow function.

##### !end-question

##### !placeholder


```js
// notes on what to return, etc

function getLengths(words) {
  return words.map(function (word) {
    return word.length;
  });
}
```

##### !end-placeholder

##### !tests

```js
describe('getLengths', () => {

  it("returns [3, 4, 5] for ['bob', 'jane', 'alice']", () => {
    // Act
    const answer = getLengths(['bob', 'jane', 'alice']);
    expect(answer, "must be an array").to.be.an('array');
    expect(answer, 'must equal [3, 4, 5]').to.equal([3, 4, 5]);
  });

  it('returns [] for []', () => {
    const answer = getLengths([]);
    expect(answer, "must be an array").to.be.an('array');
    expect(answer, 'must equal []').to.equal([]);
  });

  it('returns [3] for [\'ada\']', () => {
    const answer = getLengths(['ada']);
    expect(answer, "must be an array").to.be.an('array');
    expect(answer, 'must equal [3]').to.equal([3]);
  });
})
```

##### !end-tests

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 102fc788-8783-4096-8f58-90cfa2bfda80
* title: Differences between normal and arrow functions
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
* topics: javascript, arrow-functions

##### !question

The difference between arrow functions and normal functions is that...

##### !end-question

##### !options

* **Only** arrow functions have a `this` keyword.
* Arrow functions do **not** have a `this` context.
* Arrow functions **cannot** take parameters.
* Arrow functions **cannot** return a value.

##### !end-options

##### !answer

* Arrow functions do **not** have a `this` context.

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

**Arrow functions do not have their own `this` context**, instead they inherit `this` from the surrounding block.  So using an arrow function makes the resulting code less confusing and error-prone.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 3c48887b-7c34-40b7-be13-9e0b36a28b5b
* title: Good place to use an arrow function
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
* topics: javascript, arrow-functions

##### !question

What is a good place to use an arrow function?

##### !end-question

##### !options

* As a member method of an object
* As a constructor
* As a callback function

##### !end-options

##### !answer

* As a callback function

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

Because an arrow function takes it's `this` from the block within which it's defined, it doesn't make a good choice for a member method of an object or a constructor.  Instead it's most useful as a callback function.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Summary

Arrow functions are a great way to minimize your JavaScript typing and make very good anonymous callback functions.

However they lack a `this` context, making them useful as callback functions, but unsuitable for constructors or as object methods.  

On older browsers, newer features like Arrow Functions, template strings, etc, will not work. Older browsers require a tool, like Babel, to convert newer (ES6) code to older JavaScript

## Additional Resources

- [MDN Docs on Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Learning ES6 Arrow Functions](https://www.eventbrite.com/engineering/learning-es6-arrow-functions/)
