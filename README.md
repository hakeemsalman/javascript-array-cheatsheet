# Arrays

> *Click &#9733; if you like the project. Your contributions are heartily ♡ welcome.*

<br/>

- It is a Special data structures which is used to store ordered collections.

---

- [Arrays](#arrays)
  - [Declaration](#declaration)
  - [Methods pop/push, shift/unshift](#methods-poppush-shiftunshift)
  - [How Arrays works internally](#how-arrays-works-internally)
  - [Performance](#performance)
  - [Loops](#loops)
  - [A word about length](#a-word-about-length)
  - [Multidimensional arrays](#multidimensional-arrays)
  - [toString](#tostring)
  - [Don’t compare arrays with ==](#dont-compare-arrays-with-)
  - [Array Methods](#array-methods)
    - [arr.splice](#arrsplice)
    - [arr.slice](#arrslice)
    - [arr.concat](#arrconcat)
    - [arr.forEach](#arrforeach)
  - [Searching methods in Array](#searching-methods-in-array)
    - [arr.indexOf](#arrindexof)
    - [arr.lastIndexOf](#arrlastindexof)
    - [arr.includes](#arrincludes)
    - [arr.find](#arrfind)
    - [arr.findIndex](#arrfindindex)
    - [arr.findLastIndex](#arrfindlastindex)
    - [arr.filter](#arrfilter)
  - [Transforming methods in an array](#transforming-methods-in-an-array)
    - [arr.map](#arrmap)
      - [2. `sort(fn)`](#2-sortfn)
      - [3. `reverse()`](#3-reverse)
      - [4. `split()` and `join()`](#4-split-and-join)
      - [5. `reduce()` and `reduceRight()`](#5-reduce-and-reduceright)
      - [6. `Array.isArray()`](#6-arrayisarray)
      - [7. `thisArg` in Array Methods](#7-thisarg-in-array-methods)


## Declaration

- There are two syntaxes &#10112;:
- Array elements are numbered, starting with zero.
- We can get an element by its number in square brackets &#10113;:
- We can replace an element and also can add new one to the array &#10114;.
- An array can store elements of any type &#10115;


    - ```js
      // ---------------------------------------------> 1
      let arr = new Array();
      let arr = [];

      // ---------------------------------------------> 2
      let fruits = ["Apple", "Orange", "Plum"];
      alert( fruits[0] ); // Apple
      alert( fruits[1] ); // Orange

      
      // ---------------------------------------------> 3
      fruits[1] = 'Pear';

      // ---------------------------------------------> 4
      let arr = [
        'Apple',            // string
        {                   // object
          name: 'John'
        },
        true,               // boolean
        function() {        // function
          alert('hello');
        }
      ];

      ```

Array has **two**  use cases.
1. [Stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type))
	1. new elements are added or taken always from the “end”.
	2. A stack is usually illustrated as a pack of cards: new cards are added to the top or taken from the top
	3. LIFO (Last-In-First-Out) principle
	- `push` adds an element to the end.
	- `pop` takes an element from the end.
1. [Queue](https://en.wikipedia.org/wiki/Queue_(abstract_data_type))
	1. means an ordered collection of elements which supports two operations:
		1. In practice we need it very often. For example, a queue of messages that need to be shown on-screen.
		2. FIFO (First-In-First-Out).
- `push` appends an element to the end.
- `shift` get an element from the beginning, advancing the queue, so that the 2nd element becomes the 1st.
> Arrays in **JavaScript** can work both as a **queue** and as a **stack**. They allow you to add/remove elements, both to/from the beginning or the end. In CS called as [deque](https://en.wikipedia.org/wiki/Double-ended_queue).

## Methods pop/push, shift/unshift

- `pop`: Remove/Extracts the last element of the array and returns it:
- `push`: Append the element to the end of the array:
- `shift`: Remove/Extracts the first element of the array and returns it
- `unshift`: Add the element to the beginning of the array

```js
let fruits = ["Apple", "Orange", "Pear"];

alert(  fruits.pop()            );          // remove "Pear"                    alert -----> "Pear"
alert(  fruits.push("Pear")     );          // append element to the end        alert -----> "3"
alert(  fruits.shift()          );          // remove "Apple"                   alert -----> "Apple"
alert(  fruits.unshift('Mango') );          // append element to the beginning  alert -----> "3" 

alert(  fruits                  );          // Mango,Orange,Pear
```


## How Arrays works internally

- An array is a special kind of object.
- The square brackets used to access a property `arr[0]` actually come from the object syntax.
- That’s essentially the same as obj[key], where arr is the object, while **numbers** are used as keys.


<table style="width: 600px;" align="center">
<tr>
<td>


But what makes arrays really special is their internal representation. The engine tries to store its elements in the contiguous memory area, one after another, just as depicted on the illustrations in this chapter, and there are other optimizations as well, to make arrays work really fast.

But they all break if we quit working with an array as with an “ordered collection” and start working with it as if it were a regular object.


</td>
</tr>
</table>

> Please think of arrays as special structures to work with the ordered data.
> They provide special methods for that. Arrays are carefully tuned inside JavaScript engines to work with contiguous ordered data, please use them this way.
> If you need arbitrary keys, chances are high that you actually require a regular object `{}`.

## Performance

- Methods `push`/`pop` run fast
- While `shift`/`unshift` are slow.

The `shift` operation must do 3 things:

- Remove the element with the index `0`.
- Move all elements to the left, renumber them from the index `1` to `0`, from `2` to `1` and so on.
- Update the `length` property.

> **The more elements in the array, the more time to move them, more in-memory operations.**

The `push`/`pop` operation have only one thing to do:

- To extract an element from the end
- the `pop` method cleans the index and shortens `length`.

> **The pop method does not need to move anything, because other elements keep their indexes. That’s why it’s blazingly fast.**

## Loops

There are **three** ways to iterate the array:

- `for` (Old traditional way)
- `for..of`
- `for..in` (**object** is bad idea)

```js
let arr = ["Apple", "Orange", "Pear"];

// Traditional way
for (let i = 0; i < arr.length; i++) {
  alert( arr[i] );
}

// iterates over array elements
for (let fruit of fruits) {
  alert( fruit );
}


// NOT RECOMMANDATION
for (let key in arr) {
  alert( arr[key] ); // Apple, Orange, Pear
}
```
But that’s actually a bad idea. There are potential problems with it:

1. The loop `for..in` iterates over all properties, not only the numeric ones.
   1. There are so-called “array-like” objects in the browser and in other environments, that look like arrays. That is, they have `length` and indexes properties, but they may also have other non-numeric properties and methods, which we usually don’t need. The `for..in` loop will list them though. So if we need to work with array-like objects, then these “extra” properties can become a problem.
2. The `for..in` loop is optimized for generic objects, not arrays, and thus is 10-100 times slower. Of course, it’s still very fast. The speedup may only matter in bottlenecks. But still we should be aware of the difference.

Generally, we shouldn’t use `for..in` for arrays.

## A word about length

- The `length` property automatically updates when we modify the array.
- It is the greatest numeric index plus one.
- ```js
  let fruits = [];
  fruits[123] = "Apple";

  alert( fruits.length ); // 124
  ```

### lenght is writable

- If we increase it manually, nothing interesting happens.
- But if we decrease it, the array is truncated.
- The process is irreversible:
    - ```js
      let arr = [1, 2, 3, 4, 5];

      arr.length = 2; // truncate to 2 elements
      alert( arr ); // [1, 2]

      arr.length = 5; // return length back
      alert( arr[3] ); // undefined: the values do not return
      ```

> So, the simplest way to **clear** the **array** is: `arr.length = 0;`.


## new Array()

- There is one more syntax to create an array:
    - ```js
      let arr = new Array("Apple", "Pear", "etc");
      ```
- If `new Array` is called with a single argument which is a number,
- then it creates an array *without items, but with the given length*.
- To avoid such suprises, we usually use **square brackets**.

```js
let arr = new Array(2); // will it create an array of [2] ?

alert( arr[0] ); // undefined! no elements.

alert( arr.length ); // length 2
```

## Multidimensional arrays

- Arrays can have items that are also arrays.
- We can use it for multidimensional arrays:

```js
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

alert( matrix[0][1] ); // 2, the second value of the first inner array
```

## toString

- Arrays have their own implementation of `toString` method that returns a comma-separated list of elements.

```js
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // true
```

- [More on toString](https://javascript.info/array#tostring)


## Don’t compare arrays with ==

- Let’s recall the rules:
  - Two objects are equal `==` only if they’re references to the same object.
  - If one of the arguments of `==` is an object, and the other one is a primitive, then the object gets converted to primitive, as explained in the chapter [Object to primitive conversion](https://javascript.info/object-toprimitive).
  - …With an exception of null and undefined that equal `==` each other and nothing else.

- To compare arrays, don’t use the == operator (as well as >, < and others), as they have no special treatment for arrays. They handle them as any objects, and it’s not what we usually want.

> Instead you can use `for..of` loop to compare arrays item-by-item.

## Array Methods

### arr.splice

- Modifies the original array by **adding, removing, or replacing elements** at a specified index.
- Takes **three** arguments: starting index, number of elements to remove, and optional elements to add.
- Returns an array of removed elements.
- *Negative* indexes allowed (Negative means from the **end** of the array)

<span style="color: red">&#9830;</span> **Parameter**: `splice(start, deleteCount, <item1, item2, /* …, */ itemN>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **YES**

```javascript
let arr = [1, 2, 3, 4, 5];
let removed = arr.splice(2, 2, 6, 7); // Removes 2 elements from starting index 2, adds 6 and 7
// Result: arr = [1, 2, 6, 7, 5],
// returned array: removed = [3, 4]
alert(arr.splice(0));                 // [1, 2, 3, 4, 5] removed all elements
alert(arr);                           // [] empty array

arr = [1, 2, 5];
// from index -1 (one step from the end)
// delete 0 elements,
// then insert 3 and 4
arr.splice(-1, 0, 3, 4);

alert( arr ); // 1,2,3,4,5
```

### arr.slice

- Returns a **shallow copy** of a portion of the array, based on the start and end indices provided.
- Does not modify the original array.
- Does **NOT** include *end* indexes value.
- Both `start` and `end` can be negative (it means from the end of the array)
- It’s similar to a string method `str.slice`, but instead of substrings, it makes subarrays.


<span style="color: red">&#9830;</span> **Parameter**: `slice(<start>, <end>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
let arr = [1, 2, 3, 4, 5];
let result = arr.slice(1, 3); // Extracts elements from index 1 to 3 (not including 3)
// Result: result = [2, 3], arr = [1, 2, 3, 4, 5]

let arrCopy = arr.slice();    // copy of arr, call without arguments 
```

> We can also call it without arguments: `arr.slice()` creates a copy of `arr`. That’s often used to obtain a copy for further transformations that <span style="color: orange">**should not affect**</span> the original array.


### arr.concat

- Combines two or more arrays and returns a **new array**.
- Does not modify the original arrays.

<span style="color: red">&#9830;</span> **Parameter**: `concat(value1, <value2, /* …, */ valueN>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];
let result = arr1.concat(arr2); // Combines arr1 and arr2
// Result: result = [1, 2, 3, 4]
```

---

### arr.forEach

- Executes a **provided function** once for each array element.
- Does not return a new array or modify the original array.

<span style="color: red">&#9830;</span> **Parameter**: `forEach(callbackFn, <thisArg>)`  
<span style="color: orange">&nbsp;&nbsp;&#9830;</span> `callbackFn(element, <index>, <array>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
let arr = [1, 2, 3];
arr.forEach((num, index) => console.log(`Index ${index}: ${num}`));
// Logs each element and 
// index:
//    "Index 0: 1"
//    "Index 1: 2"
//    ...
//    ...etc.
```

> The result of the function (if it returns any) is thrown away and ignored.


## Searching methods in Array

### arr.indexOf

- It Returns the **first index** at which a given element can be found, or `-1` if not found.
- It uses the strict equality `===` for comparison.
- It does not handle `NaN` correctly. (see [includes](#arrincludes))
- 
<span style="color: red">&#9830;</span> **Parameter**: `indexOf(searchElement, <fromIndex>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**


```javascript
let arr = [1, 2, 3, 2];
let first = arr.indexOf(2);    // Result: 1

const arr = [NaN];
alert( arr.indexOf(NaN) ); // -1 (wrong, should be 0)
```



### arr.lastIndexOf

- **`lastIndexOf(value)`**: Returns the **last index** at which an element appears, or `-1` if not found.

<span style="color: red">&#9830;</span> **Parameter**: `lastIndexOf(searchElement, <fromIndex>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
let arr = [1, 2, 3, 2];
let last = arr.lastIndexOf(2); // Result: 3
```

### arr.includes

- Returns `true` if the array **contains a specified element**; otherwise, returns `false`.
- If we want to check if `item` exists in the `array` and don’t need the index, then `arr.includes` is preferred.
- Negative index counts back from the end of the array.
- The `includes` method handles `NaN` correctly, a vice-versa of `indexOf`.

<span style="color: red">&#9830;</span> **Parameter**: `includes(searchElement, <fromIndex>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
let arr = [1, 2, 3];
alert(arr.includes(2));       // Result: true
alert(arr.includes(2, 1));    // Result: true
alert(arr.includes(2, -1));   // Result: false
alert(arr.includes("2"));     // Result: false

const arr = [NaN];
alert( arr.indexOf(NaN) ); // -1 (wrong, should be 0)
alert( arr.includes(NaN) );// true (correct)
```

### arr.find

- It Returns the **first element** that satisfies the callback function’s test.
- If it returns `true`, the search is stopped, the `item` is returned. If nothing is found, `undefined` is returned.
- It looks for a single (first) element that makes the function return true. For many use [filters](#arrfilter)


<span style="color: red">&#9830;</span> **Parameter**: `find(callbackFn, <thisArg>)`  
<span style="color: orange">&nbsp;&nbsp;&#9830;</span> `callbackFn(element, <index>, <array>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
let result = arr.find(function(item, index, array) {
  // if true is returned, item is returned and iteration is stopped
  // for falsy scenario returns undefined
});

let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);
let userUndefined = users.find(item => item.id == 4);

alert(user.name);             // John
alert(userUndefined?.name);   // undefined
```

You can practice problems from this [LINK](https://hakeemsalman.github.io/javascript-practice-questions/#)

### arr.findIndex

- It Returns the **index** of the first element that satisfies the test, or `-1` if not found.

<span style="color: red">&#9830;</span> **Parameter**: `findIndex(callbackFn, <thisArg>)`  
<span style="color: orange">&nbsp;&nbsp;&#9830;</span> `callbackFn(element, <index>, <array>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"},
  {id: 4, name: "John"}
];

// Find the index of the first John
alert(users.findIndex(user => user.name == 'John')); // 0
```

You can practice problems from this [LINK](https://hakeemsalman.github.io/javascript-practice-questions/#)

### arr.findLastIndex

- **`findLastIndex(callback)`**: Returns the **last index** where the condition is true.

<span style="color: red">&#9830;</span> **Parameter**: `findLastIndex(callbackFn, <thisArg>)`  
<span style="color: orange">&nbsp;&nbsp;&#9830;</span> `callbackFn(element, <index>, <array>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"},
  {id: 4, name: "John"}
];

// Find the index of the last John
alert(users.findLastIndex(user => user.name == 'John')); // 3
```

---

### arr.filter

- Similar to `find` but it returns as a `array` of pass elements instead of single element.
- Creates a [**Shallow copy**](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy) (new array) with all elements that pass the test implemented by the provided function.
- Does not modify the original array.
- If **no** elements pass the test, an **empty** `array` is returned.
- It should return a [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) value to keep the element in the resulting array, and a falsy value otherwise. 

<span style="color: red">&#9830;</span> **Parameter**: `filter(callbackFn, <thisArg>)`  
<span style="color: orange">&nbsp;&nbsp;&#9830;</span> `callbackFn(element, <index>, <array>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**

```javascript
// SYNTAX
let results = arr.filter(function(item, index, array) {
  // if true item is pushed to results and the iteration continues
  // returns empty array if nothing found
});

let arr = [1, 2, 3, 4];
let result = arr.filter(num => num % 2 === 0); // Filters even numbers
// Result: result = [2, 4]
```

## Transforming methods in an array

### arr.map

- Creates a **new array** by applying a provided function to each element in the array.
- Does not modify the original array.

<span style="color: red">&#9830;</span> **Parameter**: `filter(callbackFn, <thisArg>)`  
<span style="color: orange">&nbsp;&nbsp;&#9830;</span> `callbackFn(element, <index>, <array>)`  
<span style="color: red">&#9830;</span> [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm): **NO**


```javascript
let arr = [1, 2, 3];
let result = arr.map(num => num * 2); // Multiplies each element by 2
// Result: result = [2, 4, 6]
```

---

#### 2. `sort(fn)`
- Sorts the elements of an array **in place** (modifies the original array).
- Takes an optional comparison function `fn` to define custom sorting logic.

**Example:**
```javascript
let arr = [3, 1, 4, 2];
arr.sort((a, b) => a - b); // Sorts in ascending order
// Result: arr = [1, 2, 3, 4]
```

---

#### 3. `reverse()`
- Reverses the order of elements **in place**.
- Modifies the original array.

**Example:**
```javascript
let arr = [1, 2, 3];
arr.reverse();
// Result: arr = [3, 2, 1]
```

---

#### 4. `split()` and `join()`
- **`split()`**: Splits a string into an array of substrings, based on a specified delimiter. (Note: this is a `String` method, not an `Array` method).
- **`join()`**: Combines all elements of an array into a single string, separated by a specified delimiter.

**Example:**
```javascript
let str = "Hello World";
let arr = str.split(" ");       // Splits by spaces
// Result: arr = ["Hello", "World"]

let joined = arr.join(", ");    // Joins with comma and space
// Result: joined = "Hello, World"
```

---

#### 5. `reduce()` and `reduceRight()`
- **`reduce()`**: Applies a function against an accumulator and each element (left-to-right) to reduce the array to a single value.
- **`reduceRight()`**: Similar to `reduce()`, but works **right-to-left**.

**Example:**
```javascript
let arr = [1, 2, 3, 4];
let sum = arr.reduce((acc, num) => acc + num, 0); // Sum of all elements
// Result: sum = 10
```

---

#### 6. `Array.isArray()`
- Determines if a value is an **array**.
- Returns `true` if the value is an array, otherwise `false`.

**Example:**
```javascript
let arr = [1, 2, 3];
let result = Array.isArray(arr); // Result: true
```

---

#### 7. `thisArg` in Array Methods
- Many array methods, like `map()`, `forEach()`, and `filter()`, support an optional **`thisArg`** parameter.
- `thisArg` lets you specify the value of `this` inside the callback function, allowing custom contexts to be passed.

**Example:**
```javascript
let arr = [1, 2, 3];
let multiplier = {
  factor: 2,
};

let result = arr.map(function (num) {
  return num * this.factor;
}, multiplier); // Sets `this` to `multiplier` object
// Result: result = [2, 4, 6]
```
