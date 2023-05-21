# Ad Hoc Phone Screen - A Sanity Check by Josh Stroud
Source: [https://homework.adhoc.team/fetch/](https://homework.adhoc.team/fetch/)

From the Software Development section of the ["Sanity check" Wikipedia entry](https://en.wikipedia.org/wiki/Sanity_check): "In software development, a sanity test evaluates the result of a subset of application functionality to determine whether it is possible and reasonable to proceed with further testing of the entire application... The point of a sanity test is to rule out certain classes of obviously false results, not to catch every possible error."

The point of this exercise is to offer a "sanity check" of a potential software engineering applicant's abilities as an engineer. You hear about sanity checks as an important part of junior software development interviews on sites like Hacker News and Reddit, where interviewers proclaim that candidates could not even code FizzBuzz.

[FizzBuzz on Wikipedia](https://en.wikipedia.org/wiki/Fizz_buzz)

"Fizz buzz (often spelled FizzBuzz in this context) has been used as an interview screening device for computer programmers. Writing a program to output the first 100 FizzBuzz numbers is a relatively trivial problem requiring little more than a loop and conditional statements. However, its value in coding interviews is to analyze fundamental coding habits that may be indicative of overall coding ingenuity."

A note on ChatGPT and generative AI tools for coding. In general, I have no problem with using ChatGPT to solve a problem. The problem with generative AI tools for coding is that they are often wrong, and you will not catch the mistake unless you read the code. As a technical issue, eventually there will be tools that make the code 100% right. But the intent of the user will always be confusing to computers, because people do not speak in 1's and 0's; they speak in language. 

Applicants who use ChatGPT or any sort of Github Copilot-type coding assistant will be automatically rejected. We will be using GPTZero, an AI plagarism tool, to detect generative AI code, and plan accordingly. 

Brought to you by [Agilend](https://github.com/agilend) of the San Francisco and Los Angeles areas.

# Fetch

At Ad Hoc, our front-end applications often exchange JSON data with various RESTful APIs. We use modern JavaScript
to interact with these APIs and to transform their responses into a format needed by the client application. In
this homework, we provide a sample API with a single endpoint and ask you to write some JavaScript to request data from
the API and transform the response.

## Records API

You'll be provided with a `/records` API endpoint that returns a JSON array of items in the following format:

```json
[
  {
    "id": 1,
    "color": "brown",
    "disposition": "closed"
  },
  {
    "id": 2,
    "color": "green",
    "disposition": "open"
  }
]
```

Each item returned from the `/records` endpoint will have the following:

- **id**: A unique integer
- **color**: One of `"red"`, `"brown"`, `"blue"`, `"yellow"`, or `"green"`
- **disposition**: Either `"open"` or `"closed"`

The `/records` endpoint accepts the following options, sent as query string parameters on the request URL:

- **limit**: The number of items to be returned
- **offset**: The index of the first item to be returned
- **color[]**: Which color to be included in the result set. May be included multiple times, once for each color. If omitted, all colors will be returned.

An example request URL might look like: `/records?limit=2&offset=0&color[]=brown&color[]=green`

## Task

In `api/managed-records.js`, write a function named `retrieve` that requests data from the `/records` endpoint, transforms the result into the format outlined below, and returns a promise that resolves with the transformed object. In addition to `retrieve`, you may add as many helper functions as you wish.

1. Get data from the `/records` endpoint using the Fetch API. Process pages of 10 items at a time. Note that the `/records` endpoint may return more than 10 items per request.

2. The `retrieve` function accepts an `options` object and should support the following keys:

- **page** - Specifies which page to retrieve from the `/records` endpoint. If omitted, fetch page 1.
- **colors** - An array of colors to retrieve from the `/records` endpoint. If omitted, fetch all colors.

  As an example, to fetch the 2nd page of red and brown items from the API, `retrieve` might be called like this:

  ```js
  retrieve({ page: 2, colors: ["red", "brown"] });
  ```

3. You can assume standard HTTP status codes on the response. If a request is unsuccessful, output a simple error message via `console.log()` and recover.

4. Upon a successful API response, transform the fetched payload into an object containing the following keys:

- **ids**: An array containing the ids of all items returned from the request.
- **open**: An array containing all of the items returned from the request that have a `disposition` value of `"open"`. Add a fourth key to each item called `isPrimary` indicating whether or not the item contains a primary color (red, blue, or yellow).
- **closedPrimaryCount**: The total number of items returned from the request that have a `disposition` value of `"closed"` and contain a primary color.
- **previousPage**: The page number for the previous page of results, or `null` if this is the first page.
- **nextPage**: The page number for the next page of results, or `null` if this is the last page.

5. Return a promise from `retrieve` that resolves with the transformed data.

## Additional requirements

- Use the [provided URI library](https://medialize.github.io/URI.js/) to construct the request URL.
- Write your solution using ES2015 or later. Any methods and syntax [supported by Babel are fair game](https://babeljs.io/docs/en/learn#ecmascript-2015-features).
- You must [use the Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) to interact with the `records` endpoint.
- Don't add any additional libraries or edit any files other than `api/managed-records.js`
- We've provided a suite of unit tests. Your solution should pass all tests.
- Please delete the `node_modules` directory before submitting your completed homework.

## Setup

**Requirements:** NodeJS >= 14.0.0, and [yarn >=1.22.0](https://yarnpkg.com/en/docs/install)

`yarn install` to install.

`yarn test` to run the provided unit tests.
