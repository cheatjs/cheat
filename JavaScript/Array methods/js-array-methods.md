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

## Search among elements

-   indexOf/lastIndexOf(item, pos) <br>
    look for `item` starting from index `pos`, return the index or -1 if not found. Method `lastIndexOf()` searches from right to left

```js
const arr = [10, 20, 20, 30];
const first = arr.indexOf(20); // first = 1
const last = arr.lastIndexOf(20); // last = 2
```

-   includes(value) <br>
    returns true if the array has value, else false

```js
const arr = [10, 20, 30, 40];
const n = arr.includes(15); // false
```

-   find/findIndex(func(item, index, arr)) <br>
    `func()` is called for each element of the array. If the `func()` returns true, the search is interrupted and item is returned, else - undefined

```js
const arr = [1, 13, 23, 43, 56, 71, 97]
const evenNum = arr.find(item => {
    return % 2 === 0
})
// evenNum = 56
```

-   filter(func(item, index, arr)) <br>
    the method is similar to `find()`, but `filter()` returns an array of all matching elements

```js
const arr = [1, 2, 3, 4, 5, 6, 7];
const evenArr = arr.filter((item) => {
    return item % 2 === 0;
}); // evenArr = [2, 4, 6]
```

## Iteration of elements

-   forEach(func(item, index, array)) <br>
    calls `func()` for every element in array, does not return anything

```js
const arr = [1, 2, 3];
arr.forEach((item, index, arr) => {
    console.log(item, index, arr);
});
// 1 0 [1, 2, 3]
// 2 1 [1, 2, 3]
// 3 2 [1, 2, 3]
```

## Transform the array

-   map(func(item, index, array)) <br>
    calls the `func()` for each element of the array and returns the array of results

```js
const arr = [1, 2, 3, 4, 5];
const newArr = arr.map((item) => {
    return item * 10;
});
// newArr = [10, 20, 30, 40, 50]
```

-   sort(func()) <br>
    sorts the array changing it's element order, `func()` defining the sorting order (optional).

```js
const arr = [25, 7, 13 31]
arr.sort((a, b) => {
    return a - b
})
// arr = [7, 13, 25, 31]
```

-   reverse() <br>
    reverse the order of the elements of the current array

```js
const arr = [1, 2, 3, 4, 5];
arr.reverse();
// arr = [5, 4, 3, 2, 1]
```

-   join(separator)/string.split(separator) <br>
    convert an array to string / a string to array

```js
const str = "one, two, three, four";
const arr = str.split(", ");
// arr = ["one", "two", "three", "four"]
const newStr = arr.join("-");
// newStr = "one-two-three-four"
```

-   reduce/reduceRight(func(accumulator, current, index, array), initial) <br>
    calculate a single value over the array by calling `func()` for each element and passing an intermediate result between the calls

```js
const arr = [1, 2, 3, 4, 5];
const sumFromElements = arr.reduce((sum, current) => {
    return sum + current;
}, 0);
// sumFromElements = 15
```
