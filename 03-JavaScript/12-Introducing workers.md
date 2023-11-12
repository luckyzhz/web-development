# 12-Introducing workers

> Workers enable you to run some tasks in a separate thread of execution.

---

Workers give you the ability to run some tasks in a different thread, so you can start the task, then continue with other processing (such as handling user actions).

There are three different sorts of workers:

- **dedicated workers**
- **shared workers**
- **service workers**

In this article, we'll walk through an example of the first sort of worker, then briefly discuss the other two.

?> ⚠️ **Note**: Workers can't access the DOM (the window, document, page elements, and so on).

!> To run the code of this article, you'll have to run a local **web server**, because `file://` URLs are not allowed to load workers.

## Dedicated workers

We will run an inefficient prime number generator (it may take several seconds to finish generating) in a worker while our main thread can still accept users' input.

To do the experiment, We need three files:

- `index.html`
- `main.js`
- `generate.js`

### index.html

Note that only the `main.js` is included in a `<script>` element.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime numbers</title>

    <!-- The worker code is kept in a separate script from the main code. -->
    <!-- Only the main code is included in a `<script>` element -->
    <script src="main.js" defer></script>
</head>

<body>
    <label for="quota">Number of primes:</label>
    <input type="text" id="quota" name="quota" value="1000000">

    <button id="generate">Generate primes</button>
    <button id="reload">Reload</button>

    <textarea id="user-input" rows="5" cols="62">
        Try typing in here immediately after pressing "Generate primes"
    </textarea>

    <div id="output"></div>
</body>

</html>
```

### main.js

- First, we're creating the worker using the `Worker()` constructor. We pass it a URL pointing to the worker script. **As soon as the worker is created, the worker script is executed**.
- Next, we add a click event handler to the "Generate primes" button. When the button is clicked, we send a **message** to the worker using `worker.postMessage()`. This message can take an argument, and in this case, we're passing a **JSON** object.
- Next, we add a `message` event handler to the worker. This is so the worker can tell us when it has finished, and pass us any resulting data.
- Finally, we implement the `click` event handler for the "Reload" button.

```js
// Create a new worker, giving it the code in "generate.js"
// As soon as the worker is created, the worker script is executed.
const worker = new Worker("./generate.js");

// When the user clicks "Generate primes", send a message to the worker.
// The message command is "generate", and the message also contains "quota",
// which is the number of primes to generate.
document.querySelector("#generate").addEventListener("click", () => {
    const quota = document.querySelector("#quota").value;
    worker.postMessage({
        command: "generate",
        quota,
    });
});

// When the worker sends a message back to the main thread,
// update the output box with a message for the user, including the number of
// primes that were generated, taken from the message data.
worker.addEventListener("message", (message) => {
    document.querySelector("#output").textContent
        = `Finished generating ${message.data} primes!`;
});

document.querySelector("#reload").addEventListener("click", () => {
    document.querySelector("#user-input").value =
        'Try typing in here immediately after pressing "Generate primes"';
    document.location.reload();
});
```

### generate.js

- First, the worker starts listening for messages from the main script. It does this using `addEventListener()`, which is a **global function** in a worker. Inside the `message` event handler, the `data` property of the event contains a copy of the argument passed from the main script.
- We send a message to the main script when we are done. We use the `postMessage()` function for this, which is also a **global function** in a worker.

```js
// Listen for messages from the main thread.
// If the message command is "generate", call `generatePrimes()`
addEventListener("message", (message) => {
    if (message.data.command === "generate") {
        let primesLength = generatePrimes(message.data.quota);
        // When we have finished, send a message to the main thread,
        // including the number of primes we generated.
        postMessage(primesLength);
    }
});

// Generate random prime numbers (very inefficiently)
function generatePrimes(quota) {
    function isPrime(n) {
        for (let i = 2; i <= Math.sqrt(n); i++) {
            if (n % i === 0) {
                return false;
            }
        }
        return true;
    }

    const primes = [];
    const min = 1000
    const max = 1000000;

    while (primes.length < quota) {
        const candidate =
            Math.floor(Math.random() * (max - min + 1) + min);
        if (isPrime(candidate)) {
            primes.push(candidate);
        }
    }

    return primes.length;
}
```

---

## Other types of workers

The worker we just created was what's called a **dedicated worker**. This means it's *used by a **single** script instance*.

There are other types of workers:

- **Shared workers**: can be *shared by **several** different scripts* running in different windows.
- **Service workers**: act like **proxy servers**, **caching resources** so that web applications can work when the user is **offline**. They're a key component of [Progressive Web Apps](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps).



---

?> {docsify-updated}