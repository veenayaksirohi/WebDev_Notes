# 🔒 Scope and Closures

## 🎯 Understanding Scope

Scope determines where variables and functions are accessible in your code. JavaScript uses **lexical scoping**, meaning the scope is determined by where variables and functions are declared in the code.

```mermaid
graph TD
    A[JavaScript Scope] --> B[🌍 Global Scope]
    A --> C[⚙️ Function Scope]
    A --> D[🧱 Block Scope]
    A --> E[🔗 Lexical Scope]
    
    B --> B1[Window/Global Object<br/>Accessible Everywhere<br/>var declarations]
    C --> C1[Function Parameters<br/>var declarations<br/>function declarations]
    D --> D1[let/const declarations<br/>Inside {} blocks<br/>Loop variables]
    E --> E1[Nested Functions<br/>Closure Creation<br/>Variable Resolution]
```

## 🌍 Global Scope

Variables declared in the global scope are accessible from anywhere in your program.

```javascript
// Global scope variables
var globalVar = "I'm global with var";
let globalLet = "I'm global with let";
const globalConst = "I'm global with const";

// Global function
function globalFunction() {
    console.log("I'm a global function");
}

// Accessing global variables from anywhere
function testGlobalAccess() {
    console.log(globalVar);     // Output: I'm global with var
    console.log(globalLet);     // Output: I'm global with let
    console.log(globalConst);   // Output: I'm global with const
    globalFunction();           // Output: I'm a global function
}

testGlobalAccess();

// In browser: global variables become properties of window object
// console.log(window.globalVar); // "I'm global with var"
// console.log(window.globalLet); // undefined (let/const don't attach to window)

// Global scope pollution (avoid this)
function badPractice() {
    implicitGlobal = "I'm accidentally global!"; // No var/let/const
}

badPractice();
console.log(implicitGlobal); // Output: I'm accidentally global!
```

## ⚙️ Function Scope

Variables declared inside a function are only accessible within that function.

```javascript
function demonstrateFunctionScope() {
    var functionVar = "I'm function scoped";
    let functionLet = "I'm also function scoped";
    const functionConst = "Me too!";
    
    function innerFunction() {
        console.log(functionVar);   // Accessible
        console.log(functionLet);   // Accessible
        console.log(functionConst); // Accessible
    }
    
    innerFunction();
    return "Function completed";
}

demonstrateFunctionScope();

// These will throw ReferenceError
// console.log(functionVar);   // ReferenceError
// console.log(functionLet);   // ReferenceError
// console.log(functionConst); // ReferenceError

// Function parameters are function-scoped
function greet(name, greeting = "Hello") {
    var message = `${greeting}, ${name}!`;
    
    function createResponse() {
        return message; // Can access parameter and local variable
    }
    
    return createResponse();
}

console.log(greet("Alice")); // Output: Hello, Alice!
// console.log(name);        // ReferenceError: name is not defined

// var vs let/const in function scope
function scopeComparison() {
    console.log(hoistedVar); // Output: undefined (hoisted)
    // console.log(notHoisted); // ReferenceError (temporal dead zone)
    
    var hoistedVar = "I'm hoisted";
    let notHoisted = "I'm not hoisted";
    
    console.log(hoistedVar); // Output: I'm hoisted
    console.log(notHoisted); // Output: I'm not hoisted
}

scopeComparison();
```

## 🧱 Block Scope

Block scope is created by curly braces `{}` and applies to `let` and `const` declarations.

