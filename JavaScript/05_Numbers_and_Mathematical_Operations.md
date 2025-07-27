# 🔢 Numbers and Mathematical Operations

## 📊 Number System in JavaScript

JavaScript uses the **IEEE 754 double-precision floating-point** format to represent all numbers. This means there's only one number type that handles both integers and decimals.

### 🎯 Number Creation and Types

```javascript
// Integer numbers
let age = 25;
let temperature = -10;
let zero = 0;

// Floating-point numbers
let price = 99.99;
let pi = 3.14159;
let scientific = 1.23e-4;  // 0.000123

// Different number bases
let binary = 0b1010;      // Binary (base 2) = 10 in decimal
let octal = 0o755;        // Octal (base 8) = 493 in decimal
let hexadecimal = 0xFF;   // Hexadecimal (base 16) = 255 in decimal

console.log(binary);      // Output: 10
console.log(octal);       // Output: 493
console.log(hexadecimal); // Output: 255

// Large numbers with underscores (ES2021)
let million = 1_000_000;
let billion = 1_000_000_000;
console.log(million);     // Output: 1000000

// Number constructor
let num1 = Number(42);
let num2 = Number("123");
let num3 = Number(true);   // 1
let num4 = Number(false);  // 0

console.log(num1, num2, num3, num4); // Output: 42 123 1 0
```

### ⚠️ Special Numeric Values

```javascript
// Infinity and -Infinity
console.log(1 / 0);        // Output: Infinity
console.log(-1 / 0);       // Output: -Infinity
console.log(Infinity + 1); // Output: Infinity
console.log(Infinity - Infinity); // Output: NaN

// NaN (Not a Number)
console.log(0 / 0);        // Output: NaN
console.log("hello" * 2);  // Output: NaN
console.log(Math.sqrt(-1)); // Output: NaN

// Checking for special values
console.log(Number.isFinite(42));        // Output: true
console.log(Number.isFinite(Infinity));  // Output: false
console.log(Number.isNaN(NaN));          // Output: true
console.log(Number.isNaN("hello"));      // Output: false (not converted)

// Global vs Number methods
console.log(isNaN("hello"));             // Output: true (converts to NaN)
console.log(Number.isNaN("hello"));      // Output: false (strict check)
```

### 🔍 Number Properties and Constants

```javascript
// Number properties
console.log(Number.MAX_VALUE);           // Largest representable number
console.log(Number.MIN_VALUE);           // Smallest positive number
console.log(Number.MAX_SAFE_INTEGER);    // 9007199254740991
console.log(Number.MIN_SAFE_INTEGER);    // -9007199254740991
console.log(Number.POSITIVE_INFINITY);   // Infinity
console.log(Number.NEGATIVE_INFINITY);   // -Infinity
console.log(Number.NaN);                 // NaN

// Safe integer checking
console.log(Number.isSafeInteger(9007199254740991));  // Output: true
console.log(Number.isSafeInteger(9007199254740992));  // Output: false

// Epsilon (smallest difference between 1 and next representable number)
console.log(Number.EPSILON);             // Output: 2.220446049250313e-16

// Practical use of epsilon for floating-point comparison
function isEqual(a, b) {
    return Math.abs(a - b) < Number.EPSILON;
}

console.log(0.1 + 0.2 === 0.3);         // Output: false (floating-point precision)
console.log(isEqual(0.1 + 0.2, 0.3));   // Output: true
```

## 🧮 Number Methods and Formatting

### 🎯 Number Conversion Methods

```javascript
let num = 123.456789;

// toString() - convert to string
console.log(num.toString());      // Output: "123.456789"
console.log(num.toString(2));     // Output: "1111011.0111010..." (binary)
console.log(num.toString(16));    // Output: "7b.74bc6a7ef9db" (hexadecimal)

// toFixed() - fixed decimal places
console.log(num.toFixed(2));      // Output: "123.46"
console.log(num.toFixed(0));      // Output: "123"
console.log((1.005).toFixed(2));  // Output: "1.00" (rounding quirk)

// toPrecision() - significant digits
console.log(num.toPrecision(4));  // Output: "123.5"
console.log(num.toPrecision(2));  // Output: "1.2e+2"

// toExponential() - scientific notation
console.log(num.toExponential());    // Output: "1.23456789e+2"
console.log(num.toExponential(2));   // Output: "1.23e+2"

// valueOf() - primitive value
let numObj = new Number(42);
console.log(numObj.valueOf());    // Output: 42
console.log(typeof numObj);       // Output: "object"
console.log(typeof numObj.valueOf()); // Output: "number"
```

