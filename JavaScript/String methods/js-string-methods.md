# String methods cheatsheet

---

## Changing the case

-   **toLowerCase / toUpperCase**()

```js
const str = "Hello";
const low = str.toLowerCase(); // hello
const up = str.toUpperCase(); // HELLO
```

---

## Combining strings

-   **concat**(...items)
    _Combines two or more strings and returns one string_

```js
const str = "Hello";
const str2 = "World!";
const newStr = str.concat(" ", str2);
// newStr = "Hello World!"
```

---

## Splitting a string

-   **split**(separator, limit)

_Splits a string into an array by the specified separator, which can be a substring or a regular expression_

```js
const str = "Just some text";
const arr = str.split(" ");
arr = ["Just", "some", "text"];
```

---

## Repeating a sting

-   **repeat**(count)
    _Repeats the string the specified number of times_

```js
const str = "hey";
const newStr = str.repeat(3);
// newStr = "heyheyhey"
```

---

## Substring search

-   **charAt**(index)
    _Returns a character at the specified index_

```js
const str = "hello";
const char = str.charAt(1);
// char = "e"
```

-   **includes**(substr, startPositon)
    _Checks if the string contains the specified substring and returns true/false_

```js
const str = "example@gmail.com";
str.includes("gmail"); // true
```

-   **indexOf / lastIndexOf**(substr, startPositon)
    _Returns the index of the first/last substring found, otherwise returns -1_

```js
const str = "example@gmail.com";
str.indexOf("@"); // 6
str.lastIndexOf("m"); // 15
```

-   **endsWith/startsWith**(substr, searchLength)
    _Checks if the string ends/starts with the specified substring and returns true/false_

```js
const link = "www.google.com";
link.startsWith("www"); // true
link.endsWith(".com"); // true
```

-   **search**(substr)
    _Checks if there is a specified substring or regular expression in the string and returns the index of the beginning of the match_

```js
const str = "first name, second name";
str.search("name"); // 6
```

---

## Extracting a substring

-   **slice**(start, end)
    _Extracts part of the string starting at the `start` position and ending at the `end`-1 position_

```js
const str = "javascript";
const substr = str.slice(4); // script
const substr = str.slice(4, 0); // java
```

-   **substring**(start, end)
    _Extracts substring from a string between `start` and `end`. Unlike `slice()`, you can set `start` more than `end`._

```js
const str = "javascript";
const substr = str.substring(4); // script
const substr2 = str.substring(4); // script
```

-   **substr**(start, length)
    _Extracts part of a string of a specified `length`. The first parameter can be negative, then the position is determined from the end of the string._

```js
const str = "typescript";
const sub = str.substr(4, 6); // script
const sub2 = str.substr(-6); // script
```

---

## Replacing a substring

-   **replace**(substr, newSubstr)
    _Searches for the specified substring (or regular expression) in the string and replaces it with another one_

```js
const str = "typescript";
const str2 = str.replace("type", "java");
// str2 = javascript
```

-   **replaceAll**(substr, newSubstr)
    _Replaces all found matches with another string or passed function_

```js
const str = "one two three";
const str2 = str.replaceAll(" ", "-");
// str2 = one-two-three
```

---

## Adding characters

-   **padStart / padEnd**(strLength, str)
    _Adds padding at the beginning/end of a string until the string reaches the length specified by the first parameter_

```js
const msg = "hello";
msg.padStart(10, "_"); // "_____hello"
msg.padStart(7); // "  hello"
msg.padEnd(10, "*"); // "hello*****"
```

---

## Removing spaces

-   **trim / trimStart / trimEnd**()
    _Deletr spaces at both ends of the string, either only at the beginning or only at the end_

```js
const str = "  hello   ";
str.trim(); // "hello"
str.trimStart(); // "hello   "
str.trimEnd(); // "  hello"
```

## Working with ASCII code

-