```javascript
// Block scope with if statement
if (true) {
    var blockVar = "I escape the block";
    let blockLet = "I'm trapped in the block";
    const blockConst = "Me too!";
    
    console.log(blockVar);   // Output: I escape the block
    console.log(blockLet);   // Output: I'm trapped in the block
    console.log(blockConst); // Output: Me too!
}

console.log(blockVar);   // Output: I escape the block
// console.log(blockLet);   // ReferenceError
// console.log(blockConst); // ReferenceError

// Block scope in loops
for (let i = 0; i < 3; i++) {
    let loopVariable = `Iteration ${i}`;
    console.log(loopVariable);
}

// console.log(i);            // ReferenceError
// console.log(loopVariable); // ReferenceError

// Classic var problem in loops
console.log("var in loops:");
for (var j = 0; j < 3; j++) {
    setTimeout(() => {
        console.log(`var j: ${j}`); // Output: var j: 3 (three times)
    }, 100);
}

// Fixed with let
console.log("let in loops:");
for (let k = 0; k < 3; k++) {
    setTimeout(() => {
        console.log(`let k: ${k}`); // Output: let k: 0, let k: 1, let k: 2
    }, 200);
}

// Block scope with try-catch
try {
    let tryVariable = "I'm in try block";
    throw new Error("Test error");
} catch (error) {
    let catchVariable = "I'm in catch block";
    console.log(error.message); // Output: Test error
    // console.log(tryVariable); // ReferenceError
} finally {
    let finallyVariable = "I'm in finally block";
    console.log("Finally executed");
    // console.log(catchVariable); // ReferenceError
}

// Switch statement block scope
let value = 1;
switch (value) {
    case 1: {
        let caseVariable = "Case 1 variable";
        console.log(caseVariable); // Output: Case 1 variable
        break;
    }
    case 2: {
        let caseVariable = "Case 2 variable"; // Different variable
        console.log(caseVariable);
        break;
    }
}
// console.log(caseVariable); // ReferenceError
```

## 🔗 Lexical Scope and Scope Chain

Lexical scope means that the scope is determined by where variables are declared in the code.

```javascript
// Lexical scope demonstration
let globalVar = "Global";

function outerFunction() {
    let outerVar = "Outer";
    
    function middleFunction() {
        let middleVar = "Middle";
        
        function innerFunction() {
            let innerVar = "Inner";
            
            // Can access all variables in the scope chain
            console.log(innerVar);  // Output: Inner
            console.log(middleVar); // Output: Middle
            console.log(outerVar);  // Output: Outer
            console.log(globalVar); // Output: Global
        }
        
        innerFunction();
        // console.log(innerVar); // ReferenceError
    }
    
    middleFunction();
    // console.log(middleVar); // ReferenceError
}

outerFunction();

// Scope chain resolution
let name = "Global Alice";

function outer() {
    let name = "Outer Bob";
    
    function inner() {
        let name = "Inner Charlie";
        console.log(name); // Output: Inner Charlie (closest scope)
    }
    
    inner();
    console.log(name); // Output: Outer Bob
}

outer();
console.log(name); // Output: Global Alice

// Variable shadowing
function demonstrateShadowing() {
    let message = "Outer message";
    
    if (true) {
        let message = "Inner message"; // Shadows outer variable
        console.log(message); // Output: Inner message
    }
    
    console.log(message); // Output: Outer message
}

demonstrateShadowing();

// Scope chain with function expressions
let scopeChainDemo = function() {
    let level1 = "Level 1";
    
    return function() {
        let level2 = "Level 2";
        
        return function() {
            let level3 = "Level 3";
            return `${level3} -> ${level2} -> ${level1}`;
        };
    };
};

let result = scopeChainDemo()()();
console.log(result); // Output: Level 3 -> Level 2 -> Level 1
```

## 🔐 Closures

A closure is created when a function has access to variables from an outer scope even after the outer function has finished executing.

### 🎯 Basic Closure Concepts

