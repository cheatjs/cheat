# Node.js basics cheatsheet

## Table of content

## Node package manager (NPM)

Node.js has a huge number of packages created by different developers that you can easily import into your projects using `npm`.

Basic console commands:

_Create a `package.json` - configuration file that will describe the installed packages, scripts and application information:_

```sh
npm init -y
```

_Add package:_

```sh
npm install package-name
```

_Add package only for development:_

```sh
npm install -D package-name
```

_Delete package:_

```sh
npm uninstall package-name
```

## Run code

-   **Running code**
    _Use command `node` + path to file to run it_

```sh
node app.js
```

-   **Running code with passing parameters**
    `node app.js hello 123`

```js
// app.js
// The first two parameters always determine the paths
const pathToNode = process.argv[0]; // path to node.exe on PC
const pathToApp = process.argv[1]; // path to current file

// Your agruments
const param1 = process.argv[2]; // hello
const param2 = process.argv[3]; // 123
```

-   **Environment variables**
    _`dotenv` is needed to load environment variables from `.env` file_

```sh
node install dotenv
```

```js
// .env
TEST = "Hello from .env file";
```

```js
// app.js
// Connect dotenv package
const dotenv = require("dotenv");
dotenv.config();

console.log(process.env.TEST); // Hello from .env file
```

## Modules

-   **CommonJS**
    _Modular system created specifically for Node.js_

```js
// module.js
const message = "Hello Node.js!";
const calcSum = (a, b) => a + b;

module.exports = { message, calcSum };
```

```js
// app.js
const { message, calcSum } = require("./module");

console.log(message); // Hello Node.js!
console.log(calcSum(2, 3)); // 5
```

-   **ES modules**
    _A modular system added to JavaScript in 2015. To enable it in Node.js, add the option `”type”: "module"` to the `package.json`_

```js
// module.js
export const message = "Hello Node.js!";
export const calcSum = (a, b) => a + b;
```

```js
// app.js
import { message, calcSum } from "./module";

console.log(message); // Hello Node.js!
console.log(calcSum(2, 3)); // 5
```

> Of course, the future belongs to ES modules. But there are still a number of difficulties associated with compatibility.

## Working with paths

Node.js has a built-in `path` module for working with paths

```js
const path = require("path");

// global variable showing the path to the current folder
console.log(__dirname);
// global variable showing the path to the current file
console.log(__filename);

// joins all given path segments together (crossplatform)
path.join(__dirname, "modules", "mod.js");

// return object with properties describing a given path
path.parse("/home/user/project/data.txt");

//resolves a sequence/segments of paths into an absolute path
path.resolve("/modules", "mod.js");

// return the platform-specific path segment separator
path.sep; // '/' or '\'

path.isAbsolute("modules/mod.js"); // false
path.isAbsolute("/modules/mod.js"); // true

path.basename("/home/user/project/app.js"); // app.js
path.extname("/home/user/project/app.js"); // .js
```

## Working with files

Node.js has a built-in fs module for working with files

-   **Create/delete folders**

```js
const fs = require("fs");
const path = require("path");

// create folder "dir" in current directory
fs.mkdir(path.resolve(__dirname, "dir"), (err) => {
    if (err) throw err;
});

// // delete folder "dir" from current directory
fs.rmdir(path.resolve(__dirname, "dir"));
```

-   **Create/read/update/delete files**

```js
// Write data to a new file or overwrite an existing file
fs.writeFile("file.txt", "Hello Node.js!", (error) => {
    if (error) throw error;
});
```

```js
// Add data to the end of the file
fs.appendFile("file.txt", "!!!", (error) => {
    if (error) throw error;
});
```

```js
// Read exists file
fs.readFile("file.txt", (error, data) => {
    if (error) throw error;
    console.log(data.toString()); // Hello Node.js!!!
});
```

```
fs.open(path, flags, [mode], callback)
```

```js
// Delete file
fs.unlink("file.txt", (error) => {
    if (error) throw error;
});
```

> To ensure that all operations run in sync one by one, you can add `Sync` to each method name

## System info

Node.js has a built-in `os` module for OS information

```js
const os = require("os");

console.log(os.platform()); // identifying the OS platform
console.log(os.version()); // identifying the kernel version
console.log(os.arch()); // info about CPU architecture
console.log(os.cpus()); // info about each logical CPU core
```

## Events

Node.js allows you to create so-called `Event Emmitters`, which call special functions (`Listeners`) when an event is triggered.

```js
const EventEmitter = require("events");
const myEmitter = new EventEmitter();

// Create the event called "helloEvent"
myEmitter.on("helloEvent", (param) => {
    console.log(`Hello, ${param}!`);
});

// Call the event "helloEvent"
myEmitter.emit("helloEvent", "Node.js");
```

```js
myEmitter.once("single", () => console.log(`Hi!`));
```

```js
// delete all
myEmitter.removeAllListeners();
// delete only "helloEvent"
myEmitter.removeListener("helloEvent");
```

## Streams

The `stream` module allow you to read stream data in small chunks (64kb by default) <br>
There are 4 types of streams: `Readable`, `Writable`, `Duplex` (R + W) and `Transform`.

```js
const fs = require("fs");
const path = require("path");

// Create readable stream
const rStream = fs.createReadStream(
    path.resolve(__dirname, "big.txt") //path to data
);

// First param is event. There are events:
// data, open, ready, error, pause, resume, end, close, readable
rStream.on("data", (chunk) => {
    console.log(chunk);
});
rStream.on("end", () => console.log("File has been read"));
rStream.on("error", (err) => console.log(err));
```

```js
const wStream = fs.createWriteStream(
    path.resolve(__dirname, "data.txt") // path to writable file
);

for (let i = 0; i < 10; i++) {
    wStream.write(`Text line ${i + 1} \n`);
}

wStream.end(); // close stream
```

## HTTP server

Server operations are the main application area fo Node.js

-   **Basic http server**

```js
const http = require("http");
const PORT = process.env.PORT || 3000;
const server = http.createServer((req, res) => {
    // req - object with request data
    // res - object with response data
    res.writeHead(200, {
        "Content-type": "text/html;",
    });

    res.end(`<h1>Welcome to Node.js server</h1>`);
});

server.listen(PORT, () => {
    console.log("Server is running...");
});
```

> After starting the server, you can view it if open http://localhost://3000 on your browser.

For more convenient and fast creation of servers on Node.js uses various frameworks, such as `Express.js`, `Fastify`, `Koa.js`, `Nest.js`.