### 🌍 Locale-Aware Number Formatting

```javascript
let number = 1234567.89;

// Basic locale formatting
console.log(number.toLocaleString());           // Output: "1,234,567.89" (US)
console.log(number.toLocaleString('de-DE'));    // Output: "1.234.567,89" (German)
console.log(number.toLocaleString('fr-FR'));    // Output: "1 234 567,89" (French)

// Currency formatting
let price = 1234.56;
console.log(price.toLocaleString('en-US', {
    style: 'currency',
    currency: 'USD'
})); // Output: "$1,234.56"

console.log(price.toLocaleString('de-DE', {
    style: 'currency',
    currency: 'EUR'
})); // Output: "1.234,56 €"

console.log(price.toLocaleString('ja-JP', {
    style: 'currency',
    currency: 'JPY'
})); // Output: "￥1,235"

// Percentage formatting
let percentage = 0.1234;
console.log(percentage.toLocaleString('en-US', {
    style: 'percent'
})); // Output: "12.34%"

// Custom formatting options
let bigNumber = 1234567890;
console.log(bigNumber.toLocaleString('en-US', {
    minimumFractionDigits: 2,
    maximumFractionDigits: 2,
    useGrouping: true
})); // Output: "1,234,567,890.00"
```

## 🔄 Number Parsing and Conversion

### 📥 Parsing Strings to Numbers

```javascript
// parseInt() - parse integer
console.log(parseInt("123"));        // Output: 123
console.log(parseInt("123.45"));     // Output: 123
console.log(parseInt("123abc"));     // Output: 123
console.log(parseInt("abc123"));     // Output: NaN
console.log(parseInt(""));           // Output: NaN

// parseInt with radix (base)
console.log(parseInt("1010", 2));    // Output: 10 (binary)
console.log(parseInt("FF", 16));     // Output: 255 (hexadecimal)
console.log(parseInt("77", 8));      // Output: 63 (octal)

// parseFloat() - parse floating-point
console.log(parseFloat("123.45"));   // Output: 123.45
console.log(parseFloat("123.45abc")); // Output: 123.45
console.log(parseFloat("abc123.45")); // Output: NaN

// Number() constructor - strict conversion
console.log(Number("123"));          // Output: 123
console.log(Number("123.45"));       // Output: 123.45
console.log(Number("123abc"));       // Output: NaN
console.log(Number(""));             // Output: 0
console.log(Number(" 123 "));        // Output: 123

// Unary plus operator - quick conversion
console.log(+"123");                 // Output: 123
console.log(+"123.45");              // Output: 123.45
console.log(+"123abc");              // Output: NaN

// Practical parsing function
function safeParseNumber(str, defaultValue = 0) {
    const parsed = Number(str);
    return Number.isNaN(parsed) ? defaultValue : parsed;
}

console.log(safeParseNumber("123"));     // Output: 123
console.log(safeParseNumber("abc"));     // Output: 0
console.log(safeParseNumber("abc", -1)); // Output: -1
```

### 🔄 Type Coercion Examples

```javascript
// Implicit conversion in operations
console.log("5" + 3);        // Output: "53" (string concatenation)
console.log("5" - 3);        // Output: 2 (numeric subtraction)
console.log("5" * 3);        // Output: 15 (numeric multiplication)
console.log("5" / 3);        // Output: 1.6666666666666667

// Boolean to number conversion
console.log(true + 1);       // Output: 2
console.log(false + 1);      // Output: 1
console.log(Number(true));   // Output: 1
console.log(Number(false));  // Output: 0

// Array to number conversion
console.log(Number([]));     // Output: 0
console.log(Number([5]));    // Output: 5
console.log(Number([1,2]));  // Output: NaN

// Object to number conversion
console.log(Number({}));     // Output: NaN
console.log(Number(null));   // Output: 0
console.log(Number(undefined)); // Output: NaN
```

## 📐 Math Object and Mathematical Functions

The `Math` object provides mathematical constants and functions.

### 🔢 Mathematical Constants