```javascript
// Basic closure example
function createGreeter(greeting) {
    // This variable is "closed over" by the returned function
    return function(name) {
        return `${greeting}, ${name}!`;
    };
}

let sayHello = createGreeter("Hello");
let sayHi = createGreeter("Hi");

console.log(sayHello("Alice")); // Output: Hello, Alice!
console.log(sayHi("Bob"));      // Output: Hi, Bob!

// The outer function has finished, but the inner function still has access to 'greeting'

// Counter closure
function createCounter() {
    let count = 0; // Private variable
    
    return {
        increment: function() {
            count++;
            return count;
        },
        decrement: function() {
            count--;
            return count;
        },
        getCount: function() {
            return count;
        }
    };
}

let counter1 = createCounter();
let counter2 = createCounter();

console.log(counter1.increment()); // Output: 1
console.log(counter1.increment()); // Output: 2
console.log(counter2.increment()); // Output: 1 (separate closure)
console.log(counter1.getCount());  // Output: 2

// Each counter has its own closure with its own 'count' variable

// Closure with parameters
function multiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

let double = multiplier(2);
let triple = multiplier(3);

console.log(double(5)); // Output: 10
console.log(triple(4)); // Output: 12

// Module pattern with closures
let calculator = (function() {
    let result = 0; // Private variable
    
    return {
        add: function(x) {
            result += x;
            return this;
        },
        subtract: function(x) {
            result -= x;
            return this;
        },
        multiply: function(x) {
            result *= x;
            return this;
        },
        divide: function(x) {
            if (x !== 0) {
                result /= x;
            }
            return this;
        },
        getResult: function() {
            return result;
        },
        reset: function() {
            result = 0;
            return this;
        }
    };
})();

let calcResult = calculator
    .add(10)
    .multiply(2)
    .subtract(5)
    .getResult();

console.log(calcResult); // Output: 15
```

### 🏭 Practical Closure Examples

```javascript
// Event handler with closures
function setupEventHandlers() {
    let clickCount = 0;
    
    return {
        onClick: function(event) {
            clickCount++;
            console.log(`Button clicked ${clickCount} times`);
        },
        
        getClickCount: function() {
            return clickCount;
        }
    };
}

let buttonHandler = setupEventHandlers();
// In browser: document.getElementById('button').addEventListener('click', buttonHandler.onClick);

// Configuration with closures
function createApiClient(baseUrl, apiKey) {
    return {
        get: function(endpoint) {
            return `GET ${baseUrl}${endpoint} with key: ${apiKey}`;
        },
        
        post: function(endpoint, data) {
            return `POST ${baseUrl}${endpoint} with data: ${JSON.stringify(data)} and key: ${apiKey}`;
        }
    };
}

let apiClient = createApiClient('https://api.example.com', 'secret123');
console.log(apiClient.get('/users')); // Output: GET https://api.example.com/users with key: secret123

// Memoization with closures
function memoize(fn) {
    let cache = {};
    
    return function(...args) {
        let key = JSON.stringify(args);
        
        if (key in cache) {
            console.log('Cache hit!');
            return cache[key];
        }
        
        console.log('Computing...');
        let result = fn.apply(this, args);
        cache[key] = result;
        return result;
    };
}

function expensiveFunction(n) {
    // Simulate expensive computation
    let result = 0;
    for (let i = 0; i < n * 1000000; i++) {
        result += i;
    }
    return result;
}

let memoizedFunction = memoize(expensiveFunction);

console.log(memoizedFunction(5)); // Computing... then result
console.log(memoizedFunction(5)); // Cache hit! then result

// Debounce function with closure
function debounce(func, delay) {
    let timeoutId;
    
    return function(...args) {
        clearTimeout(timeoutId);
        
        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

function searchFunction(query) {
    console.log(`Searching for: ${query}`);
}

let debouncedSearch = debounce(searchFunction, 300);

// Simulate rapid calls
debouncedSearch('a');
debouncedSearch('ap');
debouncedSearch('app'); // Only this will execute after 300ms

// Private methods with closures
function createBankAccount(initialBalance) {
    let balance = initialBalance;
    let transactionHistory = [];
    
    // Private method
    function addTransaction(type, amount) {
        transactionHistory.push({
            type: type,
            amount: amount,
            balance: balance,
            timestamp: new Date()
        });
    }
    
    return {
        deposit: function(amount) {
            if (amount > 0) {
                balance += amount;
                addTransaction('deposit', amount);
                return balance;
            }
            throw new Error('Deposit amount must be positive');
        },
        
        withdraw: function(amount) {
            if (amount > 0 && amount <= balance) {
                balance -= amount;
                addTransaction('withdrawal', amount);
                return balance;
            }
            throw new Error('Invalid withdrawal amount');
        },
        
        getBalance: function() {
            return balance;
        },
        
        getHistory: function() {
            return [...transactionHistory]; // Return copy to prevent modification
        }
    };
}

let account = createBankAccount(1000);
console.log(account.deposit(500));   // Output: 1500
console.log(account.withdraw(200));  // Output: 1300
console.log(account.getBalance());   // Output: 1300
console.log(account.getHistory());   // Transaction history
// console.log(account.balance);     // undefined (private)
```

