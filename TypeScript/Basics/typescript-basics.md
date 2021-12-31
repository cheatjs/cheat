# TypeScript basics

---

## Basic types

-   **boolean**

```ts
const isLoading: boolean = true;
```

-   **string**

```ts
const message: string = "Hello World!";
```

-   **number**

```ts
const year: number = 2022;
const exp: number = 2.718;
```

-   **array**
    _There are some ways to declare an array_

```ts
const nums: number[] = [1, 2, 3, 4, 5]; // only numbers
const products: Array<string> = ["bread", "milk"]; // only strings
const someValues: [string, boolean] = ["ts", true]; // only 1 string and 1 boolean
```

-   **any**
    _Allows to disable type checking, as a result the variable can dynamically change it's type. Avoid `any` in your code._

```ts
let value: any = "this is string";
value = 107;
value = false;
value = [1, 2, "a", "b", true];
```

---

## Custom types and interfaces

-   **Type Aliases**
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

_You can extending a type_

```ts
type Cat = Animal & {
    color: string;
};
```

```ts
type ID = string | number;

const userId: ID = 239053;
const itemId: ID = "A934VL";
```

-   **Interfaces**
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
