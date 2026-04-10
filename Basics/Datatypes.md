# JavaScript Data Types and String Operations

## 1. String Indexing

Strings in JavaScript are zero-indexed, meaning the first character is at position 0.

### Accessing Characters
```js
const message = "Hello World";

// Access individual characters
console.log(message[0]);    // "H"
console.log(message[6]);    // "W"
console.log(message[11]);   // undefined (out of bounds)

// Get string length
console.log(message.length); // 11
```

### Negative Indexing
JavaScript doesn't support negative indexing like Python, but you can calculate from the end:
```js
const text = "JavaScript";
const lastChar = text[text.length - 1]; // "t"
const secondLast = text[text.length - 2]; // "p"
```

## 2. Useful String Methods

### Common String Methods

#### `toUpperCase()` and `toLowerCase()`
```js
const name = "john doe";
console.log(name.toUpperCase()); // "JOHN DOE"
console.log(name.toLowerCase()); // "john doe"
```

#### `indexOf()` and `lastIndexOf()`
```js
const sentence = "The quick brown fox jumps over the lazy dog";
console.log(sentence.indexOf("fox"));      // 16
console.log(sentence.lastIndexOf("o"));    // 42
console.log(sentence.indexOf("cat"));      // -1 (not found)
```

#### `includes()`, `startsWith()`, `endsWith()`
```js
const text = "JavaScript is awesome";
console.log(text.includes("Script"));     // true
console.log(text.startsWith("Java"));     // true
console.log(text.endsWith("some"));       // true
```

#### `slice()`, `substring()`, `substr()`
```js
const str = "Hello World";

// slice(start, end) - end not included
console.log(str.slice(0, 5));     // "Hello"
console.log(str.slice(6));        // "World"
console.log(str.slice(-5));       // "World"

// substring(start, end) - similar to slice but doesn't accept negative indices
console.log(str.substring(0, 5)); // "Hello"

// substr(start, length) - deprecated, avoid using
console.log(str.substr(6, 5));    // "World"
```

#### `replace()` and `replaceAll()`
```js
let text = "I love cats. Cats are cute.";
console.log(text.replace("cats", "dogs"));     // "I love dogs. Cats are cute."
console.log(text.replaceAll("cats", "dogs"));  // "I love dogs. Dogs are cute."
```

#### `trim()`, `trimStart()`, `trimEnd()`
```js
const padded = "  Hello World  ";
console.log(padded.trim());       // "Hello World"
console.log(padded.trimStart());  // "Hello World  "
console.log(padded.trimEnd());    // "  Hello World"
```

#### `split()` and `join()`
```js
const csv = "apple,banana,orange";
const fruits = csv.split(",");           // ["apple", "banana", "orange"]
console.log(fruits.join(" | "));         // "apple | banana | orange"

const sentence = "This is a sentence";
const words = sentence.split(" ");       // ["This", "is", "a", "sentence"]
```

#### `repeat()` and `padStart()`/`padEnd()`
```js
console.log("Ha".repeat(3));             // "HaHaHa"

const num = "5";
console.log(num.padStart(3, "0"));       // "005"
console.log(num.padEnd(3, "0"));         // "500"
```

## 3. Template Strings (Template Literals)

Template strings use backticks (`) instead of quotes and allow embedded expressions.

### Basic Usage
```js
const name = "Alice";
const greeting = `Hello, ${name}!`;
console.log(greeting); // "Hello, Alice!"
```

### Multi-line Strings
```js
const multiLine = `This is a
multi-line
string`;
console.log(multiLine);
```

### Expressions in Template Strings
```js
const a = 5;
const b = 10;
console.log(`Sum: ${a + b}`);           // "Sum: 15"
console.log(`Random: ${Math.random()}`); // "Random: 0.12345..."
```

### Tagged Templates
```js
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) =>
    result + str + (values[i] ? `<strong>${values[i]}</strong>` : ''), '');
}