```javascript
// Important mathematical constants
console.log(Math.PI);        // Output: 3.141592653589793
console.log(Math.E);         // Output: 2.718281828459045 (Euler's number)
console.log(Math.LN2);       // Output: 0.6931471805599453 (ln(2))
console.log(Math.LN10);      // Output: 2.302585092994046 (ln(10))
console.log(Math.LOG2E);     // Output: 1.4426950408889634 (log₂(e))
console.log(Math.LOG10E);    // Output: 0.4342944819032518 (log₁₀(e))
console.log(Math.SQRT1_2);   // Output: 0.7071067811865476 (√(1/2))
console.log(Math.SQRT2);     // Output: 1.4142135623730951 (√2)

// Using constants in calculations
function circleArea(radius) {
    return Math.PI * radius * radius;
}

function circleCircumference(radius) {
    return 2 * Math.PI * radius;
}

console.log(circleArea(5));           // Output: 78.53981633974483
console.log(circleCircumference(5));  // Output: 31.41592653589793
```

### 🧮 Basic Mathematical Methods

```javascript
// Rounding methods
console.log(Math.round(4.7));    // Output: 5 (round to nearest integer)
console.log(Math.round(4.4));    // Output: 4
console.log(Math.round(-4.5));   // Output: -4 (rounds toward positive infinity)

console.log(Math.floor(4.7));    // Output: 4 (round down)
console.log(Math.floor(-4.7));   // Output: -5

console.log(Math.ceil(4.1));     // Output: 5 (round up)
console.log(Math.ceil(-4.7));    // Output: -4

console.log(Math.trunc(4.7));    // Output: 4 (remove decimal part)
console.log(Math.trunc(-4.7));   // Output: -4

// Absolute value and sign
console.log(Math.abs(-5));       // Output: 5
console.log(Math.abs(5));        // Output: 5
console.log(Math.sign(-5));      // Output: -1
console.log(Math.sign(5));       // Output: 1
console.log(Math.sign(0));       // Output: 0

// Min and max
console.log(Math.min(1, 3, 2));     // Output: 1
console.log(Math.max(1, 3, 2));     // Output: 3
console.log(Math.min());             // Output: Infinity
console.log(Math.max());             // Output: -Infinity

// With arrays
let numbers = [1, 5, 3, 9, 2];
console.log(Math.min(...numbers));  // Output: 1
console.log(Math.max(...numbers));  // Output: 9

// Power and square root
console.log(Math.pow(2, 3));     // Output: 8 (2³)
console.log(2 ** 3);             // Output: 8 (ES2016 exponentiation operator)
console.log(Math.sqrt(16));      // Output: 4
console.log(Math.cbrt(27));      // Output: 3 (cube root)

// Logarithms
console.log(Math.log(Math.E));   // Output: 1 (natural logarithm)
console.log(Math.log10(100));    // Output: 2 (base-10 logarithm)
console.log(Math.log2(8));       // Output: 3 (base-2 logarithm)
```

### 📊 Trigonometric Functions

```javascript
// Basic trigonometric functions (angles in radians)
console.log(Math.sin(Math.PI / 2));  // Output: 1
console.log(Math.cos(0));            // Output: 1
console.log(Math.tan(Math.PI / 4));  // Output: 0.9999999999999999 (≈ 1)

// Convert degrees to radians
function degreesToRadians(degrees) {
    return degrees * (Math.PI / 180);
}

function radiansToDegrees(radians) {
    return radians * (180 / Math.PI);
}

console.log(Math.sin(degreesToRadians(90)));  // Output: 1
console.log(radiansToDegrees(Math.PI));       // Output: 180

// Inverse trigonometric functions
console.log(Math.asin(1));           // Output: 1.5707963267948966 (π/2)
console.log(Math.acos(1));           // Output: 0
console.log(Math.atan(1));           // Output: 0.7853981633974483 (π/4)
console.log(Math.atan2(1, 1));       // Output: 0.7853981633974483 (π/4)

// Hyperbolic functions (ES6)
console.log(Math.sinh(0));           // Output: 0
console.log(Math.cosh(0));           // Output: 1
console.log(Math.tanh(0));           // Output: 0
```

### 🎲 Random Number Generation

