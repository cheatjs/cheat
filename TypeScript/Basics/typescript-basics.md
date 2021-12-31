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
