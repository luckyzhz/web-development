# 03-Arrays

> To understand how to manipulate array in JavaScript.

---

## Finding the length of an array

`length` property.

```js
const shopping = ["bread", "milk", "cheese", "hummus", "noodles"];
shopping.length;    // 5
```

## Finding the index of items in an array

`indexOf()` method.

```js
const birds = ["Parrot", "Falcon", "Owl"];
birds.indexOf("Owl");       // 2
birds.indexOf("Rabbit");    // -1
```

## Adding items

Two methods:

- `push()`: add one or more items to the **end** of an array.
- `unshift()`: add one or more items to the **start** of an array.

```js
const cities = ["Manchester", "Liverpool"];

cities.push("Bradford", "Brighton");
cities; // [ "Manchester", "Liverpool", "Bradford", "Brighton" ]

cities.unshift("Cardiff");
cities; // [ "Cardiff", "Manchester", "Liverpool", "Bradford", "Brighton" ]
```

## Removing items

Three methods:

- `pop()`: remove the **last** item from the array.
- `shift()`: remove the **first** item from the array.
- `splice()`: remove one or more items from the specified index.

```js
const cities = ["Manchester", "Liverpool"];
const removedCity = cities.pop();
cities;         // [ "Manchester" ]
removedCity;    // "Liverpool"
```

```js
const cities = ["Manchester", "Liverpool"];
const removedCity = cities.shift();
cities;         // [ "Liverpool" ]
removedCity;    // "Manchester"
```

```js
const cities = ["Manchester", "Liverpool", "Edinburgh", "Carlisle"];
const index = cities.indexOf("Liverpool");
const removedCities = cities.splice(index, 2);
cities;         // [ "Manchester", "Carlisle" ]
removedCities;  // [ "Liverpool", "Edinburgh" ]
```

## Accessing every item

`for...of` statement.

```js
const birds = ["Parrot", "Falcon", "Owl"];

for (const bird of birds) {
    console.log(bird);
}
```

`map()` method.

```js
function double(number) {
    return number * 2;
}
const numbers = [5, 2, 7, 6];
const doubled = numbers.map(double);
doubled;    // [ 10, 4, 14, 12 ]
```

`filter()` method.

```js
function isLong(city) {
    return city.length > 8;
}
const cities = ["London", "Liverpool", "Totnes", "Edinburgh"];
const longer = cities.filter(isLong);
longer; // [ "Liverpool", "Edinburgh" ]
```

## Converting between strings and arrays

Three methods:

- `split()`: a string method.
- `join()`
- `toString()`

```js
const data = "Manchester,London,Liverpool,Birmingham,Leeds,Carlisle";
const cities = data.split(",");
cities; // [ "Manchester", "London", "Liverpool", "Birmingham", "Leeds", "Carlisle" ]
cities.join(" ");   // "Manchester London Liverpool Birmingham Leeds Carlisle"
cities.toString();  // "Manchester,London,Liverpool,Birmingham,Leeds,Carlisle"
```



---

?> {docsify-updated}