```javascript
// Basic random number (0 to 1, exclusive of 1)
console.log(Math.random());          // Output: 0.123456789... (random)

// Random integer between min and max (inclusive)
function randomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

console.log(randomInt(1, 6));        // Output: 1-6 (dice roll)
console.log(randomInt(10, 20));      // Output: 10-20

// Random float between min and max
function randomFloat(min, max) {
    return Math.random() * (max - min) + min;
}

console.log(randomFloat(1.5, 2.5));  // Output: 1.5-2.5

// Random array element
function randomChoice(array) {
    return array[Math.floor(Math.random() * array.length)];
}

let colors = ['red', 'green', 'blue', 'yellow'];
console.log(randomChoice(colors));   // Output: random color

// Shuffle array (Fisher-Yates algorithm)
function shuffleArray(array) {
    const shuffled = [...array];
    for (let i = shuffled.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
    }
    return shuffled;
}

let numbers = [1, 2, 3, 4, 5];
console.log(shuffleArray(numbers));  // Output: shuffled array

// Random string generator
function generateRandomString(length, chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789') {
    let result = '';
    for (let i = 0; i < length; i++) {
        result += chars.charAt(Math.floor(Math.random() * chars.length));
    }
    return result;
}

console.log(generateRandomString(8));  // Output: random 8-character string
```

## ⚠️ Floating-Point Precision Issues

### 🔍 Understanding Precision Problems

```javascript
// Classic floating-point precision issues
console.log(0.1 + 0.2);              // Output: 0.30000000000000004
console.log(0.1 + 0.2 === 0.3);      // Output: false

console.log(0.1 * 3);                // Output: 0.30000000000000004
console.log(0.3 / 3);                // Output: 0.09999999999999999

// Large number precision loss
console.log(9007199254740992 + 1);    // Output: 9007199254740992 (no change!)
console.log(9007199254740993 + 1);    // Output: 9007199254740994 (skips 9007199254740995)

// Demonstration of precision limits
let largeNum = Number.MAX_SAFE_INTEGER;
console.log(largeNum);                // Output: 9007199254740991
console.log(largeNum + 1);            // Output: 9007199254740992
console.log(largeNum + 2);            // Output: 9007199254740993
console.log(largeNum + 3);            // Output: 9007199254740994 (skips one)
```

### 🛠️ Solutions for Precision Issues

```javascript
// Solution 1: Use epsilon for comparison
function isEqual(a, b, epsilon = Number.EPSILON) {
    return Math.abs(a - b) < epsilon;
}

console.log(isEqual(0.1 + 0.2, 0.3));  // Output: true

// Solution 2: Round to specific decimal places
function roundToPrecision(num, precision) {
    const factor = Math.pow(10, precision);
    return Math.round(num * factor) / factor;
}

console.log(roundToPrecision(0.1 + 0.2, 10));  // Output: 0.3

// Solution 3: Use integer arithmetic for currency
class Money {
    constructor(amount, currency = 'USD') {
        this.cents = Math.round(amount * 100);  // Store as cents
        this.currency = currency;
    }
    
    add(other) {
        return new Money((this.cents + other.cents) / 100, this.currency);
    }
    
    subtract(other) {
        return new Money((this.cents - other.cents) / 100, this.currency);
    }
    
    multiply(factor) {
        return new Money((this.cents * factor) / 100, this.currency);
    }
    
    divide(divisor) {
        return new Money((this.cents / divisor) / 100, this.currency);
    }
    
    toString() {
        return `${this.currency} ${(this.cents / 100).toFixed(2)}`;
    }
    
    valueOf() {
        return this.cents / 100;
    }
}

let price1 = new Money(0.1);
let price2 = new Money(0.2);
let total = price1.add(price2);
console.log(total.toString());        // Output: USD 0.30
console.log(total.valueOf() === 0.3); // Output: true

// Solution 4: Use BigInt for large integers
let bigInt1 = BigInt(Number.MAX_SAFE_INTEGER);
let bigInt2 = bigInt1 + 1n;
let bigInt3 = bigInt1 + 2n;
console.log(bigInt1.toString());      // Output: "9007199254740991"
console.log(bigInt2.toString());      // Output: "9007199254740992"
console.log(bigInt3.toString());      // Output: "9007199254740993"
```

## 🧪 Practical Mathematical Applications

### 📊 Statistical Functions

