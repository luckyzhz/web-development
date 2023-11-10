# 05-JavaScript object basics

> To understand the basics of working with objects in JavaScript: creating objects, accessing and modifying object properties, and using constructors.

---

## Object literal

```js
const person = {
    name: ["Bob", "Smith"],
    age: 32,
    bio: function () {
        console.log(`${this.name[0]} ${this.name[1]} is ${this.age} years old.`);
    },
    introduceSelf: function () {
        console.log(`Hi! I'm ${this.name[0]}.`);
    },
};
```

---

## Access object's members

### Dot notation

```js
person.age;     // 32
person.bio();   // Bob Smith is 32 years old.
```

### Bracket notation

```js
person["age"];  // 32
person["name"]; // [ "Bob", "Smith" ]
```

This looks very similar to how you access the items in an array. It is no wonder that objects are sometimes called **associative arrays** — they map strings to values in the same way that arrays map numbers to values.

There are some cases where you have to use square brackets. For example, if an object **property name is held in a variable**.

```js
const person = {
    name: ["Bob", "Smith"],
    age: 32,
};

function logProperty(propertyName) {
    console.log(person[propertyName]);
}

logProperty("name");    // ["Bob", "Smith"]
logProperty("age");     // 32
```

---

## Setting object members

We can not only update the value of existing members but also create completely new members.

```js
// update member
person.age = 45;

// add new members
person["eyes"] = "hazel";
person.farewell = function () {
    console.log("Bye everybody!");
};
```

---

## Introducing constructors

```js
function Person(name) {
    this.name = name;
    this.introduceSelf = function () {
        console.log(`Hi! I'm ${this.name}.`);
    };
}

const salva = new Person("Salva");
salva.introduceSelf();      // "Hi! I'm Salva."

const frankie = new Person("Frankie");
frankie.introduceSelf();    // "Hi! I'm Frankie."
```



---

?> {docsify-updated}