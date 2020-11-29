# JavaScript Worksheet: Functions
For Part 1, read the code in each section, then write the equivalent JavaScript code for the Ruby that is given. Start by writing it out in a text editor or on a piece of paper. Then try running it and tweak your code until it successfully runs with expected output.
For Part 2, follow the directions for each problem.

**Note:** For each function you create, you should **also write the code to call** the function.

## Part 1
<!--BEGIN CHALLENGE-->

### !challenge

* type: paragraph
* id: f5499bb9-86ab-40cc-86b8-320306e2ebfc
* title: Convert to JavaScript
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

Convert the following code into JavaScript, and then call the function:
```ruby
def hello
  puts 'hello!'
end
```

##### !end-question

##### !placeholder

your code here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

```javascript
const hello = function() { 
  console.log('hello!');
}

hello()
```

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: paragraph
* id: aeea65c1-cb0d-4126-b14d-7f01ae183556
* title: Convert to JavaScript
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

Convert the following code into JavaScript, and then call the function:
```ruby
def say_num(number)
  puts 'Your number is #{number}.'
end
```

##### !end-question

##### !placeholder

your code here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

```javascript
const sayNum = function (number) {
    console.log(`Your number is ${number}`);
  }

sayNum(5)
```

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: paragraph
* id: 0bac36b7-ce84-4851-9899-3a0361343b58
* title: Convert to JavaScript
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

Convert the following code into JavaScript, and then call the function:
```ruby
def larger_num(first, second)
  if first >= second
    first
  elsif second > first
    second
  end
end
```

##### !end-question

##### !placeholder

your code here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

```javascript
const largerNum = function (first, second) {
  if (first >= second) {
    return first
  } else {
    return second
  }
}

console.log(largerNum(5,7))
console.log(largerNum(7,5))
```

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: paragraph
* id: e3555349-29a4-44d7-afcb-5bcff277352c
* title: Convert to JavaScript
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

Convert the following code into JavaScript, and then call the function:
```ruby
def output(items)
  items.each do |item|
    puts item
  end
end
```

##### !end-question

##### !placeholder

your code here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

```javascript
const output = function (items) {
  for (const i in items) {
    console.log(items[i]);  
  };
}

output([1,2,3])
```

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->

## Part 2
Follow the directions for each problem.
<!--BEGIN CHALLENGE-->

### !challenge

* type: short-answer
* id: 18921e5f-ee7b-45f8-8aa7-8262782e8dfe
* title: JavaScript Syntax
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

Invoke the `zombies` function.
```javascript
const zombies = function() {
  return "We like to eat people";
};
```

##### !end-question

##### !answer

zombies();

##### !end-answer

##### !placeholder

your answer here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

`zombies();`

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: short-answer
* id: ebd24b23-ad42-4393-a0cd-9f4360d11f5c
* title: JavaScript Syntax
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

What does the following code print to the console?
```javascript
console.log(function() {
  return "Hey hey hey";
}());
```

##### !end-question

##### !answer

Hey hey hey

##### !end-answer

##### !placeholder

your answer here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

`Hey hey hey`

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->
<!--BEGIN CHALLENGE-->

### !challenge

* type: short-answer
* id: 8bc11819-d611-47b7-9b1c-8719826b6472
* title: JavaScript Syntax
<!--Other optional fields (checkpoints only) -->
<!--`points: 1`: the number of points for scoring as a checkpoint-->
<!--`topics: python, pandas`: the topics for analyzing points-->

##### !question

What does the following code print to the console?
```javascript
const blabbermouth = function() { };
console.log(blabbermouth.name);
```

##### !end-question

##### !answer

blabbermouth

##### !end-answer

##### !placeholder

your answer here...

##### !end-placeholder

<!--optional-->
##### !hint

##### !end-hint

<!--optional, checkpoints only-->
##### !rubric

##### !end-rubric

<!--optional-->
##### !explanation

`blabbermouth`

##### !end-explanation

### !end-challenge

<!--END CHALLENGE-->