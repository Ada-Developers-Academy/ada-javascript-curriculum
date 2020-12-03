# Ruby to JavaScript Worksheet
Read the code in each section, then write the equivalent JavaScript code for the Ruby that is given. Start by writing it out in a text editor or on a piece of paper. Then try running it and tweak your code until it successfully runs with expected output.

Each problem stands alone. Variables from previous problems do not exist.

## Problem Set

### !challenge

* type: code-snippet
* language: javascript
* id: 10c8b04b-6428-42d9-88cc-f405c8206306
* title: Problem 1
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

Convert the following ruby code into JavaScript using the input box below.

```ruby
ada_age = 2

if person_age < ada_age
    print "This person is younger"
elsif ada_age < person_age
    print "Ada is younger"
else
    print "They’re the same!"
end
```

##### !end-question

##### !placeholder

```js
function ageChecker(personAge) {// DO NOT EDIT THIS CODE
  //Paste your code here


}//DO NOT EDIT THIS ONE EITHER
```

##### !end-placeholder

##### !tests

```js
/**
 * Chris doesn't like this testing format and I don't know it well enough to ignore him!
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

describe('ageChecker', () => {
  let oldConsoleLog = console.log;
  
  // Mock console.log
  beforeEach(() => {
    console.log = fn();
  });
  
  // restore console.log
  afterEach(() => {
    console.log = oldConsoleLog;
  });

  it("Prints correctly for older person (person_age = 35)", () => {
    ageChecker(35);
    expect(console.log.mock.calls.length).to.equal(1);
    expect(console.log.mock.calls[0][0]).to.equal("Ada is younger");
  });
  it("Prints correctly for younger person (person_age = 0)", () => {
    ageChecker(0);
    expect(console.log.mock.calls.length).to.equal(1);
    expect(console.log.mock.calls[0][0]).to.equal("This person is younger");
  });
  it("Prints correctly for same age person (person_age = 2)", () => {
    ageChecker(2);
    expect(console.log.mock.calls.length).to.equal(1);
    expect(console.log.mock.calls[0][0]).to.equal("They’re the same!");
  });
});
```

##### !end-tests

<!-- other optional sections -->
##### !hint
Make sure that your code uses the correct capitalization and punctuation! 
##### !end-hint
##### !hint
We are going to be providing a variable called `personAge` by calling the function! Don't edit this variable!
##### !end-hint
##### !hint
Copy the text of your code, and then hit the button to reset the window! You might have deleted something important.
##### !end-hint  
##### !hint
Here is our solution!
```javascript
const adaAge = 2

if (personAge < adaAge) {
  console.log("This person is younger")
}
else if (adaAge < personAge) {
  console.log("Ada is younger")
}
else {
  console.log("They’re the same!")
}
``` 
##### !end-hint
### !end-challenge

1. Ruby


    <!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: javascript
* id: 5f521652-b4e5-456a-a437-12c9717fb7e0
* title: Problem 2
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

Convert the following ruby code to javascript

```ruby
if x > y || x == y
    if x > y
      print "x is bigger"
    else
      print "x = y"
    end
else
    print "y is bigger"
end
```

##### !end-question

##### !placeholder

```js
function comparisonPractice(x,y) { //Don't delete this

  // Your code here

}//don't delete this either
```

##### !end-placeholder

##### !tests
```js
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

describe('comparisonPractice', function() {

  let oldConsoleLog = console.log;

  // Mock console.log
  beforeEach(() => {
    console.log = fn();
  });

  // restore console.log
  afterEach(() => {
    console.log = oldConsoleLog;
  });

  it("Prints correctly x > y", () => {
    comparisonPractice(7,6);
    expect(console.log.mock.calls.length).to.equal(1);
    expect(console.log.mock.calls[0][0]).to.equal("x is bigger");
  });
  it("Prints correctly for x is equal to y", () => {
    comparisonPractice(7,7);
    expect(console.log.mock.calls.length).to.equal(1);
    expect(console.log.mock.calls[0][0]).to.equal("x = y");
  });
  it("Prints correctly for x < y", () => {
    comparisonPractice(2,7);
    expect(console.log.mock.calls.length).to.equal(1);
    expect(console.log.mock.calls[0][0]).to.equal("y is bigger");
  });
})
```

