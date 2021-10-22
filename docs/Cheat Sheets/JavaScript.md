## Loops

### for
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)

```js
for (let i = 0; i < 5; i++)
    {
        console.log(i);
    }
// OUTPUT: 0 1 2 3 4
```

### for...in
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)

```js
const arr = [3, 5, 7];
arr.foo = 'hello';
for (let i in arr) {
    console.log(i);
}
// OUTPUT: "0", "1", "2", "foo"
```

### for...of
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

```js
const arr = [3, 5, 7];
for (let i of arr) {
    console.log(i);
}
// OUTPUT: 3, 5, 7
```

### do...while
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/do...while)

```js
let iterator = 0;
do {
    iterator++;
    console.log(iterator);
} while (iterator < 5);
// OUTPUT: 1 2 3 4 5
```

### while
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while)

```js
let iterator = 0;
while (iterator < 5) {
    iterator++;
    console.log(iterator);
}
// OUTPUT: 1 2 3 4 5
```

## JS ES6

### Arrow function

```js
const sum = (a, b) => a + b
console.log(sum(2, 6)) // OUTPUT: 8
```

### Default parameters

```js
function print(a = 5) {
    console.log(a)
}
print() // OUTPUT: 5
print(22) // OUTPUT: 22
```

### Let Scope

```js
let a = 3
if (true) {
    let a = 5
    console.log(a) // OUTPUT: 5
}
console.log(a) // OUTPUT: 3
```

### Const

```js
// can be assigned only once
const a = 55
a = 44 // throws an error
```

### Multiline string

```js
console.log(`
This is a
multiline string
`)
```

### Template strings

```js
const name = 'World';
const message = `Hello ${name}`;
console.log(message); // OUTPUT: "Hello World"
```

### Exponent operator

```js
const byte = 2 ** 8
// Same as: Math.pow(2, 8)
```

### Spread operator

```js
const a = [ 1, 2 ]
const b = [ 3, 4 ]
const c = [ ...a, ...b ]
console.log(c) // OUTPUT: [1, 2, 3, 4]
```

### String `includes()`

```js
console.log('apple'.includes('pl')); // OUTPUT: true
console.log('apple'.includes('tt')); // OUTPUT: false
```

### String `startsWith()`

```js
console.log('apple'.startsWith('ap')); // OUTPUT: true
console.log('apple'.startsWith('bb')); // OUTPUT: false
```

### String `repeat()`

```js
console.log('ab'.repeat(3)); // OUTPUT: "ababab"
```

### Destructuring `array`

```js
let [a, b] = [3, 7];
console.log(a); // 3
console.log(b); // 7
```

### Destructuring `object`

```js
let obj = {
    a: 55,
    b: 44
};
let { a, b } = obj;
console.log(a); // OUTPUT: 55
console.log(b); // OUTPUT: 44
```

### Object `property` assignment

```js
const a = 2
const b = 5
const obj = { a, b }
// Before es6:
// obj = { a: a, b: b }
console.log(obj) // OUTPUT: { a: 2, b: 5 }
```

### Object `function` assignment

```js
const obj = {
    a: 5,
    b() {
        console.log('b')
    }
}
obj.b() // OUTPUT: "b"
```

### `Object.assign()`

```js
const obj1 = { a: 1 }
const obj2 = { b: 2 }
const obj3 = Object.assign({}, obj1, obj2)
console.log(obj3)
// { a: 1, b: 2 }
```

### `Object.entries()`

```js
const obj = {
    firstName: 'FirstName',
    lastName: 'LastName',
    age: 24,
    country: 'India',
};
const entries = Object.entries(obj);
/* returns an array of [key, value]
pairs of the object passed */
console.log(entries);
/* prints
[
['firstName', 'FirstName'],
['lastName', 'LastName'],
['age', 24],
['country', 'India']
]; */
```

### Promises with `finally`

```js
promise
.then((result) => { ··· })
.catch((error) => { ··· })
.finally(() => { /* logic
    independent of success/error */ })
/* The handler is called when the
promise is fulflled or rejected.*/
```

### Destructuring Nested Objects

```js
const Person = {
    name: "Harry Potter",
    age: 29,
    sex: "male",
    materialStatus: "single",
    address: {
        country: "USA",
        state: "Nevada",
        city: "Carson City",
        pinCode: "500014",
    },
};
const { address : { state, pinCode }, name } = Person;
console.log(name, state, pinCode)
// Harry Potter Nevada 500014
console.log(city) // ReferenceError
```

### Spread operator

```js
const a = {
    firstName: "FirstName",
    lastName: "LastName1",
}
const b = {
    ...a,
    lastName: "LastName2",
    canSing: true,
}
console.log(a)
//{firstName: "FirstName", lastName: "LastName1"}
console.log(b)
/* {firstName: "FirstName", lastName: "LastName2",
canSing: true} */
/* great for modifying objects without side
effects/affecting the original */
```

## Arrays destructuring

### Assigning `array` items to variables

```js
const [a, b, c] = [123, 'second', true];
// a => 123
// b => 'second'
// c => true
```

### Skipping items

```js
const [, b] = [123, 'second', true];
// b => 'second'
```

### Assigning the first values, storing the rest together

```js
const [a, b, ...rest] = [123, 'second', true, false, 42];
// a => 123
// b => 'second'
// rest => [true, false, 42]
```

### Swapping variables

```js
let x = true;
let y = false;
[x, y] = [y, x];
// x => false
// y => true
```

## String methods

### `charAt()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charAt)

