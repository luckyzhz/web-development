# 10-How to use promises

> To understand how to use promises in JavaScript.

---

With a promise-based API, the asynchronous function starts the operation and returns a `Promise` object. You can then attach **handlers** to this promise object, and these handlers will be executed when the operation has succeeded or failed.

!> Open a browser tab and visit <https://example.org>. The codes of this article need to be test in the console of that tab.

## Using the fetch() API

```js
const fetchPromise = fetch(
    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

console.log(fetchPromise);

fetchPromise.then((response) => {
    console.log(`Received response: ${response.status}`);
});

console.log("Started request…");
```

The complete output should be something like:

```
Promise { <state>: "pending" }
Started request…
Received response: 200
```

Note that `Started request…` is logged before we receive the response. Unlike a synchronous function, `fetch()` returns while the request is still going on, enabling our program to stay responsive. The response shows the `200` (OK) [status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status), meaning that our request succeeded.

---

## Chaining promises

With the `fetch()` API, once you get a `Response` object, you need to call another function to get the response data. In this case, we want to get the response data as **JSON**, so we would call the `json()` method of the `Response` object. It turns out that `json()` is also **asynchronous**. So this is a case where we have to call **two successive asynchronous functions**.

```js
const fetchPromise = fetch(
    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise.then((response) => {
    const jsonPromise = response.json();
    jsonPromise.then((data) => {
        console.log(data[0].name);
    });
});
```

The elegant feature of promises is that `then()` itself **returns a promise**, *which will be completed with the result of the function passed to it*. This means that we can (and certainly should) **rewrite** the above code like this:

```js
const fetchPromise = fetch(
    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise
    .then((response) => response.json())
    .then((data) => {
        console.log(data[0].name);
    });
```

Instead of calling the second `then()` inside the handler for the first `then()`, we can **return the promise** returned by `json()`, and call the second `then()` on that return value. This is called **promise chaining**.

There's one more piece to add. We need to check that the server accepted and was able to handle the request, before we try to read it.

```js
const fetchPromise = fetch(
    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise
    .then((response) => {
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        return response.json();
    })
    .then((data) => {
        console.log(data[0].name);
    });
```

---

## Catching errors

In the last section, we saw that error handling can get very difficult with nested callbacks, making us handle errors at every nesting level.

To support error handling, `Promise` objects provide a `catch()` method. The **handler** passed to `catch()` is called when the asynchronous operation *fails*.

If you add `catch()` to the end of a promise chain, then it **will be called when any of the asynchronous function calls fail**. So you can implement an operation as several consecutive asynchronous function calls, and have a single place to handle all errors.

```js
const fetchPromise = fetch(
    "bad-scheme://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise
    .then((response) => {
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        return response.json();
    })
    .then((data) => {
        console.log(data[0].name);
    })
    .catch((error) => {
        console.error(`Could not get products: ${error}`);
    });
```

---

## Promise terminology

promise states:

- **pending**: the promise has been created, and the asynchronous function it's associated with has not succeeded or failed yet. This is the state your promise is in when it's returned from a call to `fetch()`, and the request is still being made.
- **fulfilled**: the asynchronous function has **succeeded**. When a promise is fulfilled, its `then()` handler is called.
- **rejected**: the asynchronous function has **failed**. When a promise is rejected, its `catch()` handler is called.

Sometimes, we use the term **settled** to cover both **fulfilled** and **rejected**.

A promise is **resolved** if it is settled, or if it has been "locked in" to follow the state of another promise.

---

## Combining multiple promises

Sometimes, you may need **all the promises to be fulfilled**, but they **don't depend** on each other. In a case like that, it's much more efficient to start them all off together, then **be notified when they have all fulfilled**. The `Promise.all()` method is what you need here. It takes **an array of promises** and returns a single promise.

The promise returned by `Promise.all()` is:

- fulfilled when and if **all** the promises in the array are fulfilled. In this case, the `then()` handler is called with **an array of all the responses**, in the same order that the promises were passed into `all()`.
- rejected when and if **any** of the promises in the array are rejected. In this case, the `catch()` handler is called with the error thrown by the promise that rejected.

```js
const fetchPromise1 = fetch(
    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);
const fetchPromise2 = fetch(
    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found",
);
const fetchPromise3 = fetch(
    "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json",
);

Promise.all([fetchPromise1, fetchPromise2, fetchPromise3])
    .then((responses) => {
        for (const response of responses) {
            console.log(`${response.url}: ${response.status}`);
        }
    })
    .catch((error) => {
        console.error(`Failed to fetch: ${error}`);
    });
```

Sometimes, you might need **any** one of a set of promises to be fulfilled, and **don't care which one**. In that case, you want `Promise.any()`.

```js
const fetchPromise1 = fetch(
    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);
const fetchPromise2 = fetch(
    "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found",
);
const fetchPromise3 = fetch(
    "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json",
);

Promise.any([fetchPromise1, fetchPromise2, fetchPromise3])
    .then((response) => {
        console.log(`${response.url}: ${response.status}`);
    })
    .catch((error) => {
        console.error(`Failed to fetch: ${error}`);
    });
```

---

## async and await

The `async` keyword gives you a simpler way to work with asynchronous promise-based code. Adding `async` at the start of a function **makes it an async function**:

```js
async function myFunction() {
    // This is an async function
}
```

**Inside an async function**, you can use the `await` keyword before a call to **a function that returns a promise**. This makes the code **wait** at that point **until the promise is settled**, at which point the **fulfilled value** of the promise is treated as a return value, or the **rejected value** is thrown.

This enables you to write code that uses asynchronous functions but looks like synchronous code.

```js
async function fetchProducts() {
    try {
        // after this line, our function will wait for the `fetch()` call to be settled
        // the `fetch()` call will either return a Response or throw an error
        const response = await fetch(
            "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
        );
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        // after this line, our function will wait for the `response.json()` call to be settled
        // the `response.json()` call will either return the parsed JSON object or throw an error
        const data = await response.json();
        console.log(data[0].name);
        // `async` functions always **return a promise**
        // the returned value `data` will be the response of the Promise object returned by `fetchProducts()`
        return data;
    } catch (error) {
        console.error(`Could not get products: ${error}`);
    }
}

fetchProducts();
```

Here, we are calling `await fetch()`, and instead of getting a `Promise`, our caller gets back a fully complete `Response` object, just as if `fetch()` were a synchronous function!

Note that `async` functions always **return a promise**, so you **can't** do something like:

```js
const promise = fetchProducts();
console.log(promise[0].name); // "promise" is a Promise object, so this will not work
```

Instead, you'd need to do something like:

```js
const promise = fetchProducts();
promise.then((data) => console.log(data[0].name));
```

Also, note that you can only use `await` **inside** an `async` function, unless your code is in a [JavaScript module](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules).

You'll probably use `async` functions a lot where you might otherwise use promise chains, and they make working with promises much more **intuitive**.



---

?> {docsify-updated}