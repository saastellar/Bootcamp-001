# Lecture #002 📌

### **<ins>JavaScript: Variables, Data Types, and Data Manipulation</ins>**

***

This lecture provides a **deep dive into variables, data types, and how to manipulate data in JavaScript**. This topic is fundamental to understanding how JavaScript works and is crucial for anyone learning or working with the language.

***

### **1. Variables in JavaScript**

#### **1.1. Variable Declaration**

In JavaScript, you can declare variables using `var`, `let`, and `const`. Each of these behaves differently and is used in specific scenarios.

##### **1.1.1. ****`var`**

* **Scope**: Function-scoped (not block-scoped). This means `var` is scoped to the nearest function block and is not confined to `if`, `for`, or other block-level constructs.
* **Hoisting**: `var` declarations are **hoisted** to the top of their scope, meaning you can reference the variable even before it is declared.
   
  ```javascript
  console.log(x); // undefined
  var x = 5;
  console.log(x); // 5
  ```

&#x20; \`\`\`
 

* **Issues with ****`var`**: Due to hoisting and lack of block scope, `var` can lead to unexpected behavior and bugs.

##### **1.1.2. ****`let`**

* **Scope**: Block-scoped. This means `let` variables are confined to the nearest block in which they are defined (e.g., inside an `if`, `for`, or `{}` block).
   
  ```javascript
  if (true) {
      let y = 10;
      console.log(y); // 10
  }
  console.log(y); // ReferenceError: y is not defined
  ```

&#x20; \`\`\`

* **Re-declaration**: Unlike `var`, you **cannot re-declare** a `let` variable in the same scope.
  ```javascript
  let a = 3;
  let a = 5; // SyntaxError: Identifier 'a' has already been declared
  ```

&#x20; \`\`\`

* **Hoisting**: `let` variables are hoisted but are not initialized, meaning you cannot access them before their declaration (this results in a **temporal dead zone** error).

##### **1.1.3. ****`const`**

* **Scope**: Block-scoped like `let`.
* **Constant**: Once assigned, the value of a `const` variable **cannot be reassigned**.
   
  ```javascript
  const z = 15;
  z = 20; // TypeError: Assignment to constant variable.
  ```

&#x20; \`\`\`

* **Objects and Arrays**: While the variable itself cannot be reassigned, the contents of **objects** or **arrays** declared with `const` can still be modified.
  ```javascript
  const arr = [1, 2, 3];
  arr.push(4); // Valid
  console.log(arr); // [1, 2, 3, 4]

  const obj = { name: "John" };
  obj.name = "Doe"; // Valid
  console.log(obj); // { name: "Doe" }
  ```

&#x20; \`\`\`

* **Hoisting**: `const` is also hoisted but remains uninitialized until the actual line where it is defined (temporal dead zone).

***

### **2. JavaScript Data Types**

JavaScript is a dynamically typed language, meaning variables do not have a fixed type and can change types at runtime. There are **two categories of data types**: **primitive** and **reference** types.

#### **2.1. Primitive Data Types**

Primitive data types are immutable and are stored directly by value. JavaScript has 7 primitive data types:

