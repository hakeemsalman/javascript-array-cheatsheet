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