### 🔄 Closure Patterns and Use Cases

```javascript
// Iterator pattern with closures
function createIterator(array) {
    let index = 0;
    
    return {
        next: function() {
            if (index < array.length) {
                return { value: array[index++], done: false };
            } else {
                return { done: true };
            }
        },
        
        reset: function() {
            index = 0;
        },
        
        hasNext: function() {
            return index < array.length;
        }
    };
}

let iterator = createIterator(['a', 'b', 'c']);
console.log(iterator.next()); // { value: 'a', done: false }
console.log(iterator.next()); // { value: 'b', done: false }
console.log(iterator.next()); // { value: 'c', done: false }
console.log(iterator.next()); // { done: true }

// State machine with closures
function createStateMachine(initialState, transitions) {
    let currentState = initialState;
    
    return {
        getCurrentState: function() {
            return currentState;
        },
        
        transition: function(action) {
            if (transitions[currentState] && transitions[currentState][action]) {
                currentState = transitions[currentState][action];
                return currentState;
            }
            throw new Error(`Invalid transition: ${action} from ${currentState}`);
        },
        
        canTransition: function(action) {
            return transitions[currentState] && transitions[currentState][action];
        }
    };
}

let doorStateMachine = createStateMachine('closed', {
    closed: { open: 'open' },
    open: { close: 'closed', lock: 'locked' },
    locked: { unlock: 'closed' }
});

console.log(doorStateMachine.getCurrentState()); // closed
console.log(doorStateMachine.transition('open')); // open
console.log(doorStateMachine.transition('close')); // closed

// Partial application with closures
function partial(func, ...presetArgs) {
    return function(...laterArgs) {
        return func(...presetArgs, ...laterArgs);
    };
}

function greet(greeting, name, punctuation) {
    return `${greeting}, ${name}${punctuation}`;
}

let sayHello = partial(greet, 'Hello');
let sayHelloExcited = partial(greet, 'Hello', undefined, '!');

console.log(sayHello('Alice', '.')); // Hello, Alice.
console.log(sayHelloExcited('Bob'));  // Hello, Bob!

// Curry function with closures
function curry(func) {
    return function curried(...args) {
        if (args.length >= func.length) {
            return func.apply(this, args);
        } else {
            return function(...nextArgs) {
                return curried(...args, ...nextArgs);
            };
        }
    };
}

function add(a, b, c) {
    return a + b + c;
}

let curriedAdd = curry(add);
console.log(curriedAdd(1)(2)(3)); // 6
console.log(curriedAdd(1, 2)(3)); // 6

// Observer pattern with closures
function createObservable() {
    let observers = [];
    let value = null;
    
    return {
        subscribe: function(callback) {
            observers.push(callback);
            
            // Return unsubscribe function
            return function unsubscribe() {
                let index = observers.indexOf(callback);
                if (index > -1) {
                    observers.splice(index, 1);
                }
            };
        },
        
        notify: function(newValue) {
            value = newValue;
            observers.forEach(callback => callback(newValue));
        },
        
        getValue: function() {
            return value;
        }
    };
}

let observable = createObservable();

let unsubscribe1 = observable.subscribe(value => {
    console.log(`Observer 1: ${value}`);
});

let unsubscribe2 = observable.subscribe(value => {
    console.log(`Observer 2: ${value}`);
});

observable.notify('Hello'); // Both observers called
unsubscribe1();
observable.notify('World'); // Only observer 2 called
```

## ⚠️ Memory Considerations and Common Pitfalls

### 🧠 Memory Leaks with Closures

