# 07-Classes in JavaScript

> To understand how to use the features JavaScript provides to implement "classical" object-oriented programs.

---

## Classes and constructors

`class`, `constructor`, `this`, `new`

```js
class Person {
    name;

    constructor(name) {
        this.name = name;
    }

    introduceSelf() {
        console.log(`Hi! I'm ${this.name}`);
    }
}

const giles = new Person("Giles");
giles.introduceSelf();  // Hi! I'm Giles
```

### Omitting constructors

If you don't need to do any special initialization, you can omit the constructor, and a default constructor will be generated for you:

```js
class Animal {
    sleep() {
        console.log("zzzzzzz");
    }
}

const spot = new Animal();
spot.sleep(); // 'zzzzzzz'
```

---

## Inheritance

`extends`, `super`

```js
class Professor extends Person {
    teaches;

    constructor(name, teaches) {
        super(name);
        this.teaches = teaches;
    }

    introduceSelf() {
        console.log(
            `My name is ${this.name}, and I will be your ${this.teaches} professor.`,
        );
    }

    grade(paper) {
        const grade = Math.floor(Math.random() * (5 - 1) + 1);
        console.log(grade);
    }
}

const walsh = new Professor("Walsh", "Psychology");
walsh.introduceSelf(); // 'My name is Walsh, and I will be your Psychology professor'
walsh.grade("my paper"); // some random grade
```

---

## Encapsulation

### Private fields

Private fields must be declared in the class declaration, and their names start with `#`.

```js
class Student extends Person {
    #year;

    constructor(name, year) {
        super(name);
        this.#year = year;
    }

    introduceSelf() {
        console.log(`Hi! I'm ${this.name}, and I'm in year ${this.#year}.`);
    }

    canStudyArchery() {
        return this.#year > 1;
    }
}

const summers = new Student("Summers", 2);
summers.introduceSelf();    // Hi! I'm Summers, and I'm in year 2.
summers.canStudyArchery();  // true
```

### Private methods

You can have private methods as well as private fields. Just like private fields, their names start with `#`, and they can only be called by the object's own methods.

```js
class Example {
    #somePrivateMethod() {
        console.log("You called me?");
    }

    somePublicMethod() {
        this.#somePrivateMethod();
    }
}

const myExample = new Example();
myExample.somePublicMethod(); // 'You called me?'
```

### Static methods and fields

The `static` keyword defines a static method or field for a class. Static properties (fields and methods) are defined on the class itself instead of each instance. Static methods are often used to create utility functions for an application, whereas static fields are useful for caches, fixed-configuration, or any other data that doesn't need to be replicated across instances.

```js
class Point {
    x;
    y;

    constructor(x, y) {
        this.x = x;
        this.y = y;
    }

    static displayName = "Point";
    static distance(a, b) {
        const dx = a.x - b.x;
        const dy = a.y - b.y;
        return Math.hypot(dx, dy);
    }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);
p1.displayName; // undefined
p1.distance;    // undefined
p2.displayName; // undefined
p2.distance;    // undefined

console.log(Point.displayName);         // "Point"
console.log(Point.distance(p1, p2));    // 7.0710678118654755
```

---

## getter and setter

`get`, `set`

```js
class Rectangle {
    #width;
    #height;

    constructor(width, height) {
        this.#width = width;
        this.#height = height;
    }

    // A `getter` must have exactly `zero` parameters.
    // Getter can be viewed as a `dynamic computational property`
    get area() {
        return this.#calcArea();
    }

    // A `setter` must have exactly `one` parameter.
    set area(area) {
        this.#height = area / this.#width;
    }

    #calcArea() {
        return this.#width * this.#height;
    }
}

const rec = new Rectangle(3, 4);

// Access a getter without parentheses
console.log(rec.area);  // 12

rec.area = 15;
console.log(rec.area);  // 15
```



---

?> {docsify-updated}