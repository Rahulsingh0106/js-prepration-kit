# JavaScript Variables

## 1. What is a Variable?
A variable is a named storage location that holds a value. In JavaScript, variables let you store numbers, text, booleans, objects, arrays, functions, and more.

## 2. Variable Keywords
JavaScript supports three main keywords for declaring variables:

- `var`
  - Function-scoped or globally scoped.
  - Can be re-declared and updated.
  - Hoisted with an initial value of `undefined`.
- `let`
  - Block-scoped.
  - Can be updated but not re-declared in the same scope.
  - Hoisted but not initialized until the declaration is evaluated (temporal dead zone).
- `const`
  - Block-scoped.
  - Must be initialized when declared.
  - Cannot be reassigned, but objects/arrays declared with `const` can still be mutated.

## 3. Declaration vs Assignment
- Declaration: creating the variable name.
  - Example: `let score;`
- Assignment: giving a variable a value.
  - Example: `score = 10;`
- Declaration + assignment at once:
  - `const name = "Aisha";`

## 4. Scope
- Global scope: variable is available everywhere in the script.
- Function scope: variable exists only inside the function.
- Block scope: variable exists inside a block between `{}`.

### Examples
- `var` is function-scoped:
  ```js
  function example() {
    var message = "hello";
  }
  console.log(message); // ReferenceError
  ```
- `let` and `const` are block-scoped:
  ```js
  if (true) {
    let count = 5;
    const status = true;
  }
  console.log(count); // ReferenceError
  ```

## 5. Hoisting
Hoisting means declarations are moved to the top of their scope during JavaScript compilation.

- `var` is hoisted and initialized with `undefined`.
- `let` and `const` are hoisted but not initialized until the code reaches the declaration.

Example:
```js
console.log(a); // undefined
var a = 3;

console.log(b); // ReferenceError
let b = 4;
```

## 6. Best Practices
- Prefer `const` by default.
- Use `let` when the value must change.
- Avoid `var` in modern JavaScript.
- Give meaningful variable names.
- Keep scope as small as possible.

## 7. Common Variable Types
- `number`: `42`, `3.14`
- `string`: `'hello'`, `"JS"`
- `boolean`: `true`, `false`
- `null`: intentional absence of value
- `undefined`: value not assigned yet
- `object`: `{ name: "Rahul" }`
- `array`: `[1, 2, 3]`

## 8. Examples
```js
const firstName = "Rahul";
let age = 22;
var isStudent = true;

age = 23; // allowed with let
// firstName = "Aman"; // not allowed with const
```

## 9. Summary
- Variables store values under a name.
- Use `const` for values that should not change.
- Use `let` for values that can change.
- Avoid `var` unless you need legacy function-scoped behavior.
- Understand scope and hoisting to prevent bugs.