```javascript
// Memory leak example - circular reference
function createLeakyFunction() {
    let largeData = new Array(1000000).fill('data');
    
    return function() {
        // This closure keeps largeData in memory even if not used
        console.log('Function called');
    };
}

// Better approach - clean up references
function createCleanFunction() {
    let largeData = new Array(1000000).fill('data');
    
    return function() {
        console.log('Function called');
        // largeData is not referenced, so it can be garbage collected
    };
}

// Avoiding closure memory leaks
function createEventHandler() {
    let element = document.getElementById('button');
    let data = new Array(1000000).fill('data');
    
    function clickHandler() {
        console.log('Button clicked');
        // Don't reference 'data' if not needed
    }
    
    element.addEventListener('click', clickHandler);
    
    // Return cleanup function
    return function cleanup() {
        element.removeEventListener('click', clickHandler);
        element = null; // Break circular reference
        data = null;    // Allow garbage collection
    };
}

// Common closure pitfalls
console.log("Closure pitfalls:");

// Pitfall 1: Loop closures with var
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(`var i: ${i}`); // Output: var i: 3 (three times)
    }, 100);
}

// Solution 1: Use let
for (let j = 0; j < 3; j++) {
    setTimeout(function() {
        console.log(`let j: ${j}`); // Output: let j: 0, let j: 1, let j: 2
    }, 200);
}

// Solution 2: IIFE
for (var k = 0; k < 3; k++) {
    (function(index) {
        setTimeout(function() {
            console.log(`IIFE k: ${index}`); // Output: IIFE k: 0, IIFE k: 1, IIFE k: 2
        }, 300);
    })(k);
}

// Pitfall 2: Unintended closure retention
function createHandlers() {
    let handlers = [];
    let largeObject = { data: new Array(1000000).fill('data') };
    
    for (let i = 0; i < 10; i++) {
        handlers.push(function() {
            console.log(`Handler ${i}`);
            // largeObject is retained in all closures even if not used
        });
    }
    
    return handlers;
}

// Better approach
function createHandlersBetter() {
    let handlers = [];
    
    for (let i = 0; i < 10; i++) {
        handlers.push(function() {
            console.log(`Handler ${i}`);
            // No unnecessary references to large objects
        });
    }
    
    return handlers;
}
```

### 🎯 Best Practices for Closures

```javascript
// ✅ Use closures for data privacy
function createSecureCounter() {
    let count = 0;
    
    return {
        increment: () => ++count,
        decrement: () => --count,
        getValue: () => count
        // count is not directly accessible
    };
}

// ✅ Clean up event listeners and references
function createComponent() {
    let element = document.createElement('div');
    let data = { /* some data */ };
    
    function handleClick() {
        console.log('Clicked');
    }
    
    element.addEventListener('click', handleClick);
    
    return {
        element: element,
        destroy: function() {
            element.removeEventListener('click', handleClick);
            element = null;
            data = null;
        }
    };
}

// ✅ Use WeakMap for private data when appropriate
let privateData = new WeakMap();

function createObjectWithPrivateData(initialValue) {
    let obj = {
        getValue: function() {
            return privateData.get(this);
        },
        
        setValue: function(value) {
            privateData.set(this, value);
        }
    };
    
    privateData.set(obj, initialValue);
    return obj;
}

let obj = createObjectWithPrivateData('secret');
console.log(obj.getValue()); // secret
// privateData is not accessible from outside

// ✅ Avoid unnecessary closures in loops
let functions = [];

// ❌ Creates unnecessary closures
for (let i = 0; i < 1000; i++) {
    functions.push(function() {
        return i * 2; // Each function closes over 'i'
    });
}

// ✅ Better approach for simple calculations
let betterFunctions = [];
for (let i = 0; i < 1000; i++) {
    betterFunctions.push(createMultiplier(i));
}

function createMultiplier(factor) {
    return function() {
        return factor * 2;
    };
}

// ✅ Use closures for configuration
function createApiClient(config) {
    const { baseUrl, apiKey, timeout = 5000 } = config;
    
    return {
        get: function(endpoint) {
            return fetch(`${baseUrl}${endpoint}`, {
                headers: { 'Authorization': `Bearer ${apiKey}` },
                timeout: timeout
            });
        },
        
        post: function(endpoint, data) {
            return fetch(`${baseUrl}${endpoint}`, {
                method: 'POST',
                headers: { 
                    'Authorization': `Bearer ${apiKey}`,
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data),
                timeout: timeout
            });
        }
    };
}

let api = createApiClient({
    baseUrl: 'https://api.example.com',
    apiKey: 'secret123'
});
```

