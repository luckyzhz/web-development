# 06-Object prototypes

> To understand JavaScript object prototypes, how prototype chains work, and how to set the prototype of an object.

---

## The prototype chain

This is a constructor `Dog`. We can use it to create many dog objects (instances) using the keyword `new`. The downside is that the code of the method `bark()` will be duplicated many times, but actually they are exactly the same.

```js
function Dog(name, breed, weight) {
    this.name = name;
    this.breed = breed;
    this.weight = weight;

    this.bark = function () {
        let msg = "";
        if (this.weight > 25) {
            msg = `${this.name} says Woof!`;
        } else {
            msg = `${this.name} says Yip!`;
        }
        alert(msg);
    };
}
```

We can use prototype inheritance to solve the problem above:

```js
// Put properties with `unique values` for each instance in the constructor.
function Dog(name, breed, weight) {
    this.name = name;
    this.breed = breed;
    this.weight = weight;
}

// Add properties or methods common to each instance to the constructor's prototype.
// `Dog.prototype` is essentially an object.
Dog.prototype.species = "Canine";
Dog.prototype.bark = function () {
    let msg = "";
    if (this.weight > 25) {
        msg = `${this.name} says Woof!`;
    } else {
        msg = `${this.name} says Yip!`;
    }
    alert(msg);
};

// As before, instances are created using constructors.
const fido = new Dog("Fido", "Mixed", 38);
console.log(fido.species);  // "Canine"
// `this` in the method of prototype will point to the current instance correctly.
fido.bark();    // Fido says Woof!
```

Here's the illustration:

![](../_assets/_images/prototype.svg ':size=400')

When `fido.bark()` is executed, it first looks up in the fido instance to see if there is a `bark()` method, and if there isn't, it looks up in the prototype.

---

## Shadowing properties

We can **shadow** the prototype property by setting a property with the same name in the instance without affecting other instances' references to the prototype property.

```js
const spot = new Dog("Spot", "Chihuahua", 10);

// Set `bark` method in instance to shadow the `bark` method in prototype
spot.bark = function () {
    console.log(`${this.name} says WOOF WOOF!`);
}

// Since the instance has a `bark` method, we don't need to go up to the prototype to find that method.
spot.bark();    // Spot says WOOF WOOF!
```

?> ⚠️ **Note**: One memory-saving technique is to set the default value of a property in the prototype, and then add a property of the same name to an instance when that default value needs to be changed.



---

?> {docsify-updated}