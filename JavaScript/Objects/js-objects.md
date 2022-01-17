# Objects cheatsheet

## Table of content

---

## Basic usage

Objects are used to store keyed collections of various data and more complex entities.

```js
const app = {
    name: "todo",
    version: 1.2,
};

alert(app.name); // todo
alert(app.version); // 1.2

app.version = 1.3; // update value
app.license = "MIT"; // add new property
delete app.version; // delete property
```

-   **Multiword property name**

```js
const game = {
    name: "sudoku",
    "is free": true,
};

alert(game["is free"]); // true

const isFree = "is free";
alert(game[isFree]); // true
```

-   **Computed property**

```js
let prop = "yEaR";
prop = prop.toLowerCase();

const list = {
    [prop]: 2022,
};

alert(list.year); // 2022
```

-   **Property value shorthand**

```js
function createUser(login, id) {
    return {
        login, // the same login: login
        id, // the same id: id
    };
}
```

---

## References and copying

-   **Copying objects** <br>
    _When copied, the new object will be a reference to the original object, unlike regular variables, which create independent entities when copied_

```js
const original = {
    name: "origin",
    id: 1,
};

const copy = original;

alert(copy.name); // origin
alert(copy.id); // 1

copy.name = "new copy"; // it also changes original

alert(original.name); // new copy
```

-   **Object comparison** <br>
    _The comparison operators `==` and `===` work the same for objects_

```js
// Two variables refer to the same object
const original = {};
const copy = original;

alert(original == copy); // true
```

```js
// Two independent objects
const original = {};
const otherOriginal = {};

alert(original == otherOriginal); // false
```

-   **Cloning objects** <br>
    _`Object.assign(target, ...sources)` - copies all enumerable own properties from one or more source objects to a target object._

```js
const item = {
    name: "monitor",
    color: "black",
};

const newItem = Object.assign({}, item);

newItem.color = "gray";

alert(newItem.color); // gray
alert(item.color); // black
```

---

## Iterating objects

-   Loop **for...in**

```js
const item = {
    name: "Pizza",
    price: 29,
};

for (key in item) {
    alert(`${key} - ${item[key]}`);
    // name - Pizza
    // price - 29
}
```

-   **Object.keys**(object) <br>
    _Returns an array of keys of the passed object_

```js
console.log(Object.keys(item));
// [name, price]
```

-   **Object.values**(object) <br>
    _Returns an array of values of the passed object_

```js
console.log(Object.values(item));
// ["Pizza", 29]
```

-   **Object.entries**(object) <br>
    _Returns an array of the [key, value] pairs of the passed object_

```js
console.log(Object.entries(item));
// [["name", "Pizza"], ["price", 29]]
```

---

## Object methods & this

-   **Object methods** <br>
    _In addition to values, objects can have methods that perform various actions_

```js
const greetings = {
    hiMorning() {
        alert("Good morning!");
    },
    hiDay() {
        alert("Good afternoon!");
    },
    hiEvening() {
        alert("Good evening!");
    },
};

greetings.hiDay(); // Good afternoon!
```

-   **this** <br>
    _`this` allows to refer to variables and methods that are stored in the same object_

```js
const counter = {
    value: 0,
    inc() {
        this.value++;
    },
    dec() {
        this.value--;
    },
};

counter.inc(); // counter.value = 1
counter.inc(); // counter.value = 2
counter.dec(); // counter.value = 1
```

_`this` is simply a reference to the object in the context of which it was called_

```js
const obj = {
    value: "hello",
    log() {
        console.log(this);
    },
};

obj.log(); // { value: 'hello', log: [Function] }
```

---

## Constructors

-   **Constructor functions** <br>
    _Constructor functions are used to easily create objects. They are normal functions, but developers have agreed that such functions are capitalised and called with `new` operator._

```js
function Animal(type, color) {
    this.type = type;
    this.color = color;
}

const kitten = new Animal("cat", "black");
alert(kitten.type); // cat
alert(kitten.color); // black
```

-   **Methods in constructors**

```js
function Parrot(name) {
    this.name = name;
    this.greet = function () {
        alert(`Hello, my name is ${this.name}`);
    };
}

const blueParrot = new Parrot("Mojo");
blueParrot.greet(); // Hello, my name is Mojo
```

---

## Property existance

-   **Checking property existence**

```js
const response = {
    data: "secret info",
    status: 200,
};

console.log("data" in response); // true
console.log("message" in response); // false
```

-   **Optional chaining** <br>
    _Is a safe way to access nested object properties, even if an intermediate property doesn’t exist_

```js
const response = {
    data: "some data",
};

console.log(response?.data); // some data
console.log(response?.message); // undefined
```

---

## Property flags and descriptors

Object properties can store a special configuration flags in addition to the value.<br>

**`writable`** – if `true`, the value can be changed, otherwise it’s read-only. <br>
**`enumerable`** – if `true`, then listed in loops, otherwise not listed. <br>
**`configurable`** – if `true`, the property can be deleted and these attributes can be modified, otherwise not.

> All flags default to true

-   Object.**getOwnPropertyDescriptor**(obj, property) <br>
    _Allows to query the full information about a property_

```js
const person = {
    name: "Bill",
    surname: "Gates",
};

let descriptor = Object.getOwnPropertyDescriptor(person, "name");

console.log(descriptor);
// {
//    configurable: true
//    enumerable: true
//    value: Bill
//    writable: true
// }
```

-   Object.**defineProperty**(obj, property, descriptor) <br>
    _Change the flags of the specified property_

```js
Object.defineProperty(person, "name", {
    writable: false,
});
```

-   Object.**defineProperties**(obj, {prop: descr, ...}) <br>
    _Allows to define many properties at once_
-   Object.**getOwnPropertyDescriptors**(obj) <br>
    _Get all property descriptors at once_

---

## Getters and setters

Getters and setters called as accessor properties. They are essentially functions that execute on getting and setting a value, but look like regular properties to an external code.

-   **Usage** <br>
    _The `get` keyword is used to create the getter, for the setter - `set`_

```js
const person = {
	name: "Bill",
	surname: "Gates",
	get fullName() {
		return `${this.name} ${this.surname}`
	}
	set fullName(value) {
		[this.name, this.surname] = value.split(" ")
	}
}

alert(person.fullName) // Bill Gates

person.fullName = "Jack Ma"
console.log(person)
// {fullName: "Jack Ma", name: "Jack", surname: "Ma"}
```

-   **Accessor descriptors** <br>
    _For accessor properties, there is no `value` or `writable`, but instead there are `get` and `set` functions_

```js
Object.defineProperty(person, "sayHello", {
    get() {
        return `Hello, I'm ${this.name}`;
    },
    enumerable: false,
    configurable: true,
});
```