## 🧪 Advanced Scope and Closure Patterns

### 🏭 Module Pattern

```javascript
// Revealing module pattern
let userModule = (function() {
    // Private variables and functions
    let users = [];
    let currentUser = null;
    
    function validateUser(user) {
        return user && user.name && user.email;
    }
    
    function generateId() {
        return Math.random().toString(36).substr(2, 9);
    }
    
    // Public API
    return {
        addUser: function(userData) {
            if (!validateUser(userData)) {
                throw new Error('Invalid user data');
            }
            
            let user = {
                id: generateId(),
                name: userData.name,
                email: userData.email,
                createdAt: new Date()
            };
            
            users.push(user);
            return user;
        },
        
        getUser: function(id) {
            return users.find(user => user.id === id);
        },
        
        getAllUsers: function() {
            return [...users]; // Return copy
        },
        
        setCurrentUser: function(id) {
            let user = this.getUser(id);
            if (user) {
                currentUser = user;
                return true;
            }
            return false;
        },
        
        getCurrentUser: function() {
            return currentUser;
        },
        
        getUserCount: function() {
            return users.length;
        }
    };
})();

// Usage
let user1 = userModule.addUser({ name: 'Alice', email: 'alice@example.com' });
let user2 = userModule.addUser({ name: 'Bob', email: 'bob@example.com' });

console.log(userModule.getUserCount()); // 2
console.log(userModule.getAllUsers());
userModule.setCurrentUser(user1.id);
console.log(userModule.getCurrentUser());

// Namespace pattern
let MyApp = MyApp || {};

MyApp.Utils = (function() {
    function formatDate(date) {
        return date.toLocaleDateString();
    }
    
    function formatCurrency(amount) {
        return `$${amount.toFixed(2)}`;
    }
    
    return {
        formatDate: formatDate,
        formatCurrency: formatCurrency
    };
})();

MyApp.UserManager = (function() {
    let users = [];
    
    return {
        add: function(user) {
            users.push(user);
        },
        
        getAll: function() {
            return users;
        }
    };
})();

// Usage
console.log(MyApp.Utils.formatDate(new Date()));
console.log(MyApp.Utils.formatCurrency(123.456));
```

### 🔄 Advanced Closure Techniques

```javascript
// Closure with multiple return functions
function createMathOperations(initialValue) {
    let value = initialValue;
    
    return {
        add: function(x) {
            value += x;
            return this;
        },
        
        subtract: function(x) {
            value -= x;
            return this;
        },
        
        multiply: function(x) {
            value *= x;
            return this;
        },
        
        divide: function(x) {
            if (x !== 0) {
                value /= x;
            }
            return this;
        },
        
        getValue: function() {
            return value;
        },
        
        reset: function() {
            value = initialValue;
            return this;
        }
    };
}

let math = createMathOperations(10);
let result = math.add(5).multiply(2).subtract(10).getValue();
console.log(result); // 20

// Closure factory with configuration
function createValidator(config) {
    let rules = config.rules || [];
    let messages = config.messages || {};
    
    return function validate(data) {
        let errors = [];
        
        rules.forEach(rule => {
            if (!rule.test(data)) {
                errors.push(messages[rule.name] || `Validation failed for ${rule.name}`);
            }
        });
        
        return {
            isValid: errors.length === 0,
            errors: errors
        };
    };
}

let userValidator = createValidator({
    rules: [
        { name: 'required', test: data => data && data.trim().length > 0 },
        { name: 'minLength', test: data => data && data.length >= 3 },
        { name: 'email', test: data => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(data) }
    ],
    messages: {
        required: 'This field is required',
        minLength: 'Minimum length is 3 characters',
        email: 'Invalid email format'
    }
});

console.log(userValidator('ab')); // { isValid: false, errors: [...] }
console.log(userValidator('test@example.com')); // { isValid: true, errors: [] }

// Closure with async operations
function createAsyncQueue() {
    let queue = [];
    let processing = false;
    
    async function processQueue() {
        if (processing || queue.length === 0) return;
        
        processing = true;
        
        while (queue.length > 0) {
            let { task, resolve, reject } = queue.shift();
            
            try {
                let result = await task();
                resolve(result);
            } catch (error) {
                reject(error);
            }
        }
        
        processing = false;
    }
    
    return {
        add: function(task) {
            return new Promise((resolve, reject) => {
                queue.push({ task, resolve, reject });
                processQueue();
            });
        },
        
        getQueueLength: function() {
            return queue.length;
        },
        
        isProcessing: function() {
            return processing;
        }
    };
}

let asyncQueue = createAsyncQueue();

// Usage
asyncQueue.add(() => new Promise(resolve => setTimeout(() => resolve('Task 1'), 1000)))
    .then(result => console.log(result));

asyncQueue.add(() => new Promise(resolve => setTimeout(() => resolve('Task 2'), 500)))
    .then(result => console.log(result));
```

