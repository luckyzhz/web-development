# 11-How to implement a promise-based API

> To understand how to implement promise-based APIs.

---

Generally, when you implement a promise-based API, you'll be **wrapping an asynchronous operation**, which might use *events*, or *plain callbacks*, or a *message-passing model*. You'll arrange for a Promise object to handle the *success* or *failure* of that operation properly.

## Implementing an alarm() API

In this example we'll implement a promise-based alarm API, called alarm(). It will take as arguments the name of the person to wake up and a delay in milliseconds to wait before waking the person up.

### The Promise() constructor

Our `alarm()` function will return a `Promise` that is fulfilled when the timer expires. It will pass a "Wake up!" message into the `then()` handler, and will reject the promise if the caller supplies a negative delay value.

The key component here is the `Promise()` constructor. The `Promise()` constructor takes a single **function** as an argument. We'll call this function the `executor`. When you create a new promise you supply the implementation of the executor.

This executor function itself takes two arguments, which are both also **functions**, and which are conventionally called `resolve` and `reject`.

In your executor implementation, you call the *underlying asynchronous function*. If the asynchronous function succeeds, you call `resolve`, and if it fails, you call `reject`. If the executor function throws an **error**, `reject` is called automatically. You can pass **a single parameter** of any type into `resolve` and `reject`.

So we can implement alarm() like this:

```js
function alarm(person, delay) {
    return new Promise((resolve, reject) => {
        if (delay < 0) {
            throw new Error("Alarm delay must not be negative");
        }
        setTimeout(() => {
            resolve(`Wake up, ${person}!`);
        }, delay);
    });
}
```

---

## Using the alarm() API

We can call `alarm()`, and on the returned promise call `then()` and `catch()` to set handlers for promise **fulfillment** and **rejection**.

```js
const name = document.querySelector("#name");
const delay = document.querySelector("#delay");
const button = document.querySelector("#set-alarm");
const output = document.querySelector("#output");

function alarm(person, delay) {
    return new Promise((resolve, reject) => {
        if (delay < 0) {
            throw new Error("Alarm delay must not be negative");
        }
        setTimeout(() => {
            resolve(`Wake up, ${person}!`);
        }, delay);
    });
}

button.addEventListener("click", () => {
    alarm(name.value, delay.value)
        .then((message) => (output.textContent = message))
        .catch((error) => (output.textContent = `Couldn't set alarm: ${error}`));
});
```

---

## Using async and await with the alarm() API

Since `alarm()` returns a `Promise`, we can do everything with it that we could do with any other promise: promise chaining, `Promise.all()`, and `async` / `await`:

```js
const name = document.querySelector("#name");
const delay = document.querySelector("#delay");
const button = document.querySelector("#set-alarm");
const output = document.querySelector("#output");

function alarm(person, delay) {
    return new Promise((resolve, reject) => {
        if (delay < 0) {
            throw new Error("Alarm delay must not be negative");
        }
        setTimeout(() => {
            resolve(`Wake up, ${person}!`);
        }, delay);
    });
}

button.addEventListener("click", async () => {
    try {
        const message = await alarm(name.value, delay.value);
        output.textContent = message;
    } catch (error) {
        output.textContent = `Couldn't set alarm: ${error}`;
    }
});
```



---

?> {docsify-updated}