```javascript
class Statistics {
    static mean(numbers) {
        return numbers.reduce((sum, num) => sum + num, 0) / numbers.length;
    }
    
    static median(numbers) {
        const sorted = [...numbers].sort((a, b) => a - b);
        const mid = Math.floor(sorted.length / 2);
        return sorted.length % 2 === 0 
            ? (sorted[mid - 1] + sorted[mid]) / 2 
            : sorted[mid];
    }
    
    static mode(numbers) {
        const frequency = {};
        numbers.forEach(num => frequency[num] = (frequency[num] || 0) + 1);
        
        let maxFreq = 0;
        let modes = [];
        
        for (let num in frequency) {
            if (frequency[num] > maxFreq) {
                maxFreq = frequency[num];
                modes = [Number(num)];
            } else if (frequency[num] === maxFreq) {
                modes.push(Number(num));
            }
        }
        
        return modes.length === numbers.length ? [] : modes;
    }
    
    static standardDeviation(numbers) {
        const mean = this.mean(numbers);
        const squaredDiffs = numbers.map(num => Math.pow(num - mean, 2));
        const avgSquaredDiff = this.mean(squaredDiffs);
        return Math.sqrt(avgSquaredDiff);
    }
    
    static range(numbers) {
        return Math.max(...numbers) - Math.min(...numbers);
    }
    
    static percentile(numbers, p) {
        const sorted = [...numbers].sort((a, b) => a - b);
        const index = (p / 100) * (sorted.length - 1);
        
        if (Number.isInteger(index)) {
            return sorted[index];
        } else {
            const lower = Math.floor(index);
            const upper = Math.ceil(index);
            const weight = index - lower;
            return sorted[lower] * (1 - weight) + sorted[upper] * weight;
        }
    }
}

// Usage example
let testScores = [85, 92, 78, 96, 88, 91, 87, 93, 89, 84];

console.log("Test Scores Analysis:");
console.log("Mean:", Statistics.mean(testScores).toFixed(2));
console.log("Median:", Statistics.median(testScores));
console.log("Mode:", Statistics.mode(testScores));
console.log("Standard Deviation:", Statistics.standardDeviation(testScores).toFixed(2));
console.log("Range:", Statistics.range(testScores));
console.log("75th Percentile:", Statistics.percentile(testScores, 75));
```

### 🎯 Geometric Calculations

```javascript
class Geometry {
    // Circle calculations
    static circleArea(radius) {
        return Math.PI * radius * radius;
    }
    
    static circleCircumference(radius) {
        return 2 * Math.PI * radius;
    }
    
    // Rectangle calculations
    static rectangleArea(width, height) {
        return width * height;
    }
    
    static rectanglePerimeter(width, height) {
        return 2 * (width + height);
    }
    
    // Triangle calculations
    static triangleArea(base, height) {
        return 0.5 * base * height;
    }
    
    static triangleAreaHeron(a, b, c) {
        const s = (a + b + c) / 2;  // Semi-perimeter
        return Math.sqrt(s * (s - a) * (s - b) * (s - c));
    }
    
    // Distance between two points
    static distance(x1, y1, x2, y2) {
        return Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
    }
    
    // Angle between two vectors
    static angleBetweenVectors(v1x, v1y, v2x, v2y) {
        const dot = v1x * v2x + v1y * v2y;
        const mag1 = Math.sqrt(v1x * v1x + v1y * v1y);
        const mag2 = Math.sqrt(v2x * v2x + v2y * v2y);
        return Math.acos(dot / (mag1 * mag2));
    }
    
    // Convert angle from radians to degrees
    static radToDeg(radians) {
        return radians * (180 / Math.PI);
    }
    
    // Convert angle from degrees to radians
    static degToRad(degrees) {
        return degrees * (Math.PI / 180);
    }
}

// Usage examples
console.log("Circle with radius 5:");
console.log("Area:", Geometry.circleArea(5).toFixed(2));
console.log("Circumference:", Geometry.circleCircumference(5).toFixed(2));

console.log("\nDistance between (0,0) and (3,4):");
console.log("Distance:", Geometry.distance(0, 0, 3, 4));

console.log("\nTriangle with sides 3, 4, 5:");
console.log("Area (Heron's formula):", Geometry.triangleAreaHeron(3, 4, 5));
```

### 💰 Financial Calculations