```js
let txt = 'Hello World';
console.log(txt.charAt(0)); // OUTPUT: 'H'
```

### `concat()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat)

```js
let str1 = 'Hello ';
let str2 = 'World';
console.log(str1.concat(str2)); // OUTPUT: 'Hello world';
```

### `indexOf()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)

```js
let txt = 'Lets find where the `pen` is';
console.log(txt.indexOf('pen')); // OUTPUT: 21
```

### `replace()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

```js
let str = 'Hello Dev!'
console.log(str.replace('Dev', 'World')); // OUTPUT: 'Hello World'
```

### `search()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/search)

```js
let str = 'Hello dev';
console.log(str.search('dev')); // OUTPUT: 6
```

### `slice()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice)

```js
let str1 = 'The morning is upon us.', // the length of str1 is 23.
    str2 = str1.slice(1, 8),
    str3 = str1.slice(4, -2),
    str4 = str1.slice(12),
    str5 = str1.slice(30);
console.log(str2)  // OUTPUT: he morn
console.log(str3)  // OUTPUT: morning is upon u
console.log(str4)  // OUTPUT: is upon us.
console.log(str5)  // OUTPUT: ""
```

### `substring()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)

```js
const str = 'Mozilla';
console.log(str.substring(1, 3));
// expected output: "oz"
console.log(str.substring(2));
// expected output: "zilla"
```

### `substr()`
Deprecated. Not for use in new websites. [More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substr)

```js
const str = 'Mozilla';
console.log(str.substr(1, 2));
// expected output: "oz"
console.log(str.substr(2));
// expected output: "zilla"
```

Difference between `substr()` and `substring()`

```js
let text = 'Mozilla'
console.log(text.substring(2,5))  // => "zil"
console.log(text.substr(2,3))     // => "zil"
```

### `toUpperCase()` / `toLowerCase()`
[`toUpperCase()` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) | [`toLowerCase()` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)

```js
const sentence = 'The quick brown fox jumps over the lazy dog.';
console.log(sentence.toUpperCase());
// expected output: "THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG."
const allcaps = 'HAPPY CAPSLOCK DAY!';
console.log(allcaps.toLowerCase());
// EXPECTED OUTPOOT: "HAPPY CAPSLOCK DAY!"
```

### `valueOf()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/valueOf)

```js
var x = new String('Hello world');
console.log(x.valueOf()); // Displays 'Hello world'
```

### `trim()`
[Mode on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Trim)

```js
const greeting = '   Hello world!   ';
console.log(greeting);
// expected output: "   Hello world!   ";
console.log(greeting.trim());
// expected output: "Hello world!";
```

`toString()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toString)

```js
const myNumber = 535;
console.log(myNumber.toString()); // OUTPUT: "535";
```

`includes()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)

```js
const sentence = 'The quick brown fox jumps over the lazy dog.';
const word = 'fox';
console.log(sentence.includes(word)); // OUTPUT: true
```

`charCodeAt()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt)

```js
let word = 'TEST';
console.log(word.charCodeAt(0)); // OUTPUT: 84
```

`match()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match)

```js
const paragraph = 'The quick brown fox jumps over the lazy dog. It barked.';
const found = paragraph.match("th");
console.log(found); // OUTPUT: ["th"]
```

`split()`
[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split)

```js
const str = 'The quick brown fox jumps over the lazy dog.';
const words = str.split(' ');
console.log(words[3]);
// expected output: "fox"
```

## JavaScript Async/Await

### Async

When we append the keyword `async` to the `function`, this `function`
returns the `Promise` by default on execution. Async keyword provides
extra information to the user of the function:

- The function contains some Asynchronous Execution
- The returned value will be the Resolved Value for the Promise

```js
async function f() {
    return 1;
}
f().then(alert); // OUTPUT: 1
```

### Await
The keyword `await` makes JavaScript wait until that promise settles and returns its result

- The `await` works only inside `async` functions

```js
async function f() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve("done!"), 1000)
    });
    let result = await promise; // wait until the promise resolves
    alert(result); // OUTPUT: "done!"
}
f();
```

## API calls

### XML HTTP Request

- All modern browsers support the XMLHttpRequest `object` to `request` data from a server.
- It works on the oldest browsers as well as on new ones.
- It was deprecated in ES6 but is still widely used.

```js
var request = new XMLHttpRequest();
request.open('GET',
    'https://jsonplaceholder.typicode.com/todos')
request.send();
request.onload = () => {
    console.log(JSON.parse(request.response));
}
```

### Fetch

- The Fetch API provides an interface for fetching resources (including across the network) in an asynchronous manner.
- It returns a Promise
- It is an object which contains a single value either a Response or an Error that occurred.
- `.then()` tells the program what to do once Promise is completed.

```js
fetch('https://jsonplaceholder.typicode.com/todos'
).then(response => {
    return response.json();
}).then(data => {
    console.log(data);
})
```

### Axios

- It is an open-source library for making HTTP requests.
- It works on both Browsers and Node.js
- It can be included in an HTML file by using an external CDN
- It also returns promises like fetch API

```js
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
axios.get("https://jsonplaceholder.typicode.com/todos")
    .then(response =>{
        console.log(response.data)
    })
```

### jQuery AJAX

- It performs asynchronous HTTP requests.
- Uses `$.ajax()` method to make the requests.

```js
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js">
</script>
$(document).ready(function(){
    $.ajax({
    url: "https://jsonplaceholder.typicode.com/todos",
    type: "GET",
    success: function(result){
        console.log(result);
        }
    })
})
```

