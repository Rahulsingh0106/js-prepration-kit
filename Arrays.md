# JavaScript Arrays

## Table of Contents
1. [Introduction](#introduction)
2. [Creating Arrays](#creating-arrays)
3. [Array Properties](#array-properties)
4. [Accessing Array Elements](#accessing-array-elements)
5. [Array Methods - Mutating](#array-methods---mutating)
6. [Array Methods - Non-Mutating](#array-methods---non-mutating)
7. [Array Methods - Iteration](#array-methods---iteration)
8. [Searching in Arrays](#searching-in-arrays)
9. [Multi-dimensional Arrays](#multi-dimensional-arrays)
10. [Best Practices](#best-practices)

---

## Introduction

An **array** is an ordered collection of elements, where each element can be of any data type (numbers, strings, objects, functions, etc.). Arrays are zero-indexed, meaning the first element is at index 0.

```javascript
const fruits = ['apple', 'banana', 'orange'];
// Index:       0        1        2
```

---

## Creating Arrays

### 1. Array Literal (Most Common)
```javascript
const numbers = [1, 2, 3, 4, 5];
const mixed = [1, 'hello', true, null, { name: 'John' }];
const empty = [];
```

### 2. Array Constructor
```javascript
const arr = new Array(5);  // Creates array with 5 empty slots
const arr2 = new Array(1, 2, 3);  // Creates array with elements 1, 2, 3
```

### 3. Array.from() - Convert iterable to array
```javascript
const str = 'hello';
const charArray = Array.from(str);  // ['h', 'e', 'l', 'l', 'o']

const range = Array.from({ length: 5 }, (_, i) => i + 1);  // [1, 2, 3, 4, 5]
```

### 4. Spread Operator
```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];  // [1, 2, 3, 4, 5]
```

---

## Array Properties

### length
Returns the number of elements in the array.

```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr.length);  // 5

// Modifying length can truncate array
arr.length = 3;  // [1, 2, 3]
```

---

## Accessing Array Elements

### Index-based Access
```javascript
const fruits = ['apple', 'banana', 'orange'];
console.log(fruits[0]);   // 'apple'
console.log(fruits[2]);   // 'orange'
console.log(fruits[-1]);  // undefined (JavaScript doesn't support negative indexing)
```

### at() Method (Modern)
```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr.at(0));    // 1  (first element)
console.log(arr.at(-1));   // 5  (last element)
console.log(arr.at(-2));   // 4  (second last element)
```

---

## Array Methods - Mutating

These methods modify the original array.

### 1. push() - Add to end
```javascript
const arr = [1, 2];
arr.push(3, 4);  // [1, 2, 3, 4]
console.log(arr.length);  // Returns new length: 4
```

### 2. pop() - Remove from end
```javascript
const arr = [1, 2, 3];
const last = arr.pop();  // Returns 3
// arr is now [1, 2]
```

### 3. unshift() - Add to beginning
```javascript
const arr = [2, 3];
arr.unshift(0, 1);  // [0, 1, 2, 3]
```

### 4. shift() - Remove from beginning
```javascript
const arr = [1, 2, 3];
const first = arr.shift();  // Returns 1
// arr is now [2, 3]
```

### 5. splice() - Add/remove at specific position
```javascript
const arr = ['a', 'b', 'c', 'd'];
arr.splice(1, 2);  // Removes 2 elements starting at index 1
// arr is now ['a', 'd']

arr.splice(1, 0, 'x', 'y');  // Insert without removing
// arr is now ['a', 'x', 'y', 'd']
```

### 6. reverse() - Reverse array
```javascript
const arr = [1, 2, 3];
arr.reverse();  // [3, 2, 1]
```

### 7. sort() - Sort array
```javascript
const arr = [3, 1, 4, 1, 5];
arr.sort();  // [1, 1, 3, 4, 5]

// Custom sorting
const numbers = [5, 2, 10, 3];
numbers.sort((a, b) => a - b);  // [2, 3, 5, 10] (ascending)
numbers.sort((a, b) => b - a);  // [10, 5, 3, 2] (descending)

// Sort objects
const users = [
  { name: 'John', age: 30 },
  { name: 'Jane', age: 25 }
];
users.sort((a, b) => a.age - b.age);
```

### 8. copyWithin() - Copy part of array
```javascript
const arr = [1, 2, 3, 4, 5];
arr.copyWithin(0, 3);  // Copy elements from index 3 to beginning
// [4, 5, 3, 4, 5]
```

### 9. fill() - Fill array with value
```javascript
const arr = [1, 2, 3, 4, 5];
arr.fill(0, 2, 4);  // Fill 0 from index 2 to 4
// [1, 2, 0, 0, 5]
```

---

## Array Methods - Non-Mutating

These methods return a new array without modifying the original.

### 1. slice() - Extract portion
```javascript
const arr = [1, 2, 3, 4, 5];
const sliced = arr.slice(1, 3);  // [2, 3] (not including index 3)
const slicedLast2 = arr.slice(-2);  // [4, 5]

// Shallow copy entire array
const copy = arr.slice();  // [1, 2, 3, 4, 5]
```

### 2. concat() - Combine arrays
```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];
const combined = arr1.concat(arr2);  // [1, 2, 3, 4]

// Concat with multiple arrays
const result = arr1.concat(arr2, [5, 6]);  // [1, 2, 3, 4, 5, 6]
```

### 3. join() - Convert to string
```javascript
const arr = ['Hello', 'World'];
console.log(arr.join(' '));  // 'Hello World'
console.log(arr.join('-'));  // 'Hello-World'
console.log(arr.join());     // 'Hello,World' (default comma)
```

### 4. toString() - Convert to string
```javascript
const arr = [1, 2, 3];
console.log(arr.toString());  // '1,2,3'
```

---

## Array Methods - Iteration

All of these accept a callback function and do not modify the original array.

### 1. forEach() - Iterate and execute function
```javascript
const arr = [1, 2, 3];
arr.forEach((element, index, array) => {
  console.log(`Index ${index}: ${element}`);
});
```

### 2. map() - Transform each element
```javascript
const numbers = [1, 2, 3, 4];
const squared = numbers.map(num => num * num);  // [1, 4, 9, 16]

// With objects
const users = [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }];
const names = users.map(user => user.name);  // ['John', 'Jane']
```

### 3. filter() - Select elements that match condition
```javascript
const numbers = [1, 2, 3, 4, 5, 6];
const even = numbers.filter(num => num % 2 === 0);  // [2, 4, 6]

const users = [{ name: 'John', age: 30 }, { name: 'Jane', age: 25 }];
const adults = users.filter(user => user.age >= 18);
```

### 4. reduce() - Accumulate values
```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);  // 10

const product = numbers.reduce((acc, curr) => acc * curr, 1);  // 24

// Building objects
const items = [
  { color: 'red', quantity: 2 },
  { color: 'blue', quantity: 1 },
  { color: 'red', quantity: 3 }
];
const byColor = items.reduce((acc, item) => {
  acc[item.color] = (acc[item.color] || 0) + item.quantity;
  return acc;
}, {});  // { red: 5, blue: 1 }
```

### 5. reduceRight() - Reduce from right to left
```javascript
const arr = [1, 2, 3, 4];
const result = arr.reduceRight((acc, curr) => acc + curr, 0);  // 10
```

### 6. some() - Check if at least one matches
```javascript
const numbers = [1, 2, 3, 4, 5];
const hasEven = numbers.some(num => num % 2 === 0);  // true

const users = [{ name: 'John', admin: false }, { name: 'Jane', admin: true }];
const hasAdmin = users.some(user => user.admin);  // true
```

### 7. every() - Check if all match
```javascript
const numbers = [2, 4, 6, 8];
const allEven = numbers.every(num => num % 2 === 0);  // true

const ages = [25, 30, 35];
const allAdults = ages.every(age => age >= 18);  // true
```

### 8. find() - Get first matching element
```javascript
const users = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Jane' },
  { id: 3, name: 'Bob' }
];
const user = users.find(u => u.id === 2);  // { id: 2, name: 'Jane' }
```

### 9. findIndex() - Get index of first matching element
```javascript
const arr = [1, 2, 3, 4, 5];
const index = arr.findIndex(num => num > 3);  // 3 (index of 4)
```

### 10. findLast() - Get last matching element (ES2023)
```javascript
const arr = [1, 2, 3, 4, 5];
const last = arr.findLast(num => num > 3);  // 5
```

### 11. findLastIndex() - Get index of last matching element (ES2023)
```javascript
const arr = [1, 2, 3, 4, 5];
const index = arr.findLastIndex(num => num > 3);  // 4
```

### 12. flat() - Flatten nested arrays
```javascript
const nested = [1, [2, 3], [4, [5, 6]]];
const flattened = nested.flat();  // [1, 2, 3, 4, [5, 6]]
const fullyFlattened = nested.flat(2);  // [1, 2, 3, 4, 5, 6]
const deepFlat = nested.flat(Infinity);  // [1, 2, 3, 4, 5, 6]
```

### 13. flatMap() - Map and flatten
```javascript
const arr = [1, 2, 3];
const result = arr.flatMap(num => [num, num * 2]);
// [1, 2, 2, 4, 3, 6]
```

---

## Searching in Arrays

### 1. indexOf() - Find first index
```javascript
const arr = [1, 2, 3, 2, 4];
console.log(arr.indexOf(2));   // 1
console.log(arr.indexOf(5));   // -1 (not found)
console.log(arr.indexOf(2, 2));  // 3 (search from index 2)
```

### 2. lastIndexOf() - Find last index
```javascript
const arr = [1, 2, 3, 2, 4];
console.log(arr.lastIndexOf(2));  // 3
```

### 3. includes() - Check existence
```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr.includes(3));  // true
console.log(arr.includes(10));  // false

// With NaN (includes works with NaN, indexOf doesn't)
const arrWithNaN = [1, NaN, 3];
console.log(arrWithNaN.includes(NaN));  // true
console.log(arrWithNaN.indexOf(NaN));   // -1
```

---

## Multi-dimensional Arrays

### Creating 2D Arrays
```javascript
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

console.log(matrix[0][1]);  // 2 (row 0, column 1)
console.log(matrix[2][2]);  // 9 (row 2, column 2)
```

### Iterating 2D Arrays
```javascript
const matrix = [
  [1, 2, 3],
  [4, 5, 6]
];

// Using forEach
matrix.forEach((row, rowIdx) => {
  row.forEach((element, colIdx) => {
    console.log(`[${rowIdx}][${colIdx}]: ${element}`);
  });
});

// Using for loops
for (let i = 0; i < matrix.length; i++) {
  for (let j = 0; j < matrix[i].length; j++) {
    console.log(matrix[i][j]);
  }
}
```

### Creating 2D Array with map
```javascript
const rows = 3, cols = 3;
const matrix = Array.from({ length: rows }, () => Array(cols).fill(0));
// [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
```

---

## Best Practices

### 1. Use const by default
```javascript
// Good
const arr = [1, 2, 3];
arr.push(4);  // You can mutate; just can't reassign

// Avoid
let arr = [1, 2, 3];
```

### 2. Use appropriate methods
```javascript
// Good: Use includes() for existence check
if (arr.includes(value)) { }

// Avoid: Using indexOf() for existence check
if (arr.indexOf(value) !== -1) { }

// Good: Use filter() for non-mutating operations
const even = arr.filter(n => n % 2 === 0);

// Avoid: Mutating when not necessary
arr.splice(0, arr.length, ...arr.filter(n => n % 2 === 0));
```

### 3. Understand mutating vs non-mutating
```javascript
// Mutating methods (modify original)
push(), pop(), shift(), unshift(), splice(), reverse(), sort(), fill()

// Non-mutating methods (return new array)
slice(), concat(), map(), filter(), reduce(), flat(), flatMap()
```

### 4. Use meaningful variable names
```javascript
// Good
const users = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Jane' }
];
const adminUsers = users.filter(user => user.isAdmin);

// Avoid
const arr = [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }];
const result = arr.filter(x => x.isAdmin);
```

### 5. Chain methods for better readability
```javascript
// Good
const result = users
  .filter(user => user.age >= 18)
  .map(user => user.name)
  .sort();

// Avoid: Multiple intermediate variables
const adults = users.filter(user => user.age >= 18);
const names = adults.map(user => user.name);
const sorted = names.sort();
```

### 6. Be careful with shallow copies
```javascript
const original = [{ id: 1 }, { id: 2 }];
const copy = original.slice();  // Shallow copy

copy[0].id = 999;  // Modifies both original and copy!
console.log(original[0].id);  // 999

// For deep copy, use spread operator or JSON methods
const deepCopy = JSON.parse(JSON.stringify(original));
```

### 7. Handle empty arrays
```javascript
// Good
const numbers = [1, 2, 3];
const doubled = numbers.length > 0 
  ? numbers.map(n => n * 2) 
  : [];

// Or use optional chaining
const result = numbers?.map(n => n * 2) ?? [];
```

---

## Common Patterns

### Remove duplicates
```javascript
const arr = [1, 2, 2, 3, 3, 3, 4];
const unique = [...new Set(arr)];  // [1, 2, 3, 4]
```

### Flatten nested array
```javascript
const nested = [[1, 2], [3, 4], [5, 6]];
const flat = nested.flat();  // [1, 2, 3, 4, 5, 6]
```

### Group by property
```javascript
const users = [
  { department: 'sales', name: 'John' },
  { department: 'sales', name: 'Jane' },
  { department: 'hr', name: 'Bob' }
];

const grouped = users.reduce((acc, user) => {
  (acc[user.department] ??= []).push(user);
  return acc;
}, {});
```

### Partition array
```javascript
const arr = [1, 2, 3, 4, 5, 6];
const [even, odd] = arr.reduce(
  ([evens, odds], num) => 
    num % 2 === 0 
      ? [[...evens, num], odds]
      : [evens, [...odds, num]],
  [[], []]
);
```

### Find all indices of element
```javascript
const arr = [1, 2, 3, 2, 4, 2, 5];
const indices = arr
  .map((val, idx) => val === 2 ? idx : -1)
  .filter(idx => idx !== -1);  // [1, 3, 5]
```

---

## Summary Table

| Method | Mutating | Returns | Usage |
|--------|----------|---------|-------|
| push() | ✓ | length | Add to end |
| pop() | ✓ | element | Remove from end |
| shift() | ✓ | element | Remove from start |
| unshift() | ✓ | length | Add to start |
| splice() | ✓ | array | Add/remove at index |
| map() | ✗ | array | Transform elements |
| filter() | ✗ | array | Select elements |
| reduce() | ✗ | any | Accumulate values |
| forEach() | ✗ | undefined | Iterate elements |
| find() | ✗ | element | Get first match |
| includes() | ✗ | boolean | Check existence |
| concat() | ✗ | array | Combine arrays |
| slice() | ✗ | array | Extract portion |
| sort() | ✓ | array | Sort elements |
| reverse() | ✓ | array | Reverse order |