1. **String**
   * Used to represent textual data.
   * Can be declared with single (`'`), double (`"`), or backticks (`` ` ``).
      
   ```javascript
   let str = "Hello";
   let templateStr = `Hello, ${name}!`; // Template literals allow embedded expressions.
   ```

&#x20;  \`\`\`

1. **Number**
   * Represents both integers and floating-point numbers.
   * JavaScript uses **64-bit floating point** for numbers, which means integers and decimals are handled under the same type.
      
   ```javascript
   let num1 = 42;
   let num2 = 3.14;
   let bigNum = 2e53; // Large numbers
   ```

&#x20;  \`\`\`

* **NaN (Not-a-Number)**: A special value representing "Not a Number", typically returned when an operation fails.
1. **Boolean**
   * Represents `true` or `false` values.
      
   ```javascript
   let isUserActive = true;
   let isSubscribed = false;
   ```
&#x20;  \`\`\`
1. **Null**
   * Represents the intentional absence of any object value.
      
   ```javascript
   let empty = null;
   ```
&#x20;  \`\`\`
1. **Undefined**
   * A variable is `undefined` when it is declared but not initialized.
      
   ```javascript
   let x;
   console.log(x); // undefined
   ```
&#x20;  \`\`\`
1. **Symbol** (ES6)
   * A unique and immutable value that is often used as object keys.
      
   ```javascript
   const sym = Symbol('description');
   ```
&#x20;  \`\`\`
1. **BigInt** (ES2020)
   * Used for representing integers larger than the safe range for Numbers (`2^53 - 1`).
      
   ```javascript
   let bigIntNum = 9007199254740991n; // Use "n" at the end to denote a BigInt.
   ```
&#x20;  \`\`\`
#### **2.2. Reference Data Types**
Reference types are objects stored as references (pointers) and include:
1. **Object**
   * A collection of key-value pairs, where keys are strings (or Symbols) and values can be any type (including functions).
      
   ```javascript
   let person = {
       name: 'John',
       age: 30,
       greet: function() {
           console.log("Hello");
       }
   };
   ```
&#x20;  \`\`\`
1. **Array**
   * Special type of object that holds ordered collections of values.
      
   ```javascript
   let fruits = ['apple', 'banana', 'mango'];
   console.log(fruits[0]); // apple
   ```
&#x20;  \`\`\`
1. **Function**
   * A special object type that represents reusable code blocks.
      
   ```javascript
   function greet() {
       console.log("Hello");
   }
   ```
&#x20;  \`\`\`
1. **Date, RegExp, Map, Set, etc.**
   * JavaScript has built-in objects like `Date`, `RegExp`, `Map`, and `Set`.
***
### **3. Data Manipulation in JavaScript**
Data manipulation refers to how you can operate on different data types in JavaScript. Here's how it's done with primitive and reference types:
#### **3.1. Strings**
**Common String Operations**:
* **Concatenation**:
  ```javascript
  let firstName = 'John';
  let lastName = 'Doe';
  let fullName = firstName + ' ' + lastName;
  ```

&#x20; \`\`\`

* **Template Literals** (ES6):
  ```javascript
  let greeting = `Hello, ${firstName} ${lastName}`;
  ```

&#x20; \`\`\`

* **String Methods**:
  * `length`: Returns the length of the string.
  * `toUpperCase()`, `toLowerCase()`: Case conversion.
  * `indexOf()`: Finds the index of a substring.
  * `substring()`: Extracts a portion of the string.
  * `trim()`: Removes whitespace from both ends.
  ```javascript
  let text = " JavaScript ";
  console.log(text.trim()); // "JavaScript"
  ```

&#x20; \`\`\`

#### **3.2. Numbers**

**Number Operations**:

* Arithmetic: `+`, `-`, `*`, `/`, `%` (modulo).
* Math methods: `Math.pow()`, `Math.sqrt()`, `Math.random()`, `Math.round()`.
   

```javascript
let a = 10;
let b = 3;
console.log(a % b); // 1 (modulo operation)
```

* **Type Coercion**: JavaScript automatically converts between types when necessary (though this can sometimes lead to unexpected results).
  ```javascript
  let x = '5';
  let y = 3;
  console.log(x + y); // '53' (string concatenation, not addition)
  ```

&#x20; \`\`\`

&#x20; Use `Number()` or `parseInt()`/`parseFloat()` to convert explicitly.

#### **3.3. Arrays**

**Array Methods**:

* **Push**: Adds an element to the end.
* **Pop**: Removes the last element.
* **Shift**: Removes the first element.
* **Unshift**: Adds an element to the beginning.
* **Map**: Applies a function to each element and returns a new array.
* **Filter**: Returns a new array with elements that pass the condition.
* **Reduce**: Accumulates values by applying a function to all elements.

```javascript
let numbers = [1, 2, 3, 4];
let doubled = numbers.map(n => n * 2); // [2, 4, 6, 8]
let evens = numbers.filter(n => n % 2 === 0); // [2, 4]
let sum = numbers.reduce((acc, cur) => acc + cur, 0); // 10
```

#### **3.4. Objects**

**Accessing Properties**:

* Dot notation: `obj.property`.
* Bracket notation: \`obj\['

property']\`.

```javascript
let person = {
    name: "Alice",
    age: 25,
};
console.log(person.name); // Alice
```

* **Adding/Modifying Properties**:
  ```javascript
  person.gender = 'female';
  ```

&#x20; \`\`\`

* **Object Methods**:
  * `Object.keys()`: Returns an array of property names.
  * `Object.values()`: Returns an array of property values.
  * `Object.assign()`: Merges objects.

#### **3.5. Functions**

* **Function Declaration**:
  ```javascript
  function greet() {
      return "Hello!";
  }
  ```

&#x20; \`\`\`

* **Arrow Functions** (ES6):
  ```javascript
  const greet = () => "Hello!";
  ```

&#x20; \`\`\`

* **Higher-Order Functions**: Functions that take other functions as arguments or return functions.
   
  ```javascript
  const higherOrder = (callback) => callback();
  ```

&#x20; \`\`\`

***

### **4. Type Coercion and Type Checking**

JavaScript automatically converts data types when necessary. This is called **type coercion**.

* **Implicit Coercion**:
  ```javascript
  let result = '5' + 2; // '52' (string concatenation, not addition)
  ```

&#x20; \`\`\`

* **Explicit Coercion**:
  &#x20; Use functions like `String()`, `Number()`, `Boolean()` to convert explicitly.

***

### **\<u>APIs, Promises, Async/Await: Deep Dive into JavaScript Asynchronous Programming\</u>**

we'll cover everything you need to know about **API calls, functions, promises, async/await, error handling, and more**. JavaScript’s asynchronous nature is one of its most powerful features, enabling modern web applications to handle operations like network requests without blocking the main thread.

***

### **1. API Calls in JavaScript**

An **API** (Application Programming Interface) allows one system to communicate with another. When dealing with **web APIs**, we often make **HTTP requests** to send or receive data from a server.

#### **1.1. Types of API Calls (HTTP Methods)**

* **GET**: Retrieve data from the server.
* **POST**: Send data to the server.
* **PUT**: Update existing data on the server.
* **DELETE**: Remove data from the server.

Example of making an HTTP request:

```javascript
fetch('https://api.example.com/data') // GET request
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

* `fetch()`: A modern, native JavaScript method for making HTTP requests, which returns a **Promise**.
* `.then()`: Called when the request is successful.
* `.catch()`: Called when an error occurs during the request.

#### **1.2. Request Headers, Body, and Query Parameters**

* **Headers**: Provide metadata for the request, such as content type, authorization, etc.
* **Query Parameters**: Data sent in the URL itself (for `GET` requests).
* **Body**: Data sent in the body of the request (for `POST`, `PUT`, `PATCH` requests).

```javascript
fetch('https://api.example.com/data?search=term', {
    method: 'POST', // or 'PUT'
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer token'
    },
    body: JSON.stringify({ key: 'value' }) // Send data in request body
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

* **`Content-Type`**** header**: Indicates the format of the data sent (e.g., `application/json`, `application/x-www-form-urlencoded`).
* **Authorization**: Often includes authentication tokens (e.g., OAuth tokens, API keys).

***

### **2. Promises**

JavaScript uses **Promises** to handle asynchronous operations. A **Promise** is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

#### **2.1. The Structure of a Promise**

A promise can be in one of three states:

1. **Pending**: The operation has not yet completed.
2. **Fulfilled**: The operation completed successfully.
3. **Rejected**: The operation failed.

Here’s a simple example:

```javascript
const promise = new Promise((resolve, reject) => {
    let success = true;

    if (success) {
        resolve("Operation succeeded!");
    } else {
        reject("Operation failed.");
    }
});

// Handling the Promise
promise
    .then(result => {
        console.log(result); // "Operation succeeded!"
    })
    .catch(error => {
        console.log(error); // "Operation failed."
    });
```

* **`resolve()`**: Called when the operation completes successfully.
* **`reject()`**: Called when the operation fails.
* **`then()`**: Executes when the promise is resolved (fulfilled).
* **`catch()`**: Executes when the promise is rejected.

#### **2.2. Chaining Promises**

You can chain multiple `.then()` methods to handle sequential asynchronous operations.

```javascript
const fetchData = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve("Data fetched!"), 2000);
    });
};