```javascript
class FinancialMath {
    // Simple interest
    static simpleInterest(principal, rate, time) {
        return principal * rate * time;
    }
    
    // Compound interest
    static compoundInterest(principal, rate, compoundingFrequency, time) {
        return principal * Math.pow(1 + rate / compoundingFrequency, compoundingFrequency * time);
    }
    
    // Monthly payment for a loan
    static monthlyPayment(principal, annualRate, years) {
        const monthlyRate = annualRate / 12;
        const numPayments = years * 12;
        
        if (monthlyRate === 0) return principal / numPayments;
        
        return principal * (monthlyRate * Math.pow(1 + monthlyRate, numPayments)) / 
               (Math.pow(1 + monthlyRate, numPayments) - 1);
    }
    
    // Future value of annuity
    static futureValueAnnuity(payment, rate, periods) {
        if (rate === 0) return payment * periods;
        return payment * ((Math.pow(1 + rate, periods) - 1) / rate);
    }
    
    // Present value of annuity
    static presentValueAnnuity(payment, rate, periods) {
        if (rate === 0) return payment * periods;
        return payment * ((1 - Math.pow(1 + rate, -periods)) / rate);
    }
    
    // Return on investment percentage
    static roi(initialValue, finalValue) {
        return ((finalValue - initialValue) / initialValue) * 100;
    }
}

// Usage examples
console.log("Financial Calculations:");

// Loan calculation
let loanAmount = 200000;
let annualRate = 0.045;  // 4.5%
let loanYears = 30;
let monthlyPayment = FinancialMath.monthlyPayment(loanAmount, annualRate, loanYears);
console.log(`Monthly payment for $${loanAmount} loan: $${monthlyPayment.toFixed(2)}`);

// Investment calculation
let investment = 10000;
let investmentRate = 0.07;  // 7%
let years = 10;
let futureValue = FinancialMath.compoundInterest(investment, investmentRate, 1, years);
console.log(`$${investment} invested at ${investmentRate * 100}% for ${years} years: $${futureValue.toFixed(2)}`);

// ROI calculation
let initialInvestment = 5000;
let currentValue = 7500;
let roi = FinancialMath.roi(initialInvestment, currentValue);
console.log(`ROI: ${roi.toFixed(2)}%`);
```

## 💡 Best Practices

### ✅ Number Handling Best Practices

```javascript
// ✅ Always validate numeric input
function safeAdd(a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
        throw new Error('Both arguments must be numbers');
    }
    if (!Number.isFinite(a) || !Number.isFinite(b)) {
        throw new Error('Arguments must be finite numbers');
    }
    return a + b;
}

// ✅ Use appropriate precision for comparisons
function compareFloats(a, b, precision = 10) {
    return Math.abs(a - b) < Math.pow(10, -precision);
}

// ✅ Handle edge cases in calculations
function safeDivide(dividend, divisor) {
    if (divisor === 0) {
        throw new Error('Division by zero');
    }
    return dividend / divisor;
}

// ✅ Use BigInt for large integer calculations
function factorial(n) {
    if (n < 0) throw new Error('Factorial of negative number');
    if (n === 0 || n === 1) return 1n;
    
    let result = 1n;
    for (let i = 2n; i <= BigInt(n); i++) {
        result *= i;
    }
    return result;
}

console.log(factorial(20).toString()); // Works with large numbers

// ✅ Format numbers appropriately for display
function formatNumber(num, options = {}) {
    const {
        decimals = 2,
        locale = 'en-US',
        style = 'decimal',
        currency = 'USD'
    } = options;
    
    return num.toLocaleString(locale, {
        style,
        currency: style === 'currency' ? currency : undefined,
        minimumFractionDigits: decimals,
        maximumFractionDigits: decimals
    });
}

console.log(formatNumber(1234.567));                    // "1,234.57"
console.log(formatNumber(1234.567, { style: 'currency' })); // "$1,234.57"
```

### ⚠️ Common Pitfalls to Avoid

```javascript
// ❌ Don't rely on floating-point equality
if (0.1 + 0.2 === 0.3) { /* This will never execute */ }

// ✅ Use epsilon comparison instead
if (Math.abs((0.1 + 0.2) - 0.3) < Number.EPSILON) { /* This works */ }

// ❌ Don't assume parseInt without radix
console.log(parseInt("08"));     // Could be 8 or 0 depending on environment
// ✅ Always specify radix
console.log(parseInt("08", 10)); // Always 8

// ❌ Don't ignore NaN in calculations
function average(numbers) {
    return numbers.reduce((sum, num) => sum + num, 0) / numbers.length;
}
// ✅ Validate input and handle NaN
function safeAverage(numbers) {
    if (!Array.isArray(numbers) || numbers.length === 0) return 0;
    const validNumbers = numbers.filter(num => typeof num === 'number' && !Number.isNaN(num));
    if (validNumbers.length === 0) return 0;
    return validNumbers.reduce((sum, num) => sum + num, 0) / validNumbers.length;
}
```

---

**Next Chapter**: [📅 Dates and Time](06_Dates_and_Time.md)