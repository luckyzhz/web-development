# 08-Working with JSON

> To understand how to work with data stored in JSON, and create your own JSON strings.

---

## What is JSON?

**JSON** is a **string** whose format very much resembles JavaScript object literal format. A JSON string can be stored in its own file, which is basically just a text file with an extension of `.json`, and a MIME type of `application/json`.

Here is a JSON example:

```json
{
    "squadName": "Super hero squad",
    "active": true,
    "members": [
        {
            "name": "Molecule Man",
            "age": 29,
            "powers": [
                "Radiation resistance",
                "Turning tiny",
                "Radiation blast"
            ]
        },
        {
            "name": "Madame Uppercut",
            "age": 39,
            "powers": [
                "Million tonne punch",
                "Damage resistance",
                "Superhuman reflexes"
            ]
        },
        {
            "name": "Eternal Flame",
            "age": 1000000,
            "powers": [
                "Immortality",
                "Heat Immunity",
                "Inferno"
            ]
        }
    ]
}
```

- JSON is purely a **string** with a specified data format — it contains only properties, **no methods**.
- JSON requires **double quotes** to be used around **strings** and **property names**.
- JSON can actually take the form of any data type that is valid for inclusion inside JSON, not just arrays or objects. So for example, a single string or number would be valid JSON.

?> ⚠️ **Note**: Converting a string to a native object is called *deserialization*, while converting a native object to a string so it can be transmitted across the network is called *serialization*.

---

## Working through a JSON example

We are going to load the JSON into our script, and use some nifty DOM manipulation to display it.

<!-- tabs:start -->

#### **HTML**

```html
<!DOCTYPE html>
<html lang="en-us">

<head>
    <meta charset="utf-8">
    <title>Our superheroes</title>

    <link href="https://fonts.googleapis.com/css?family=Faster+One" rel="stylesheet">
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <header></header>

    <section></section>

    <script></script>
</body>

</html>
```

#### **style.css**

```css
/* || general styles */

html {
    font-family: 'helvetica neue', helvetica, arial, sans-serif;
}

body {
    width: 800px;
    margin: 0 auto;
}

h1,
h2 {
    font-family: 'Faster One', cursive;
}

/* header styles */

h1 {
    font-size: 4rem;
    text-align: center;
}

header p {
    font-size: 1.3rem;
    font-weight: bold;
    text-align: center;
}

/* section styles */

section article {
    width: 33%;
    float: left;
}

h2 {
    font-size: 2.5rem;
    letter-spacing: -5px;
    margin-bottom: 10px;
}
```

<!-- tabs:end -->

### Top-level function

```js
async function populate() {
    const requestURL =
        "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json";
    const request = new Request(requestURL);

    const response = await fetch(request);
    const superHeroes = await response.json();

    populateHeader(superHeroes);
    populateHeroes(superHeroes);
}
```

- we declare the `requestURL` variable to store the GitHub URL
- we use the URL to initialize a new `Request` object.
- we make the network request using the `fetch()` function, and this returns a `Response` object
- we retrieve the response as JSON using the `json()` function of the `Response` object.

### Populating the header

```js
function populateHeader(obj) {
    const header = document.querySelector("header");
    const myH1 = document.createElement("h1");
    myH1.textContent = obj.squadName;
    header.appendChild(myH1);

    const myPara = document.createElement("p");
    myPara.textContent = `Hometown: ${obj.homeTown} // Formed: ${obj.formed}`;
    header.appendChild(myPara);
}
```

### Creating the hero information cards

```js
function populateHeroes(obj) {
    const section = document.querySelector("section");
    const heroes = obj.members;

    for (const hero of heroes) {
        const myArticle = document.createElement("article");
        const myH2 = document.createElement("h2");
        const myPara1 = document.createElement("p");
        const myPara2 = document.createElement("p");
        const myPara3 = document.createElement("p");
        const myList = document.createElement("ul");

        myH2.textContent = hero.name;
        myPara1.textContent = `Secret identity: ${hero.secretIdentity}`;
        myPara2.textContent = `Age: ${hero.age}`;
        myPara3.textContent = "Superpowers:";

        const superPowers = hero.powers;
        for (const power of superPowers) {
            const listItem = document.createElement("li");
            listItem.textContent = power;
            myList.appendChild(listItem);
        }

        myArticle.appendChild(myH2);
        myArticle.appendChild(myPara1);
        myArticle.appendChild(myPara2);
        myArticle.appendChild(myPara3);
        myArticle.appendChild(myList);

        section.appendChild(myArticle);
    }
}
```

### Calling the top-level function

Finally, we need to call our top-level `populate()` function:

```js
populate();
```

---

## Converting between objects and text

The above example was simple in terms of accessing the JavaScript object, because we converted the network response directly into a JavaScript object using `response.json()`.

But if we receive a *raw JSON string*, we need to convert it to an object ourselves. And when we want to send a JavaScript object across the network, we need to convert it to JSON (a string) before sending it.

The built-in `JSON` object is available in browsers, which contains the following two methods:

- `parse()`: Accepts a JSON string as a parameter, and returns the corresponding JavaScript object.
- `stringify()`: Accepts an object as a parameter, and returns the equivalent JSON string.

So the top-level function in above example can be rewritten like this:

- we retrieve the response as text rather than JSON, by calling the `text()` method of the response.
- we then use `parse()` to convert the text to a JavaScript object.

```js
async function populate() {
    const requestURL =
        "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json";
    const request = new Request(requestURL);

    const response = await fetch(request);
    const superHeroesText = await response.text();
    const superHeroes = JSON.parse(superHeroesText);

    populateHeader(superHeroes);
    populateHeroes(superHeroes);
}
```

`stringify()` works the opposite way. For example:

```js
let myObj = { name: "Chris", age: 38 };
myObj;
let myString = JSON.stringify(myObj);
myString;
```



---

?> {docsify-updated}