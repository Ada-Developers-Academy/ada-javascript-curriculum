# Making `POST` Requests using `axios` in JavaScript

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=d917a57a-afa4-4f83-a23a-ab95012a55e7&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

Setup notes: This lesson will make use of the [Ada Trip Reserving Service™ Trip API™™™](https://github.com/AdaGold/trip-api), which is running on Heroku at [https://trektravel.herokuapp.com](https://trektravel.herokuapp.com).

This lesson will use Postman, a text editor, and terminal.

If you would like a refresher on how to use Postman, the [instruction video for the Video Store API project](https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=055e7c13-0795-4c80-9933-ac780041803f&start=undefined) is a good resource.

## Learning Goals
- Review exploring APIs by reading documentation and using Postman
- Use axios to make POST requests
- Anticipate how to apply making asynchronous HTTP requests in fuller JavaScript programs

## Introduction

We can send POST requests using axios just like we send GET requests.

Think through the following questions:

- What are the big differences between POST and GET?
- What did we use POST requests for in Rails?
- What kinds of specific actions did users do in order to trigger POST requests in our Rails apps?

## Our Example Today: Trip API

The **Ada Trip Reserving Service™** is a service that does two things very well:

1. helps tour guides create Trip packages catered to global travelers
2. helps travelers find Trip packages that fit their needs, and make a reservation for that trip

Today, we will use the [Ada Trip Reserving Service™ Trip API™™™](https://github.com/AdaGold/trip-api) to create new Trip packages.

Take a few minutes to explore the [API documentation](https://github.com/AdaGold/trip-api/blob/master/README.md). Use Postman to experiment. Answer the following questions:

1. What is the API call that lists all existing Trip packages?
2. Make that API call and see the list of all existing Trip packages. How many are there? What are their IDs?
3. What is the API call that creates a new Trip package?
4. What is the verb and URL of that request?
5. What are the required query parameters? What are the optional query parameters?

<details>

  <summary>
    Check your answers here!
  </summary>

  1. `get` `https://trektravel.herokuapp.com/trips`
  2. Depends, but it's good to remember to note the trip ID for this exercise
  3. `post` `https://trektravel.herokuapp.com/trips`
  4. post, and `https://trektravel.herokuapp.com/trips`
  5. Required: `name`, `continent`, `category`, `weeks`, and `cost`. Optional: `about`

</details>

## Making a `POST` request in axios

The syntax for making a POST request is very similar to a GET request, with a few minor differences:
- The function call is `post()` instead of `get()`
- The function `post()` takes 2 parameters just like the `get()` function, first the URL and second the optional params object
- The format of the params object is slightly different:
    - GET format: 
    ```js
    {
        params: {
            category: 'tree',
            name: 'spruce',
        }
    }
    ```
    - POST format: 
    ```js
    {
        category: 'tree',
        name: 'spruce'
    }
    ```
- `post()` expects the same `then()` and `catch()` chain as `get()`

### axios `POST` example using the Trip API to make a new trip

```js
const axios = require('axios');

const tripData = {
  name: 'Simon\'s Chill Trip to Chicago',
  continent: 'North America',
  about: 'A tour around good architecture and hot dogs.',
  category: 'casual',
  weeks: 1,
  cost: 180,
};

axios.post('https://trektravel.herokuapp.com/trips', tripData)
  .then((response) => {
    console.log('RESPONSE:', response);
    console.log('RESPONSE DATA:', response.data);
    console.log('plums!');
  })
  .catch((error) => {
    console.log('ERROR:', error);
    console.log('ERROR RESPONSE:', error.response);
    console.log('mangos!');
  })
  .finally(() => {
    console.log('finally done!');
  });
```

Confirm your understanding of the code by answering these questions (use the [axios documentation](https://github.com/axios/axios) to supplement):

1. Did we need to re-install axios for this using `$ npm install`? Why or why not?
2. Did we need to "load" axios into this file? If so, how?
3. What line of code **makes** the POST request?
4. What is the first parameter to `post()`?
5. What is the value of the second parameter to `post()`? What does it represent? Where is it declared and assigned? Why is it `const`?
6. `post()` also expects the structure of chaining `then()`, `catch()`, and `finally()`. What do we do if the response comes back successfully?
7. What do we do if the response comes back unsuccessfully?
8. Does the `post()` function have support for `finally()` to be chained?

<details>

  <summary>
    Check your answers here.
  </summary>

  1. We did not need to re-install axios, because previously we installed axios onto our machine globally. If we had a new JavaScript project that had its own dependencies managed in a `package.json` file (much like a Ruby project with its own `Gemfile` file), we may need to run `$ npm install`
  2. Yes, we loaded axios with `const axios = require('axios');`
  3. The line of code that makes the POST request is `axios.post('https://trektravel.herokuapp.com/trips', tripData)`
  4. The first parameter is the URL/API endpoint, which is `'https://trektravel.herokuapp.com/trips'`
  5. The second parameter is the data we are sending with the POST request. We are sending `tripData`, which is an object that has the name/value pairs that match what the API is expecting, and our own Trip information. We make `tripData` a `const` variable because we don't expect it to ever be re-assigned.
  6. When the response comes back successfully, we print to the terminal the response, response data, and the word "plums!"
  7. When the response comes back successfully, we print to the terminal the error, error response, and the word "mangos!"
  8. The `post()` function does support `finally()`

</details>

#### By the way, we could inline `tripData`

We can sidestep the `tripData` variable, the difference is just stylistic:
```js
// ...

axios.post('https://trektravel.herokuapp.com/trips', {
    name: 'Simon\'s Chill Trip to Chicago',
    continent: 'North America',
    about: 'A tour around good architecture and hot dogs.',
    category: 'casual',
    weeks: 1,
    cost: 180,
})
.then( ... )
.catch( ... )
```

### Run This Code And Look at the Response

Start by running this code.  It should respond with success:

1. What kind of information does axios give back about the response in the `response` object (made available in `then()`)?
2. What kind of data does the Trips API™™™ give back in the `response.data` object (made available in `then()`)?

<details>

  <summary>
    Check your answers here.
  </summary>

  1. The response object contains the status code, headers, response data, etc.
  2. The `response.data` looks similar to this:

  ```js
  {
    id: 136,
    name: "Simon's Chill Trip to Chicago",
    continent: 'North America',
    about: 'A tour around good architecture and hot dogs.',
    category: 'casual',
    weeks: 1,
    cost: 180
  }
  ```
</details>

Change the code to this, and run it again. Note that the trip data has been turned into `badTripData`, which has a blank `name`, so it should not be a successful call, and get into the `catch`.

```js
const axios = require('axios');

const badTripData = {
  name: '',
  continent: 'North America',
  about: 'A tour around good architecture and hot dogs.',
  category: 'casual',
  weeks: 1,
  cost: 180,
};

axios.post('https://trektravel.herokuapp.com/trips', badTripData)
  .then((response) => {
    // 
  })
  .catch((error) => {
    console.log('ERROR:', error);
    console.log('ERROR RESPONSE:', error.response);
    console.log('error.response.data', error.response.data);
  });
```

1. What kind of information does axios give back about the error in the `error` object (made available in `catch()`)?
2. What kind of data does the Trips API™™™ give back in the `error.response.data` object (made available in `catch()`)?

<details>

  <summary>
    Check your answers here.
  </summary>

  1. The response object contains status code, headers, response data, etc.
  2. The `errror.data` looks similar to this:

  ```js
  { errors: { name: [ "can't be blank" ] } }
  ```
</details>

## Exercise: Make Your Own Trip

Using the code samples above as an example, and write a `.js` file that creates your own Trip package!

Write, iterate, and run the file, until you get your own Trip package successfully created. **Note down the ID of your newly created Trip** because you will use it soon in this lesson.

If you response comes back unsuccessful/as an error, use this chance to practice debugging. What caused the error? If the API gave back an error, you can read the details of the error in `error.response` and `error.response.data`. The text in those objects will say something useful about the error that the API sends back.

If all else fails, use these error messages to dive into the source code of the API and find any validations on the `Trip` model. :)

## Exercise: Reserve a Ticket On Your Own Trip

Utilizing the [Ada Trip Reserving Service™ Trip API™™™](https://github.com/AdaGold/trip-api) and the `post()` syntax, write a JS script that does the following:

1. Makes an object in `const tripReservationData`, with all of the correct name/value pairs that the API specifies
1. Creates a POST request to the right endpoint for specifically your own new Trip package that you created in the previous exercise, and that uses `tripReservationData`
1. If the response comes back as success, the program prints `'Trip reserved successfully.'`, and then prints the value of the response's data
1. If the response comes back as not success, the program prints `'Error occurred.'`, and then prints the value of the error response's data

<details>

  <summary>
    Once you're finished, compare your code to our sample solution
  </summary>

  ```js
  const axios = require('axios');

  const tripId = 136;

  const tripReservationData = {
    name: 'Simon',
    email: 'Simon@tildeemail.dev',
  };

  axios.post(`https://trektravel.herokuapp.com/trips/${tripId}/reservations`, tripReservationData)
    .then((response) => {
      console.log('Trip reserved successfully.')
      console.log('The response came back', response.data);
    })
    .catch((error) => {
      console.log('Error occurred.');
      console.log('The error came back', error.response.data);
    });
  ```

</details>

## Brainstorm Applications

Great work! We have some solid examples and exercises that show making HTTP requests with JavaScript. Let's brainstorm a possible user-flow for a CLI program. The CLI program should allow a user to list trip packages, see details for one trip package, and reserve a ticket for one trip package.

Then, write **pseudocode** for a JS script for that program.

Skip over the pseudocode details for getting user input, and make assumptions about the user input.

### Asynchronous Code Requires Different Patterns

When writing pseudocode, you probably observed the following things:

1. In some ways, writing the API calls in JavaScript should feel straightforward
1. Before we can make an API call to reserve a ticket on a Trip, we needed to make sure we had a value for the `tripId` that the API call requires. However, because our code is asynchronous, we need to make sure we call `axios.post()` to the Trip Reserve endpoint **after** we get a response from making our Trip using the Trip Create endpoint, which gives us our Trip ID.

<details>
<summary>Using the axios functions, how do you make sure the POST request to Trip Reserve happens after you get a response from Trip Create?</summary>

Make the API call to Trip Reserve in the function **inside** of `then()` chained to the Trip Create call.

For now, we will tend to put a lot of functionality in `then()` and `catch()` blocks, and practice our knowledge of functions, and callback functions.  When we introduce other tools, libraries, and programming paradigms, we will approach this from a different angle.
</details>

## Conclusion

As in Ruby, the difficult part of working with an API in JavaScript is not making the request, but rather figuring out what request to make, and what to do afterwards. Though the setting is different, our work will follow a similar pattern:

1. Explore the API using the documentation, Postman, and other tools
    - How do you need to format your data
    - How does the API respond
    - What does an error response look like?
1. Write code to interact with the API
    - Hard-coded data for input
    - Logging to the console as output

## Additional Resources
- [axios documentation](https://github.com/axios/axios)