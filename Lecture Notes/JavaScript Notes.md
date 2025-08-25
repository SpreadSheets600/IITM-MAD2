
# JavaScript Concepts

## 1. Difference between `let`, `var`, and `const`

- **`var`**:
  - **Redeclaration**: Can be redeclared within the same scope.
  - **Scope**: Function-scoped or globally scoped if declared outside a function.
  - **Hoisting**: The declaration is hoisted, but the initialization is not. The variable is initialized with `undefined` until the assignment is made.
  - **Example**:

    ```javascript
    var a = 10;
    var a = 20;  // No error, variable is redeclared
    console.log(a);  // 20
    ```

- **`let`**:
  - **Redeclaration**: Cannot be redeclared within the same scope.
  - **Scope**: Block-scoped.
  - **Hoisting**: The declaration is hoisted, but not the initialization. Accessing it before initialization results in a `ReferenceError`.
  - **Example**:

    ```javascript
    let a = 10;
    let a = 20;  // SyntaxError: Identifier 'a' has already been declared
    ```

- **`const`**:
  - **Redeclaration**: Cannot be redeclared or reassigned after initialization.
  - **Scope**: Block-scoped.
  - **Hoisting**: Like `let`, `const` is hoisted but cannot be accessed before initialization.
  - **Example**:

    ```javascript
    const a = 10;
    const a = 20;  // SyntaxError: Identifier 'a' has already been declared
    a = 30;  // TypeError: Assignment to constant variable.
    ```

---

## 2. Hoisting

- **Definition**: Hoisting is the behavior where JavaScript moves variable declarations (not initializations) to the top of their scope during the compilation phase.
- **Key Points**:
  - Only the declarations are hoisted, not the initializations.
  - Variables declared with `var` are hoisted and initialized with `undefined`.
  - Variables declared with `let` and `const` are hoisted but cannot be accessed before initialization (ReferenceError).

**Example**:

```javascript
console.log(a);  // undefined (due to hoisting)
var a = 10;
console.log(a);  // 10
```

**Key Example for `let` and `const`**:

```javascript
console.log(b);  // ReferenceError: Cannot access 'b' before initialization
let b = 10;
```

**Without Declaration (No Hoisting)**:

```javascript
console.log(c);  // ReferenceError: c is not defined
c = 10;  // Even though c is a 'var' variable, it is not hoisted.
```

---

## 3. Semicolons in JavaScript

- **Semicolons** are optional in JavaScript, but they are **necessary** when multiple statements are written on the same line.

**Example**:

- **Without a semicolon (works fine)**:

  ```javascript
  let a = 10
  let b = 20
  console.log(a, b);  // 10 20
  ```

- **With multiple statements on one line (causes an error without semicolons)**:

  ```javascript
  let a = 10 let b = 20;  // SyntaxError: Unexpected token
  ```

- **With semicolons (works as expected)**:

  ```javascript
  let a = 10; let b = 20;  // No error
  console.log(a, b);  // 10 20
  ```

---

## 4. Global Execution Context (GEC) and Function Execution Context (FEC)

- **Global Execution Context (GEC)**:
  - Created when the JavaScript program begins execution. It is the global context for the entire program.
  - **Memory Allocation**: Allocates memory for variables and functions, initializing them with `undefined`.
  - **Hoisting**: Variables are hoisted, and their values are initially set to `undefined`.

**Example**:

```javascript
console.log(a);  // undefined (due to hoisting)
var a = 10;
console.log(a);  // 10
```

- **Function Execution Context (FEC)**:
  - Created whenever a function is invoked.
  - Memory is allocated for the function’s local variables.
  - The FEC is destroyed once the function completes execution, and control is returned to the GEC.

**Flow of Execution**:

1. **Global Execution Context (GEC)**: Memory allocation and hoisting for global variables/functions.
2. **Function Execution Context (FEC)**: Created when a function is called, it has its own memory allocation and execution flow.
3. **Thread of Execution**: JavaScript is executed line-by-line. The program executes in the order the statements appear.
4. **Completion**: Once a function execution is completed, its FEC is destroyed, and execution continues in the GEC.

**Flowchart of GEC**:

```plaintext
+-----------------------+
|    Global Context     |
+-----------------------+
         |
         v
+---------------------------+
| Memory Allocation Phase   |<--- Variables and functions are hoisted here (initialized as undefined)
+---------------------------+
         |
         v
+---------------------------+
| Thread of Execution       |<--- Execution starts line-by-line
+---------------------------+
         |
         v
+---------------------------+
| Completion                |<--- Function context cleared after execution
+---------------------------+
```

---

## 5. Memory Allocation in GEC and FEC

- **Memory in GEC**:
  - Memory for global variables and functions is allocated at the start.
  - Functions are allocated their actual definitions.

**Example**:

```javascript
var a = 10;  // Memory is allocated for 'a' with the value 10
function abc(x) { return x * x; }  // Memory is allocated with function definition
```

- **Memory in FEC**:
  - When a function is invoked, a new memory block is created for its local variables.
  - Local variables are initialized to `undefined` initially.

---

## 6. Function Calls and Execution Contexts

- **Calling a Function**:
  - When a function is invoked, a new **FEC** is created.
  - The memory allocation phase occurs for the function’s local variables.
  - The function executes line-by-line, and once it finishes, the FEC is destroyed.

**Example**:

```javascript
function abc(x) {
    return x * x;
}

var result = abc(4);  // 16 (Function is invoked, FEC created)
```

---

## 7. Variable Scoping Between GEC and FEC

- Variables declared in the **GEC** (global scope) are accessible inside the **FEC** (local scope) of a function.
- **Local variables** declared inside an FEC are not accessible from the GEC.

**Example**:

```javascript
var x = 10;  // Global scope

function abc(y) {
    return x + y;  // x is accessible because it is in the GEC
}

console.log(abc(5));  // 15
```

**Example with function scope**:

```javascript
function abc(x) {
    var y = 5;  // Local to function
    return x + y;
}

console.log(abc(4));  // 9
console.log(y);  // ReferenceError: y is not defined (y is local to the function)
```

