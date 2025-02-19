# A Short Notes of array methods:

---

[Back To Home](../README.md)

---

- [A Short Notes of array methods:](#a-short-notes-of-array-methods)
  - [To add/remove elements:](#to-addremove-elements)
  - [To search among elements:](#to-search-among-elements)
  - [To iterate over elements:](#to-iterate-over-elements)
  - [To transform the array:](#to-transform-the-array)
  - [Additionally:](#additionally)

## To add/remove elements:

- `push(...items)` – adds items to the end,
- `pop()` – extracts an item from the end,
- `shift()` – extracts an item from the beginning,
- `unshift(...items)` – adds items to the beginning.
- `splice(pos, deleteCount, ...items)` – at index position deletes the deleteCount elements and inserts items.
- `slice(start, end)` – creates a new array, copies elements from index start till end (not inclusive) into it.
- `concat(...items)`– returns a new array: copies all members of the current one and adds items to it. If any of items is an array, then its elements are taken.

## To search among elements:

- `indexOf/lastIndexOf(item, pos)` – look for item starting from position pos, and return the index or -1 if not found.
- `includes(value)` – returns true if the array has value, otherwise false.
- `find/filter(func)` – filter elements through the function, return first/all values that make it return true.
- `findIndex` is like find, but returns the index instead of a value.

## To iterate over elements:

- `forEach(func)` – calls func for every element, does not return anything.

## To transform the array:

- `map(func)` – creates a new array from results of calling func for every element.
- `sort(func)` – sorts the array in-place, then returns it.
- `reverse()` – reverses the array in-place, then returns it.
- `split/join` – convert a string to array and back.
- `reduce/reduceRight(func, initial)` – calculate a single value over the array by calling func for each element and passing an intermediate result between the calls.

## Additionally:

- `Array.isArray(value)` checks value for being an array, if so returns true, otherwise false.