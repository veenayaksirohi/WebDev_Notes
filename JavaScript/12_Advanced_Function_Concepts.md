# 🏹 Advanced Function Concepts

## 🎯 Higher-Order Functions

Higher-order functions are functions that either take other functions as arguments or return functions as results. They enable powerful functional programming patterns and code reuse.

### 📥 Functions as Arguments

```javascript
// Basic callback function
function processData(data, callback) {
    const processed = data.map(item => item * 2);
    callback(processed);
}

function displayResults(results) {
    console.log("Results:", results);
}

processData([1, 2, 3, 4], displayResults); // Output: Results: [2, 4, 6, 8]

// Custom filter function
function customFilter(array, predicate) {
    const result = [];
    for (let item of array) {
        if (predicate(item)) {
            result.push(item);
        }
    }
    return result;
}

let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumbers = customFilter(numbers, n => n % 2 === 0);
console.log(evenNumbers); // [2, 4, 6, 8, 10]
```

### 📤 Functions as Return Values

```javascript
// Basic function factory
function createMultiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5));    // 10
console.log(triple(4));    // 12

// Closure with private state
function createCounter(initialValue = 0, step = 1) {
    let count = initialValue;
    
    return {
        increment: () => count += step,
        decrement: () => count -= step,
        getValue: () => count,
        reset: () => { count = initialValue; return count; }
    };
}

const counter1 = createCounter(0, 1);
console.log(counter1.increment()); // 1
console.log(counter1.increment()); // 2
```

## 🔄 Function Composition

```javascript
// Basic composition
function compose(f, g) {
    return function(x) {
        return f(g(x));
    };
}

const addOne = x => x + 1;
const multiplyByTwo = x => x * 2;

const addOneThenDouble = compose(multiplyByTwo, addOne);
console.log(addOneThenDouble(3)); // (3 + 1) * 2 = 8

// Pipe (left-to-right composition)
function pipe(...functions) {
    return function(value) {
        return functions.reduce((acc, fn) => fn(acc), value);
    };
}

const square = x => x * x;
const subtract5 = x => x - 5;

const piped = pipe(square, addOne, multiplyByTwo, subtract5);
console.log(piped(3)); // ((3² + 1) * 2) - 5 = 15
```

## 🍛 Currying and Partial Application

### 🍛 Currying

```javascript
// Manual currying
function curriedAdd(a) {
    return function(b) {
        return function(c) {
            return a + b + c;
        };
    };
}

console.log(curriedAdd(1)(2)(3)); // 6

// Generic curry function
function curry(func) {
    return function curried(...args) {
        if (args.length >= func.length) {
            return func.apply(this, args);
        } else {
            return function(...nextArgs) {
                return curried.apply(this, args.concat(nextArgs));
            };
        }
    };
}

function add(a, b, c) {
    return a + b + c;
}

const curriedAddGeneric = curry(add);
console.log(curriedAddGeneric(1)(2)(3)); // 6
console.log(curriedAddGeneric(1, 2)(3)); // 6
```

### 🔧 Partial Application

```javascript
// Basic partial application
function partial(func, ...presetArgs) {
    return function(...laterArgs) {
        return func(...presetArgs, ...laterArgs);
    };
}

function greet(greeting, name, punctuation) {
    return `${greeting}, ${name}${punctuation}`;
}

const sayHello = partial(greet, 'Hello');
console.log(sayHello('Alice', '!')); // Hello, Alice!
```

## 🎭 Decorators and Function Wrappers

```javascript
// Basic decorator pattern
function withLogging(func) {
    return function(...args) {
        console.log(`Calling ${func.name} with arguments:`, args);
        const result = func.apply(this, args);
        console.log(`${func.name} returned:`, result);
        return result;
    };
}

function add(a, b) {
    return a + b;
}

const loggedAdd = withLogging(add);
console.log(loggedAdd(3, 4));
// Output:
// Calling add with arguments: [3, 4]
// add returned: 7
// 7

// Timing decorator
function withTiming(func) {
    return function(...args) {
        const start = performance.now();
        const result = func.apply(this, args);
        const end = performance.now();
        console.log(`${func.name} took ${(end - start).toFixed(2)}ms`);
        return result;
    };
}

// Cache decorator
function withCache(func, ttl = 60000) {
    const cache = new Map();
    
    return function(...args) {
        const key = JSON.stringify(args);
        const cached = cache.get(key);
        
        if (cached && Date.now() - cached.timestamp < ttl) {
            console.log('Cache hit');
            return cached.value;
        }
        
        console.log('Cache miss');
        const result = func.apply(this, args);
        cache.set(key, { value: result, timestamp: Date.now() });
        return result;
    };
}
```

## 🔄 Recursion Patterns

```javascript
// Basic recursion: Factorial
function factorial(n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

console.log(factorial(5)); // 120

// Optimized fibonacci with memoization
function fibonacciMemo(n, memo = {}) {
    if (n in memo) return memo[n];
    if (n < 2) return n;
    
    memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
    return memo[n];
}

console.log(fibonacciMemo(50)); // Much faster for large numbers

// Tree traversal
function traverseTree(node, callback) {
    callback(node.value);
    
    for (let child of node.children) {
        traverseTree(child, callback);
    }
}

// Tail recursion optimization
function factorialTail(n, accumulator = 1) {
    if (n <= 1) return accumulator;
    return factorialTail(n - 1, n * accumulator);
}

console.log(factorialTail(5)); // 120
```

## 💡 Best Practices

### ✅ Advanced Function Best Practices

```javascript
// ✅ Use pure functions when possible
const calculateTax = (amount, rate) => amount * rate;

// ✅ Prefer function composition over complex nested calls
const processUser = pipe(
    validateUser,
    normalizeUserData,
    enrichUserData,
    saveUser
);

// ✅ Use currying for reusable, configurable functions
const createValidator = (rules) => (data) => {
    return rules.every(rule => rule(data));
};

// ✅ Handle errors gracefully in higher-order functions
function safeMap(array, transform) {
    return array.map(item => {
        try {
            return transform(item);
        } catch (error) {
            console.error(`Error transforming item ${item}:`, error);
            return null;
        }
    }).filter(item => item !== null);
}
```

---

**Next Chapter**: [🔒 Scope and Closures](13_Scope_and_Closures.md)