fetchData()
    .then(response => {
        console.log(response); // "Data fetched!"
        return response + " Processed.";
    })
    .then(extendedResponse => {
        console.log(extendedResponse); // "Data fetched! Processed."
    })
    .catch(error => {
        console.error(error);
    });
```

* Each `.then()` in the chain returns a new promise, which can either resolve with a value (which is passed to the next `.then()`) or reject with an error (handled by `.catch()`).

#### **2.3. Promise.all() and Promise.race()**

* **`Promise.all()`**: Runs multiple promises concurrently and waits for all of them to resolve or reject.
  ```javascript
  const promise1 = Promise.resolve("First Promise");
  const promise2 = Promise.resolve("Second Promise");
  const promise3 = Promise.resolve("Third Promise");

  Promise.all([promise1, promise2, promise3])
    .then(results => {
        console.log(results); // ["First Promise", "Second Promise", "Third Promise"]
    });
  ```

&#x20; \`\`\`

* **`Promise.race()`**: Resolves as soon as the first promise in the array resolves or rejects.
  ```javascript
  const promise1 = new Promise((resolve) => setTimeout(resolve, 500, 'First Promise'));
  const promise2 = new Promise((resolve) => setTimeout(resolve, 100, 'Second Promise'));

  Promise.race([promise1, promise2])
    .then(result => {
        console.log(result); // "Second Promise"
    });
  ```

&#x20; \`\`\`

***

### **3. Async/Await**

**Async/await** is a modern syntax for handling asynchronous code. It makes asynchronous code look and behave more like synchronous code, which can improve readability.

#### **3.1. How Async/Await Works**

* **`async`**** function**: Declares a function that returns a **Promise**.
* **`await`**** expression**: Pauses the execution of the `async` function until the promise is resolved.

```javascript
async function fetchData() {
    let response = await fetch('https://api.example.com/data');
    let data = await response.json();
    return data;
}