## 💡 Best Practices

### ✅ Scope and Closure Best Practices

```javascript
// ✅ Use const and let instead of var
const API_URL = 'https://api.example.com';
let userCount = 0;

// ✅ Minimize global scope pollution
(function() {
    // Your code here
})();

// ✅ Use closures for data privacy
function createSecureObject(initialData) {
    let data = { ...initialData };
    
    return {
        get: (key) => data[key],
        set: (key, value) => { data[key] = value; },
        has: (key) => key in data
    };
}

// ✅ Clean up closures to prevent memory leaks
function createComponent() {
    let element = document.createElement('div');
    
    function handleClick() {
        console.log('Clicked');
    }
    
    element.addEventListener('click', handleClick);
    
    return {
        element,
        destroy() {
            element.removeEventListener('click', handleClick);
            element = null;
        }
    };
}

// ✅ Use block scope appropriately
if (condition) {
    let temporaryVariable = 'only needed here';
    // Use temporaryVariable
}
// temporaryVariable is not accessible here

// ✅ Prefer function declarations for hoisting when needed
function hoistedFunction() {
    return 'I can be called before declaration';
}

// ✅ Use arrow functions for lexical this binding
class EventHandler {
    constructor() {
        this.count = 0;
        
        // Arrow function preserves 'this'
        this.handleClick = () => {
            this.count++;
            console.log(`Clicked ${this.count} times`);
        };
    }
}
```

### ⚠️ Common Scope and Closure Pitfalls

```javascript
// ❌ Accidental global variables
function badFunction() {
    accidentalGlobal = 'Oops!'; // Missing var/let/const
}

// ✅ Always declare variables
function goodFunction() {
    let intentionalLocal = 'Good!';
}

// ❌ Closure memory leaks
function createLeakyHandler() {
    let largeData = new Array(1000000).fill('data');
    
    return function() {
        console.log('Handler called');
        // largeData is retained even if not used
    };
}

// ✅ Avoid unnecessary references
function createCleanHandler() {
    return function() {
        console.log('Handler called');
        // No unnecessary references
    };
}

// ❌ Incorrect loop closures
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100); // Logs 3 three times
}

// ✅ Use let or IIFE
for (let j = 0; j < 3; j++) {
    setTimeout(() => console.log(j), 200); // Logs 0, 1, 2
}

// ❌ Overusing closures
function unnecessaryClosure(x) {
    return function() {
        return x * 2; // Simple calculation doesn't need closure
    };
}

// ✅ Use closures when you need state or privacy
function necessaryClosure() {
    let state = 0;
    
    return function() {
        return ++state; // Closure needed for state
    };
}
```

---

**Next Chapter**: [🌐 Document Object Model (DOM)](14_Document_Object_Model_DOM.md)