##### !end-tests
##### !hint
Make sure you are using the right version of equivalence! 
##### !end-hint
##### !hint
Remember, don't assign `x` or `y`!
##### !end-hint
##### !hint
```javascript
if (x > y || x === y) {
  if (x > y) {
    console.log("x is bigger")
  }
  else {
    console.log("x = y")
  }
}
else {
  console.log("y is bigger")
}
```
##### !end-hint

### !end-challenge

### !challenge

* type: code-snippet
* language: javascript
* id: c7d71bcc-ec8d-4ebc-a919-8c432a22056a
* title: Problem  3
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

Convert the following Ruby into JS:

```ruby
10.times do |i|
  puts i * i
end
```

##### !end-question

##### !placeholder
```js
function loopPractice() {
  // Your code here
}
```

##### !end-placeholder

##### !tests
```js
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

describe('doSomething', function() {
  let oldConsoleLog = console.log;

  // Mock console.log
  beforeEach(() => {
    console.log = fn();
  });

  // restore console.log
  afterEach(() => {
    console.log = oldConsoleLog;
  });

  it("Prints the right number of times", () => {
    loopPractice();
    expect(console.log.mock.calls.length).to.equal(10);

  });
  it("Prints the correct values", () =>{
    loopPractice();
    expect(console.log.mock.calls[0][0]).to.equal(0);
    expect(console.log.mock.calls[9][0]).to.equal(81);
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

    <details>
    <summary>
    Javascript
    </summary>

    ```javascript

    for (let i = 0; i< 10; i += 1) {
      console.log(i*i)
    }
    ```

    </details>

1. Ruby 
    ```ruby
    total = 0

    (1..3).each do |i|
      total = total + i
    end

    puts total
    ```

    <details>
    <summary>
    Javascript
    </summary>

    ```javascript
    let total = 0

    for (let i = 1; i<=3; i+=1) {
      total += i
    } 

    console.log(total)
    ```

    </details>

1. Ruby
    ```ruby
    i = 0

    while i < 3
      puts "hi"
      i = i + 1
    end

    puts "bye"
    ```

    <details>
    <summary>
    Javascript
    </summary>

    ```javascript
    let i = 0

    while (i < 3) {
      console.log("hi")
      i = i + 1
    }
    console.log("bye")
    ```

    </details>

1. Ruby
    ```ruby
    fruits = ["banana", "apple", "kiwi"]
    fruits.each do |fruit|
      puts "I love #{fruit}!"
    end
    ```

    <details>
    <summary>
    Javascript
    </summary>

    ```javascript
    //for..in
    const fruits = ["banana", "apple", "kiwi"]
    for(let i in fruits) {
      console.log(`I love ${fruits[i]}!`)
    }

    //forEach
    const fruits2 = ["banana", "apple", "kiwi"]
    fruits2.forEach(fruit => console.log(`I love ${fruit}!`))
    ```

    </details>

1. Ruby
    ```ruby
    total = 0
    values = [4, 6, 2, 8, 11]

    values.each do |value|
        total = total + value
    end

    puts total
    ```

    <details>
    <summary>
    Javascript
    </summary>

    ```javascript
    //for..in
    let total = 0
    const values = [4, 6, 2, 8, 11]

    for(let i in values) {
        total = total + values[i]
    }

    console.log(total)

    //forEach
    let total = 0
    const values = [4, 6, 2, 8, 11]

    values.forEach(value => total += value)
        
    console.log(total)
    ```

    </details>

1. Ruby
    ```ruby
    values = [8, 5, 3, 10, 14, 2]
    values.each do |value|
      if value == 10
        puts "Special case!"
      else
        puts "Regular values like #{value}"
      end
    end
    ```

    <details>
    <summary>
    Javascript
    </summary>

    ```javascript
    const values = [8, 5, 3, 10, 14, 2]

    for(let i in values) {
      let value = values[i]
      if (value == 10) {
        console.log("Special case!")
      }
      else {
        console.log(`Regular values like ${value}`)
      }
    }
    ```

    </details>