const name = "World";
const result = highlight`Hello ${name}! Welcome to ${2024}!`;
// "Hello <strong>World</strong>! Welcome to <strong>2024</strong>!"
```

## 4. Null, Undefined, BigInt, and typeof

### `null`
- Represents the intentional absence of any object value
- Must be assigned explicitly
- `typeof null` returns `"object"` (this is a historical bug in JavaScript)

```js
let emptyValue = null;
console.log(emptyValue);        // null
console.log(typeof emptyValue); // "object"
```

### `undefined`
- Represents a variable that has been declared but not assigned a value
- Default value for uninitialized variables
- `typeof undefined` returns `"undefined"`

```js
let notAssigned;
console.log(notAssigned);        // undefined
console.log(typeof notAssigned); // "undefined"

function noReturn() {}
console.log(noReturn());         // undefined
```

### `BigInt`
- Represents integers larger than `Number.MAX_SAFE_INTEGER` (2^53 - 1)
- Created by appending `n` to an integer or using `BigInt()` constructor
- Cannot be mixed with regular numbers in operations

```js
const bigNum = 123456789012345678901234567890n;
const anotherBig = BigInt("123456789012345678901234567890");

console.log(bigNum + anotherBig); // 246913578024691357802469135780n
console.log(typeof bigNum);       // "bigint"

// Mixing with numbers requires conversion
const num = 10;
console.log(bigNum + BigInt(num)); // 123456789012345678901234567900n
```

### `typeof` Operator
Returns a string indicating the type of the operand.

```js
console.log(typeof "hello");     // "string"
console.log(typeof 42);          // "number"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof null);        // "object" (quirk)
console.log(typeof {});          // "object"
console.log(typeof []);          // "object"
console.log(typeof function(){}); // "function"
console.log(typeof 42n);         // "bigint"
console.log(typeof Symbol());    // "symbol"
```

## 5. Booleans and Comparison Operators

### Boolean Values
- `true` or `false`
- Can be created explicitly or as a result of comparisons

```js
const isTrue = true;
const isFalse = false;
console.log(typeof isTrue);  // "boolean"
```

### Truthy and Falsy Values
JavaScript has truthy and falsy values that evaluate to `true` or `false` in boolean contexts:

**Falsy values:**
- `false`
- `0`, `-0`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

**Truthy values:** Everything else

```js
console.log(Boolean(0));        // false
console.log(Boolean(""));       // false
console.log(Boolean(null));     // false
console.log(Boolean("hello"));  // true
console.log(Boolean(42));       // true
console.log(Boolean({}));       // true
```

### Comparison Operators

#### Equality Operators
```js
// Loose equality (==) - performs type coercion
console.log(5 == "5");          // true
console.log(0 == false);        // true
console.log(null == undefined); // true

// Strict equality (===) - no type coercion
console.log(5 === "5");         // false
console.log(0 === false);       // false
console.log(null === undefined); // false
```

#### Relational Operators
```js
console.log(5 > 3);     // true
console.log(5 < 3);     // false
console.log(5 >= 5);    // true
console.log(5 <= 4);    // false
```

#### Logical Operators
```js
const a = true;
const b = false;

console.log(a && b);    // false (AND)
console.log(a || b);    // true (OR)
console.log(!a);        // false (NOT)
```

#### String Comparisons
```js
console.log("apple" < "banana");     // true (lexicographical order)
console.log("Apple" < "apple");      // true (uppercase comes before lowercase)
console.log("2" < "10");             // false (string comparison, not numeric)
console.log("2" < 10);               // true (type coercion to number)
```

### Best Practices
- Use `===` instead of `==` to avoid unexpected type coercion
- Be careful with `null` and `undefined` comparisons
- Use `Boolean()` to explicitly convert values to booleans
- Remember that `typeof null` returns `"object"` (quirk)
- Use `BigInt` for very large integers, but avoid mixing with regular numbers

## Summary
- Strings are zero-indexed and have many useful methods
- Template strings provide powerful string interpolation
- `null` and `undefined` represent absence of value but behave differently
- `BigInt` handles large integers safely
- `typeof` helps identify data types
- Booleans have truthy/falsy concepts and comparison operators require careful use