fetchData().then(data => console.log(data));
```

#### **3.2. Example with Try/Catch for Error Handling**

You can handle errors in `async` functions using `try/catch` blocks:

```javascript
async function getData() {
    try {
        let response = await fetch('https://api.example.com/data');
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error:', error);
    }
}

getData();
```

* **`try/catch`**: Use `try/catch` to handle errors thrown within the `async` function.
* **`response.ok`**: Checks if the HTTP request was successful (status code 200-299).

#### **3.3. Combining Promises with Async/Await**

You can still combine **`Promise.all()`** with `async/await`:

```javascript
async function fetchMultipleData() {
    const [data1, data2, data3] = await Promise.all([
        fetch('https://api.example.com/data1').then(res => res.json()),
        fetch('https://api.example.com/data2').then(res => res.json()),
        fetch('https://api.example.com/data3').then(res => res.json())
    ]);
    console.log(data1, data2, data3);
}

fetchMultipleData();
```

***

### **4. Error Handling in Asynchronous Code**

When dealing with asynchronous code (whether using **Promises** or **async/await**), it’s important to handle errors properly.

#### **4.1. Using ****`.catch()`**** for Promises**

When chaining promises, you can handle errors using `.catch()`:

```javascript
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

#### **4.2. Using ****`try/catch`**** with Async/Await**

In an `async` function, errors are typically handled with `try/catch` blocks:

```javascript
async function fetchData() {
    try {
        let response = await fetch('https://api.example.com/data');
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error:', error);
    }
}

fetchData();
```

#### **4.3. Custom Error Handling**

You can also throw custom errors within async functions or promise chains:

```javascript
async function getData() {
    let response = await fetch('https://api.example.com/data');
    if (!response.ok) {
        throw new Error('Failed to fetch data');
    }
    return await response.json();
}

getData()
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

***

### **Why Does a Promise Need to Be Resolved?**

In JavaScript, a **Promise** is an object representing the eventual completion (or failure) of an asynchronous operation. Promises allow you to handle asynchronous tasks like fetching data, performing background calculations, or waiting for events. Since these tasks take time, JavaScript uses promises to manage their completion or failure without blocking the rest of the code.

#### **Why Resolution is Necessary**

When you create a promise, it’s in a pending state. Eventually, it will either:

* **Resolve**: The asynchronous operation was successful, and the promise is fulfilled.
* **Reject**: The operation failed, and the promise is rejected.

Without resolving or rejecting, the promise would stay in the pending state forever, and you wouldn’t be able to tell when the asynchronous task is done or handle any results/errors from it.

***

### **Real-Life Example: Pizza Delivery**

Let’s compare promises and asynchronous behavior with a common real-life scenario: ordering pizza.

1. **You order a pizza (the async task starts)**.
   * This doesn’t happen instantly; it takes time to prepare and deliver.
2. **The promise (pending state)**: You don't know whether it will be delivered yet or not; you just have the promise from the restaurant.
3. **Pizza delivered (promise is resolved)**: The promise is fulfilled when the pizza arrives.
4. **Pizza delivery failed (promise is rejected)**: If there’s an issue (e.g., the delivery is canceled), the promise is rejected, and you get a failure message.

***

### **Code Example**

Let's simulate the pizza delivery scenario in JavaScript using a promise:

```javascript
function orderPizza() {
    return new Promise((resolve, reject) => {
        console.log("Ordering pizza...");

        // Simulating the time it takes to deliver a pizza
        setTimeout(() => {
            const deliverySuccess = Math.random() > 0.5; // Randomly decide success or failure

            if (deliverySuccess) {
                resolve("Pizza delivered successfully!");
            } else {
                reject("Pizza delivery failed.");
            }
        }, 3000); // Simulate a 3-second delivery time
    });
}

orderPizza()
    .then((message) => {
        console.log(message); // Success: Pizza delivered
    })
    .catch((error) => {
        console.log(error); // Failure: Delivery failed
    });
