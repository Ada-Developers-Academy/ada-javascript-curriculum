# Intro to Asynchronous Programming

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=594c1094-c9bf-4e67-888b-ac89016740b0&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

By the end of this lesson we will be able to...

- Know the definition for synchronous programming
- Know the definition for asynchronous programming
- Understand that asynchronous programming will ask us to anticipate what to do after the asynchronous process is finished

## A Pizza Metaphor

Imagine the laziest, most exhausted Friday evening at home. It's dinner time, and you have no food in your freezer or fridge, and you aren't about to go grocery shopping, and nobody will make dinner for you. You are going to make a phone call to your favorite restaurant (they're not on an app) and order a dinner for yourself to be delivered to your bed.

There is a series of things that happens between the moment you make the order right to the point where you take the first bite.

In pain-staking detail, with a neighbor, outline all of the actions you would do that start at picking up the phone, and end at eating your meal.

<details style="max-width: 700px; margin: auto;">
  <summary>
    No, seriously. Take 3 minutes to make a list of the actions you do. After that, then read more here.
  </summary>

  What we imagine most people saying is that they somehow make the order, then wait for the order, and then eat.

  It's actually way more likely that people say they make the order, then **while they wait for the order, they do other things,** like read, shower, sleep, watch TV. **You are only able to eat your food after the food order has been** received, cooked, assembled, assigned a driver, driven over, and **delivered to you**.

  This is all to point out that two processes happened at the same time. One process was the food order being received, made, and delivered. The other process was your life: You didn't stop everything you were doing and sit on the couch and stared at the wall while you were waiting for food. Or maybe you did! The point is, you didn't **need** to stop executing other actions while you were waiting for your food. You were able to do plenty of other actions and processes while the food-delivery process was working and finishing.

  Lastly, **once the food delivery happened, you knew what action you had to do next: receive the food and then eat it!**

  Throughout this lesson, we can keep in mind these two questions:
  1. When does this line of code "finish"?
  1. What do we do when this line of code "finishes"?

</details>

## We have been writing Synchronous Code this whole time!

The code that we've always written has been [synchronous](https://developer.mozilla.org/en-US/docs/Glossary/synchronous) code. This means that our code has always finished executing an entire line of code before proceeding to the next line of code.

For example, observe this Ruby code and this JavaScript code which do the same thing:

```ruby

def say_apples
  puts "apples"
end

def say_oranges
  puts "oranges"
end

say_apples
say_oranges
```

```javascript
const sayApples = function() {
  console.log('apples');
}

const sayOranges = function() {
  console.log('oranges')
}

sayApples();
sayOranges();
```

Both code snippets print out `apples` first, and then `oranges` second, because we call the method/function that prints `apples` first, and we call the method/function that prints `oranges` second. If we need to change the order of how these print, we need to change the order of the lines of code.

### Analogy

Unlike the food-delivery example from above, synchronous code **executes and finishes** in a very specific order. An analogy may be more like calling the restaurant and making the order; the restaurant asks what dishes you want, and they wait when you answer before proceeding to the next question.

## What is Asynchronous Programming?

[Asynchronous Programming](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts) is a method of programming that intentionally breaks program flow in order to:

1. Call actions/processes outside of program flow, so that the program doesn't stop for a result

1. Define what happens when the result comes back

How asynchronous programming is actually possible depends on the implementation/way of executing asynchronous calls.

If we get to employ asynchronous programming into our programs, then we get to do interesting things that would normally require us to wait a long time **at the same time** as doing other things, without waiting for a long task to finish.

In order to do this well, though, we will have to write code that:
- uses specific technologies that support running asynchronous code (again, this is a matter of tools and environment)
- anticipate all of the cases of what happens while an asynchronous call is running

## How Do We Write Asynchronous Programming?

To write good asynchronous code, we will have to determine and write the following things:

1. The _asynchronous call/function that we are invoking_
    - How do we order the food?
1. What do we do after the asynchronous call finishes
    - What do we do after we receive the food deliver?
1. What do we do if the asynchronous call doesn't finish successfully
    - What do we do if the food never arrives? What do we do if the restaurant calls back and says that they are out of food? What do we do if the restaurant calls back and says they lost your order?
1. Ensure that the rest of the program runs correctly, without bugs, even if it does things while the asynchronous call is executing
    - If you are watching TV while waiting for the food to be delivered, how do we make sure that you aren't too hungry and you order another dinner?
    - If you are hanging out with a friend while waiting for the food to be delivered, and your friend asks you to feed them now, what do you do?

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: da98a947-e73e-4894-b320-fe2e47ec604d
* title: What does this best describe
* points: 1
* topics: javascript, asynch

##### !question

What does this best describe:

1.  I open the box
1.  Then a take out the parts
1.  I read step 1 of the instructions
1.  I find the parts for step 1
1.  I do step 1 in assembling the widget
1.  I move on to read step 2 and repeat

##### !end-question

##### !options

* A **synchronous** process
* An **asynchronous** process

##### !end-options

##### !answer

* A **synchronous** process

##### !end-answer

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
* id: 2ad883e0-7e16-4b0b-8e9e-58519dc73c77
* title: What does this best describe
* points: 1
* topics: javascript, async

##### !question

What does this best describe:

-  I combine the ingredients into the mixer
-  I start the mixer and go on start my Ada CS Fun homework
-  When the mixer finishes I will move on to putting it into the crust and then into the oven
-  Then while it bakes I'll do more CS Fun homework
-  When the oven finishes I'll turn off the oven and remove the pie.
-  While it cools I'll do more CS fun homework
-  When it's cool enough I'll eat.

##### !end-question

##### !options

* A **synchronous** process
* An **asynchronous** process

##### !end-options

##### !answer

* An **asynchronous** process

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

It's asynchronous because you don't know when precisely each step of the cooking will complete, instead you start it and go on to do other things.  Then you respond when those tasks finish.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->



## Conclusion

Asynchronous programming is a big, broad subject. Traditionally, we have written a lot of code that runs in a very specific order (synchronous). However, certain technologies allow us to write asynchronous code, and we'll see plenty in JavaScript.

To write asynchronous code, we'll generally need to anticipate four things:

1. How do we make an asynchronous call?
1. What should happen if the asynchronous call finishes successfully?
1. What should happen if the asynchronous call doesn't finish successfully?
1. What other pieces of code are depending on this asynchronous call?

## An Optional Introduction: Event-Driven Programming

[Event-Driven Programming](https://en.wikipedia.org/wiki/Event-driven_programming) is a programming paradigm. Another programming paradigm we've learned about is Object-Oriented programming. Event-Driven Programming as a programming paradigm means that there is a set of design patterns meant for a different way of thinking of code.

In Event-Driven Programming, design patterns will lead developers to think about how to write code in terms of **events**, not objects.

In event-driven programming, there is a concept of an **event.** An **event** is named action that can be triggered/fired/sent, and also listened to/handled/received.

In our food delivery analogy, likely we would say "When the delivery person rings the doorbell" is triggering an event of "a person is at the front door." Then, we would say "answering the door" is handling the event.

Event-driven programming pairs really well with asynchronous programming. For both, we have to think about who makes the call (asynchronous call or event trigger), and what happens when that call happens (whether it finished successfully, or how to handle the event). We will get more into event-driven programming more soon!

## An Optional Aside: A Deeper Look

JavaScript can be written for programs that utilize event-driven programming. Actually, under-the-hood, JavaScript environments manage how code runs in the [Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop).

A more technical dive into how JavaScript executes code using the JavaScript event loop may help your understanding of asynchronous programming and also how JavaScript works in general.

## Resources

- [MDN's intro on General Asynchronous Programming Concepts](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts)
- [MDN's intro to Asynchronous JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)
- [MDN's article on JavaScript's Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)