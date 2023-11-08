# 01-How to add JavaScript

> Learn how to add JavaScript and its loading strategies.

---

## Internal JavaScript

```html
<script>
    // JavaScript goes here
</script>
```

For example:

```html
<script>
    document.addEventListener("DOMContentLoaded", () => {
        function createParagraph() {
            const para = document.createElement("p");
            para.textContent = "You clicked the button!";
            document.body.appendChild(para);
        }

        const buttons = document.querySelectorAll("button");

        for (const button of buttons) {
            button.addEventListener("click", createParagraph);
        }
    });
</script>
```

---

## External JavaScript

```html
<script src="script.js"></script>
```

---

## Script loading strategies

We can use attributes `async` and `defer` to decide how to load our JavaScript.

Here is a visual representation of the different script loading methods and what that means for your page:

![](../_assets/_images/async-defer.jpg ':size=1000')

- `async` and `defer` both instruct the browser to download the script(s) in a **separate thread**, while the rest of the page (the DOM, etc.) is downloading, so **the page loading is not blocked during the fetch process**.
- scripts with an `async` attribute will **execute as soon as the download is complete**. This **blocks the page** and **does not guarantee any specific execution order**.
- scripts with a `defer` attribute will load **in the order** they are in and will only **execute once everything has finished loading**.
- If your scripts should be run immediately and they **don't have any dependencies**, then use `async`.
- If your scripts need to wait for parsing and **depend on other scripts or the DOM being in place**, load them using `defer` and put their corresponding `<script>` elements in the order you want the browser to execute them.



---

?> {docsify-updated}