```

### **How it Works**:

* **Pending State**: When you call `orderPizza()`, the promise is created, and the state is pending while waiting for the pizza to be delivered.



* **Resolution (Fulfilled)**: If the pizza is delivered successfully, `resolve()` is called, and the `.then()` block executes.
* **Rejection (Failed)**: If something goes wrong, `reject()` is called, and the `.catch()` block handles the failure.

***

### **Real-Life Example: Movie Ticket Booking**

Imagine booking a movie ticket online. Once you request a ticket, the system checks seat availability, processes your payment, and then issues the ticket. This is also an asynchronous task because it takes time.

1. **Request a ticket (async task)**: You ask for a seat in a specific theater.
2. **Pending (promise state)**: You wait for the system to check availability and process your request.
3. **Resolved (fulfilled)**: The system finds a seat, processes your payment, and sends the ticket.
4. **Rejected (failed)**: If the payment fails or no seats are available, the promise is rejected, and you get a failure notification.

***

### **Code Example**

```javascript
function bookTicket(seat) {
    return new Promise((resolve, reject) => {
        console.log(`Requesting seat ${seat}...`);

        setTimeout(() => {
            const seatAvailable = Math.random() > 0.3; // 70% chance the seat is available

            if (seatAvailable) {
                resolve(`Seat ${seat} booked successfully!`);
            } else {
                reject(`Seat ${seat} is not available.`);
            }
        }, 2000); // Simulate a 2-second delay for booking
    });
}

bookTicket(5)
    .then((message) => {
        console.log(message); // Success: Seat booked
    })
    .catch((error) => {
        console.log(error); // Failure: Seat not available
    });
```

In this case, the system takes some time to check if the seat is available and then either resolves the promise (ticket booked) or rejects it (seat not available).

***

### **How Asynchronous Tasks Work in Real Life**

#### **1. Coffee Shop Example (Real-Life Async Task)**

At a coffee shop, you order a latte. This is an asynchronous task because it takes time to make the coffee.

* **Order Placed**: You place your order (async task starts).
* **Pending**: The barista is preparing your coffee.
* **Resolved**: The coffee is ready, and you get your drink.
* **Rejected**: If the machine breaks, your order fails, and you don’t get your coffee.

```javascript
function orderLatte() {
    return new Promise((resolve, reject) => {
        console.log("Latte order placed...");

        setTimeout(() => {
            const machineWorking = Math.random() > 0.2; // 80% chance the machine works

            if (machineWorking) {
                resolve("Latte is ready!");
            } else {
                reject("Sorry, the machine is broken.");
            }
        }, 4000); // Simulate a 4-second coffee preparation time
    });
}

orderLatte()
    .then((message) => {
        console.log(message); // Coffee is ready
    })
    .catch((error) => {
        console.log(error); // Coffee preparation failed
    });
```

***

### **Promises, ****`async/await`****, and Real-Life Examples**

#### **Understanding ****`async/await`**

In JavaScript, `async/await` makes working with promises more intuitive by using a synchronous-style syntax for asynchronous code.

1. **`async`**** Function**: Declares that a function will return a promise.
2. **`await`**: Pauses the execution of the `async` function until the promise is resolved.

### **Real-Life Example with ****`async/await`****: Online Shopping**

When you order multiple items online, you may need to wait for several operations like confirming availability, processing payment, and preparing the package. Let's simulate this using `async/await`.

```javascript
function checkStock(item) {
    return new Promise((resolve, reject) => {
        console.log(`Checking stock for ${item}...`);
        setTimeout(() => {
            const inStock = Math.random() > 0.2; // 80% chance item is in stock
            if (inStock) {
                resolve(`${item} is available.`);
            } else {
                reject(`${item} is out of stock.`);
            }
        }, 1000);
    });
}

function processPayment() {
    return new Promise((resolve, reject) => {
        console.log("Processing payment...");
        setTimeout(() => {
            const paymentSuccess = Math.random() > 0.1; // 90% chance payment is successful
            if (paymentSuccess) {
                resolve("Payment successful.");
            } else {
                reject("Payment failed.");
            }
        }, 1500);
    });
}

async function placeOrder(item) {
    try {
        const stockMessage = await checkStock(item);
        console.log(stockMessage);

        const paymentMessage = await processPayment();
        console.log(paymentMessage);

        console.log(`${item} order completed.`);
    } catch (error) {
        console.log(error);
    }
}

placeOrder("Laptop");
```

### **Key Points**:

* The `placeOrder` function waits for stock to be checked and payment to be processed in sequence.
* If either operation fails, the error is caught and handled gracefully using `try/catch`.
* This makes it easier to read and maintain compared to traditional promise chaining with `.then()` and `.catch()`.

***
