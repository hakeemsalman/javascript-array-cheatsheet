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
    - [arr.](#arr)


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

### arr.