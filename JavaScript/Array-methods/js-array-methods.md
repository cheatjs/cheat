# Array methods cheatsheet

1. [Adding/Removing elements](js-array-methods.md#addingremoving-elements)
2. [Search among elements](js-array-methods.md#search-among-elements)
3. [Iteration of elements](js-array-methods.md#iteration-of-elements)
4. [Transform the array](js-array-methods.md#transform-the-array)
5. [Bonus](js-array-methods.md#bonus)

***

## Adding/Removing elements

* **push**(...items)\
  _add `items` to the end_

```js
const arr = [1, 2, 3];
arr.push(4);
// arr = [1, 2, 3, 4]
```

* **pop**()\
  _extracts an element from the end_

```js
const arr = [1, 2, 3];
arr.pop();
// arr = [1, 2]
```

* **unshift**(...items)\
  _add `items` to the beginning (bad for performance)_

```js
const arr = [1, 2, 3];
arr.unshift(0);
// arr = [0, 1, 2, 3]
```

* **shift**()\
  _extracts from the beginning_

```js
const arr = [1, 2, 3];
arr.shift();
// arr = [2, 3]
```

* **concat**(...items)\
  _returns a new array: copy of the current array + `items`_

```js
const arr = [1, 2, 3];
const newArr = arr.concat(4, 5);
const newArr2 = newArr.concat([6, 7]);
// newArr2 = [1, 2, 3, 4, 5, 6, 7]
```

* **splice**(pos, count, ...items)\
  _at index `pos` deletes `count` elements and inserts `items`_

```js
const arr = ["a", "*", "*", "d"];
arr.splice(1, 2, "b", "c");
// arr = ['a', 'b', 'c', d']
```

* **slice**(start, end)\
  _creates a new array, copies elements from index `start` till `end` (not inclusive) into it_

```js
const arr = [1, 2, 3, 4, 5];
const newArr = arr.slice(1, 4);
// newArr = [2, 3, 4]
```

***

## Search among elements

* **indexOf / lastIndexOf**(item, pos)\
  _look for `item` starting from index `pos`, return it's index or -1 if not found. Method `lastIndexOf()` searches from right to left_

```js
const arr = [10, 20, 20, 30];
const first = arr.indexOf(20); // first = 1
const last = arr.lastIndexOf(20); // last = 2
```

* **includes**(value)\
  _returns true if the array has value, else false_

```js
const arr = [10, 20, 30, 40];
const n = arr.includes(15); // false
```

* **find / findIndex**(func(item, index, arr))\
  _`func()` is called for each element of the array. If the `func()` returns true, the search is interrupted and item is returned, else - undefined_

```js
const arr = [1, 13, 23, 43, 56, 71, 97]
const evenNum = arr.find(item => {
    return % 2 === 0
})
// evenNum = 56
```

* **filter**(func(item, index, arr))\
  _the method is similar to `find()`, but `filter()` returns an array of all matching elements_

```js
const arr = [1, 2, 3, 4, 5, 6, 7];
const evenArr = arr.filter((item) => {
    return item % 2 === 0;
}); // evenArr = [2, 4, 6]
```

***

## Iteration of elements

* **forEach**(func(item, index, array))\
  _calls `func()` for every element in array, does not return anything_

```js
const arr = [1, 2, 3];
arr.forEach((item, index, arr) => {
    console.log(item, index, arr);
});
// 1 0 [1, 2, 3]
// 2 1 [1, 2, 3]
// 3 2 [1, 2, 3]
```

***

## Transform the array

* **map**(func(item, index, array))\
  _calls the `func()` for each element of the array and returns the array of results_

```js
const arr = [1, 2, 3, 4, 5];
const newArr = arr.map((item) => {
    return item * 10;
});
// newArr = [10, 20, 30, 40, 50]
```

* **sort**(func())\
  _sorts the array changing it's element order, `func()` defining the sorting order (optional)._

```js
const arr = [25, 7, 13 31]
arr.sort((a, b) => {
    return a - b
})
// arr = [7, 13, 25, 31]
```

* **reverse**()\
  _reverse the order of the elements of the current array_

```js
const arr = [1, 2, 3, 4, 5];
arr.reverse();
// arr = [5, 4, 3, 2, 1]
```

* **join**(separator) / string.split(separator)\
  _convert an array to string / a string to array_

```js
const str = "one, two, three, four";
const arr = str.split(", ");
// arr = ["one", "two", "three", "four"]
const newStr = arr.join("-");
// newStr = "one-two-three-four"
```

* **reduce / reduceRight**(func(accumulator, current, index, array), initial)\
  _calculate a single value over the array by calling `func()` for each element and passing an intermediate result between the calls_

```js
const arr = [1, 2, 3, 4, 5];
const sumFromElements = arr.reduce((sum, current) => {
    return sum + current;
}, 0);
// sumFromElements = 15
```

***

## Bonus

* Array.**isArray**(variable)\
  _checks `variable` for being an array, return true/false_

```js
const a = [1, 2, 3];
const b = 17;
Array.isArray(a); // true
Array.isArray(b); // false
```

* **some / every**(fn())\
  _The function `fn()` is called on each element of the array similar to `map()`. If any/all results are true - return true, otherwise - false_

```js
const arr = [1, 2, 3, 4, 5];
const even = (element) => element % 2 === 0;
arr.some(even); // true

const arr2 = [8, 20, 100, 29, 10, 13];
const lessThanForty = (element) => element < 40;
arr2.every(lessThanForty); // false
```

* **fill**(value, start, end)\
  _fills the array with repeating `value` from `start` to `end` positiion_

```js
const arr = ["a", "b", "c", "d"];
const filledArr = arr.fill("*", 2, 4);
// filledArr = ['a', 'b', '*', '*']
```

* **flat**(depth)\
  _create a new flat array from a multidimensioanl array_

```js
const arr = [0, 1, 2, [[[3, 4]]]];
const newArr = arr.flat(2);
// newArr = [0, 1, 2, [3, 4]]
```
