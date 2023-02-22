# Classes cheatsheet

[Download image version](js-classes.png)

## Basic usage

Classes provide a simpler, more intuitive way of creating objects and organising inheritance.

```js
class Element {
    height = 10;
    width = 10;
    calcArea() {
        return this.height * this.width;
    }
}

const element = new Element();
element.height; // 10
element.width; // 10
element.calcArea(); // 100
```

`Сonstructor` is a special method required to initialise the passed values.

```js
class Element {
    constructor(width, height) {
        this.width = width;
        this.height = height;
    }
    calcArea() {
        return this.height * this.width;
    }
}

const rectangle = new Element(20, 30);
const square = new Element(25, 25);
```

---

## Сlass inheritance

For class inheritance is used the keyword `extends`, `super` is used to pass values to the parent constructor

```js
class Element {
    constructor(margin) {
        this.margin = margin;
    }
}

class Square extends Element {
    constructor(margin, size) {
        super(margin); // pass to Element
        this.size = size;
    }
    calcArea() {
        return Math.pow(this.size, 2);
    }
}

const box = new Square(0, 50);
box.margin; // 0
box.size; // 50
box.calcArea(); // 2500
```

Inherited methods can be completely overwritten

```js
class Circle extends Square {
    borserRadius = "100%";
    constructor(margin, size) {
        super(margin, size);
    }
    // Method overwriting
    calcArea() {
        const radius = this.size / 2;
        return (Math.PI * Math.pow(radius, 2)).toFixed(2);
    }
}

const circle = new Circle(0, 70);
circle.calcArea(); // 3848.45
circle.borserRadius; // 100%
```

`super` keyword can call the parent version of the method

```js
class Logger {
    log() {
        console.log("Log to console...");
    }
}

class ExtLogger extends Logger {
    log() {
        super.log(); // from Logger
        console.log("process...");
    }
}

const logger = new ExtLogger();
logger.log();
// Log to console...
// process...
```

---

## Getters & setters

Getters and setters work in the same way as in objects. They are essentially functions that execute on getting and setting a value, but look like regular properties to an external code.

```js
class Square {
    constructor(size) {
        this.size = size;
    }

    get area() {
        return Math.pow(this.size, 2);
    }

    set area(value) {
        this.size = Math.sqrt(value);
    }
}

const box = new Square(4);
console.log(box.size); // 4
console.log(box.area); // 16

box.area = 100;
console.log(box.size); // 10
```

---

## Static methods & properties

Static methods/properties are called without creating an instance of their class.

```js
class Calc {
    static pi = 3.14;

    static sum(a, b) {
        return a + b;
    }
    avg(a, b) {
        // "this" is not available!
        return Calc.sum(a, b) / 2;
    }
}

console.log(Calc.pi); // 3.14
Calc.sum(20, 30); // 50
```

Static properties/methods are not available for instances.

```js
const proc = new Calc();

console.log(proc.avg(2, 3)); // 2.5
console.log(proc.pi); // undefined
proc.sum(10, 15); // ERROR
```

But static properties/methods can be inherited

```js
class Process extends Calc {}
Process.sum(2, 3); // 5
```

---

## Operator instanceof

The `instanceof` operator allows to check whether an object belongs to a certain class

```js
class Square {}
class Circle extends Square {}

const box = new Square();
console.log(box instanceof Square); // true
console.log(box instanceof Circle); // false
```

It also works with function-constructors

```js
class Process extends Calc {}
Process.sum(2, 3); // 5

const newProc = new Process();
console.log(newProc.avg(3, 4)); // 3.5
```

---

## Mixins

Mixin is just objects. They are used to add additional properties/methods to existing classes. The mixins themselves are not used.

```js
class Square {
    constructor(size) {
        this.size = size;
    }
}

const areaMixin = {
    area() {
        console.log(Math.pow(this.size, 2));
    },
};

// Copying methods from a mixin to a class
Object.assign(Square.prototype, areaMixin);

const box = new Square(5);
box.area(); // 25
```
