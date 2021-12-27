# Array methods cheatsheet

## Adding/Removing elements

-   push(...items) <br>
    add elements to the end

```js
const arr = [1, 2, 3];
arr.push(4);
// arr = [1, 2, 3, 4]
```

-   pop() <br>
    extracts an element from the end

```js
const arr = [1, 2, 3];
arr.pop();
// arr = [1, 2]
```

-   unshift(...items) <br>
    add items to the beginning (bad for performance)

```js
const arr = [1, 2, 3];
arr.unshift(0);
// arr = [0, 1, 2, 3]
```

-   shift() <br>
    extracts from the beginning

```js
const arr = [1, 2, 3];
arr.shift();
// arr = [2, 3]
```

-   concat(...items) <br>
    returns a new array: copy of the current array + `items`

```js
const arr = [1, 2, 3];
const newArr = arr.concat(4, 5);
const newArr2 = newArr.concat([6, 7]);
// newArr2 = [1, 2, 3, 4, 5, 6, 7]
```

-   splice(pos, count, ...items) <br>
    at index `pos` deletes `count` elements and inserts `items`

```js
const arr = ["a", "*", "*", "d"];
arr.splice(1, 2, "b", "c");
// arr = ['a', 'b', 'c', d']
```

-   slice(start, end) <br>
    creates a new array, copies elements from index `start` till `end` (not inclusive) into it

```js
const arr = [1, 2, 3, 4, 5];
const newArr = arr.slice(1, 4);
// newArr = [2, 3, 4]
```
