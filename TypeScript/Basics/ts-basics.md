# TypeScript basics

1. [Basic types](#basic-types)
2. [Custom types and interfaces](#custom-types-and-interfaces)
3. [Functions](#functions)
4. [Classes](#classes)
5. [Enums](#enums)
6. [Generics](#generics)

---

## Basic types

-   **boolean** <br>

```ts
const isLoading: boolean = true;
```

-   **string** <br>

```ts
const message: string = "Hello World!";
```

-   **number** <br>

```ts
const year: number = 2022;
const exp: number = 2.718;
```

-   **array** <br>
    _There are some ways to declare an array_

```ts
const nums: number[] = [1, 2, 3, 4, 5]; // only numbers
const products: Array<string> = ["bread", "milk"]; // only strings
const someValues: [string, boolean] = ["ts", true]; // only 1 string and 1 boolean
```

-   **any** <br>
    _Allows to disable type checking, as a result the variable can dynamically change it's type. Avoid `any` in your code._

```ts
let value: any = "this is string";
value = 107;
value = false;
value = [1, 2, "a", "b", true];
```

---

## Custom types and interfaces

-   **Type Aliases** <br>
    _Good for describing types in simple objects or for variables that may have more than one type._

```ts
type Animal = {
    name: string;
    age: number;
};

const animal: Animal = {
    name: "Fluffy",
    age: 4,
};
```

```ts
// extending a type
type Cat = Animal & {
    color: string;
};
```

```ts
// value with 2 types
type ID = string | number;

const userId: ID = 239053;
const itemId: ID = "A934VL";
```

-   **Interfaces** <br>
    _An interface declaration is another way to name an object type. Interfaces support a more convenient extension and are used more often._

```ts
interface IPerson {
    firstName: string;
    lastName?: string; // an optional parameter
    gender: "female" | "male"; // only certain values
    isMarried: boolean;
}

//Extending an interface
interface IWorker extends IPerson {
    job: string;
}

const someone: IWorker = {
    firstName: "Alex",
    gender: "male",
    isMarried: true,
    job: "engineer",
};
```

---

## Functions

-   **Basic usage** <br>
    _We can describe the types of function arguments as well as the return value_

```ts
// type "void" means that our function does not return anything
function logInfo(name: string, age: number): void {
    console.log(`My name is ${name}, I'm ${age} y.o.`);
}

// Arrow function
const square = (x: number): number => x * x;
```

-   **Default arguments** <br>
    _When default parameters are specified, their types are automatically determined by the passed values_

```ts
function getNumbers(max: number = 99, min = 1): void {}
```

-   **Optional arguments** <br>

```ts
function greeting(name?: string): void {
    if (name) {
        console.log(`Welcome, ${name}!`);
    } else {
        console.log(`Welcome, annonymous user!`);
    }
}
```

-   **Unlimited arguments** <br>
    _You can describe an indefinite number of arguments of the same type using spread operator_

```ts
const logValues = (x: number, ...values: string[]): void =>
    console.log(x, ...values);

logValues(77, "one", "two", "three", "...");
```

-   **Function type** <br>
    _Use function type to describe methods_

```ts
interface IService {
    calcSum: (a: number, b: number) => number;
    getBalance: () => string;
    sendFeedback: (mes: string) => void;
}
```

---

## Classes

-   **Modifiers** <br>
    _Various modifiers allow you to define the scope of variables and methods_

```ts
class Example {
    constructor(a: number, b: number) {
        this.a = a;
        this.b = b;
    }

    /* prevents assignments to the field outside 
    of the constructor */
    readonly a: number;

    /* visible only inside classes inherited from 
    the current class (not from outside) */
    protected b: number;

    /* visible only inside current class 
    (not from inherited and outside) */
    private secret = "hello";

    alert = () => {};
}
```

-   **Extending a class** <br>
    _Classes can easily be extended by adding new variables/methods. This also supports overriding methods, but in a way that ensures backward compatibility._

```ts
class NewExmaple extends Example {
    constructor(a: number, b: number, c: number) {
        super(a, b);
        this.c = c;
    }

    c: number;

    alert(name?: string) {
        console.log(`Hello ${name}`);
    }
}
```

-   **Abstract classes** <br>
    _Abstract classes/methods do not allow you to create instances, but only serve for expansion_

```ts
abstract class Somebody {
    hello(): void {
        console.log("Hello!");
    }
}

class User extends Somebody {
    introduce(): void {
        console.log("I am User!");
    }
}

const user = new User();
user.hello(); // "Hello!"
```

-   **Interface implementation** <br>
    _Interfaces can be used to describe classes_

```ts
interface ITest {
    value: string;
    getNumber: () => number;
}

class Test implements ITest {
    value = "test";
    getNumber = () => 7;
}
```

---

## Enums

-   **Numeric enums** <br>
    _Enums allow to define a set of named constants. Numeric enums automatically assign numbers to named constants._

```ts
enum Roles {
    user, // Roles.user = 0
    moderator, // Roles.moderator = 1
    admin, // Roles.admin = 2
}

enum Services {
    GitHub = 10, // Services.Github = 10
    Google, // Services.Google = 11
    Amazon, // Services.Amazon = 12
}
```

-   **String & mixed enums** <br>

```ts
enum Bool {
	yes = "YES",
	no = "NO"
}

enum Server {
    host = "server.com"
    port = 5432
}
```

---

## Generics

-   **Basic usage** <br>
    _Generics allows to create a component that can work over a variety of types rather than a single one_

```ts
function test<T>(value: T): T {
    return value;
}
// "T" will be replaced by the type we specified

test<string>("Hello World");
test<number>(2022);
test<boolean>(true);
```

-   **Type checking** <br>
    _You can safely use type checking with the `typeof` operator to execute the appropriate logic_

```ts
function logger<T>(value: T): void {
    if (typeof value == "string") {
        // we are pretty sure that only strings will get here
        console.log(value.toLocaleUpperCase());
        // therefore, we can use string methods
    } else if (typeof value == "number") {
        console.log(value.toFixed(2));
    } else {
        console.log(`${value} has the ${typeof value} type`);
    }
}

logger<string>("Hello World"); // "HELLO WORLD"
logger<number>(2022); // 2022.00
logger<boolean>(true); // "true has the boolean type"
```

-   **Multiple generics** <br>
    _You can pass multiple generics, for example, to describe different input and output types in functions_

```ts
interface IService {
    process: <T, S>(data: T) => S;
}
```

-   **Extending generic type** <br>

```ts
interface IValue {
    info: string;
}

function test<T extends IValue>(value: T): T {
    console.log(value.info);
    return value;
}
```
