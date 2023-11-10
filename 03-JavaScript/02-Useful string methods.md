# 02-Useful string methods

> To understand that strings are objects, and learn how to use some of the basic methods available on those objects to manipulate strings.

---

## Finding the length of a string

`length` property.

```js
const browserType = "mozilla";
browserType.length; // 7
```

## Retrieving a specific string character

`[]` square bracket.

```js
const browserType = "mozilla";

// Get the first character
browserType[0]; // "m"

// Get the last character
browserType[browserType.length - 1]; // "a"
```

## Testing if a string contains a substring

Three methods that return `true` or `false`:

- `includes()`
- `startsWith()`
- `endsWith()`

```js
const browserType = "mozilla";

browserType.includes("zilla");      // true
browserType.startsWith("zilla");    // false
browserType.endsWith("zilla");      // true
```

## Finding the position of a substring in a string

`indexOf()` method.

```js
const tagline = "MDN - Resources for developers, by developers";
tagline.indexOf("developers");  // 20
tagline.indexOf("x");           // -1

const firstOccurrence = tagline.indexOf("developers");
const secondOccurrence = tagline.indexOf("developers", firstOccurrence + 1);
firstOccurrence;    // 20
secondOccurrence;   // 35
```

## Extracting a substring from a string

`slice()` method.

```js
const browserType = "mozilla";

browserType.slice(1, 4); // "ozi"
browserType.slice(2); // "zilla"
```

## Changing case

Two methods:

- `toLowerCase()`
- `toUpperCase()`

```js
const radData = "My NaMe Is MuD";
radData.toLowerCase();
radData.toUpperCase();
```

## Updating parts of a string

Two methods:

- `replace()`
- `replaceAll()`

```js
const browserType = "mozilla";
const updated = browserType.replace("moz", "van");

updated;        // "vanilla"
browserType;    // "mozilla"
```

Note that `replace()`, like many string methods, **doesn't change the string it was called on**, but returns a new string.

```js
let quote = "To be or not to be";
quote = quote.replaceAll("be", "code");

quote;  // "To code or not to code"
```



---

?> {docsify-updated}