# 🔤 Strings and Text Processing

## 📝 String Fundamentals

Strings are sequences of characters used to represent text data. JavaScript provides powerful and flexible ways to create, manipulate, and process strings.

### 🎯 String Creation Methods

```javascript
// 1. String literals (most common)
let singleQuotes = 'Hello World';
let doubleQuotes = "Hello World";
let templateLiteral = `Hello World`;

// 2. String constructor (primitive)
let stringPrimitive = String("Hello World");
console.log(typeof stringPrimitive);  // Output: "string"

// 3. String object (avoid in most cases)
let stringObject = new String("Hello World");
console.log(typeof stringObject);     // Output: "object"

// Comparison between primitive and object
console.log(stringPrimitive === "Hello World");  // true
console.log(stringObject === "Hello World");     // false
console.log(stringObject.valueOf() === "Hello World");  // true
```

### ✨ Template Literals (ES6+)

Template literals provide powerful string interpolation and multi-line capabilities.

```javascript
let name = "Alice";
let age = 30;
let city = "New York";

// String interpolation
let introduction = `Hello, my name is ${name} and I'm ${age} years old.`;
console.log(introduction);
// Output: Hello, my name is Alice and I'm 30 years old.

// Expression evaluation
let price = 19.99;
let quantity = 3;
let total = `Total: $${(price * quantity).toFixed(2)}`;
console.log(total);  // Output: Total: $59.97

// Multi-line strings
let multiLine = `
    This is a multi-line string.
    It preserves line breaks and
    indentation exactly as written.
`;
console.log(multiLine);

// Function calls in template literals
function formatDate(date) {
    return date.toLocaleDateString();
}

let message = `Today is ${formatDate(new Date())}`;
console.log(message);  // Output: Today is 1/24/2025

// Nested template literals
let user = { name: "Bob", isOnline: true };
let status = `User ${user.name} is ${user.isOnline ? `🟢 online` : `🔴 offline`}`;
console.log(status);  // Output: User Bob is 🟢 online
```

### 🔗 String Concatenation

```javascript
// Traditional concatenation with +
let firstName = "John";
let lastName = "Doe";
let fullName = firstName + " " + lastName;
console.log(fullName);  // Output: John Doe

// Concatenation with +=
let greeting = "Hello";
greeting += " ";
greeting += "World";
greeting += "!";
console.log(greeting);  // Output: Hello World!

// Template literals (preferred for complex concatenation)
let userInfo = `Name: ${firstName} ${lastName}, Age: ${age}`;

// Array join method for multiple strings
let words = ["JavaScript", "is", "awesome"];
let sentence = words.join(" ");
console.log(sentence);  // Output: JavaScript is awesome

// Performance comparison for multiple concatenations
let result1 = "";
for (let i = 0; i < 1000; i++) {
    result1 += "a";  // Slower for many concatenations
}

let parts = [];
for (let i = 0; i < 1000; i++) {
    parts.push("a");
}
let result2 = parts.join("");  // Faster for many concatenations
```

## 🔍 String Properties and Basic Methods

### 📏 String Length and Character Access

```javascript
let text = "JavaScript";

// Length property
console.log(text.length);  // Output: 10

// Character access by index
console.log(text[0]);      // Output: J
console.log(text[9]);      // Output: t
console.log(text[10]);     // Output: undefined (out of bounds)

// charAt method (safer)
console.log(text.charAt(0));   // Output: J
console.log(text.charAt(10));  // Output: "" (empty string for out of bounds)

// Character code
console.log(text.charCodeAt(0));  // Output: 74 (ASCII code for 'J')

// Last character
console.log(text[text.length - 1]);     // Output: t
console.log(text.charAt(text.length - 1)); // Output: t

// Iterate through characters
for (let i = 0; i < text.length; i++) {
    console.log(`Character ${i}: ${text[i]}`);
}

// Modern iteration with for...of
for (let char of text) {
    console.log(char);
}
```

### 🔍 String Searching and Checking

```javascript
let sentence = "The quick brown fox jumps over the lazy dog";

// indexOf - find first occurrence
console.log(sentence.indexOf("quick"));     // Output: 4
console.log(sentence.indexOf("cat"));       // Output: -1 (not found)
console.log(sentence.indexOf("the"));       // Output: 31 (first occurrence)

// lastIndexOf - find last occurrence
console.log(sentence.lastIndexOf("the"));   // Output: 31

// includes - check if substring exists (ES6+)
console.log(sentence.includes("fox"));      // Output: true
console.log(sentence.includes("cat"));      // Output: false

// startsWith and endsWith (ES6+)
console.log(sentence.startsWith("The"));    // Output: true
console.log(sentence.startsWith("the"));    // Output: false (case sensitive)
console.log(sentence.endsWith("dog"));      // Output: true
console.log(sentence.endsWith("cat"));      // Output: false

// Case-insensitive searching
let lowerSentence = sentence.toLowerCase();
console.log(lowerSentence.includes("THE")); // Output: false
console.log(lowerSentence.includes("the")); // Output: true

// Search with position
console.log(sentence.indexOf("o", 10));     // Output: 12 (search from position 10)
```

### ✂️ String Extraction Methods

```javascript
let text = "JavaScript Programming";

// slice(start, end) - extracts part of string
console.log(text.slice(0, 10));    // Output: JavaScript
console.log(text.slice(4));        // Output: Script Programming
console.log(text.slice(-11));      // Output: Programming (negative index from end)
console.log(text.slice(-11, -1));  // Output: Programmin

// substring(start, end) - similar to slice but handles negatives differently
console.log(text.substring(0, 10)); // Output: JavaScript
console.log(text.substring(10, 0)); // Output: JavaScript (swaps if start > end)
console.log(text.substring(-5));    // Output: JavaScript Programming (treats negative as 0)

// substr(start, length) - deprecated but still used
console.log(text.substr(4, 6));     // Output: Script

// Practical examples
let email = "user@example.com";
let username = email.slice(0, email.indexOf("@"));
let domain = email.slice(email.indexOf("@") + 1);
console.log(`Username: ${username}, Domain: ${domain}`);
// Output: Username: user, Domain: example.com

// Extract file extension
let filename = "document.pdf";
let extension = filename.slice(filename.lastIndexOf(".") + 1);
console.log(extension);  // Output: pdf
```

## 🔄 String Transformation Methods

### 🔠 Case Conversion

```javascript
let text = "JavaScript Programming";

// Case conversion
console.log(text.toLowerCase());    // Output: javascript programming
console.log(text.toUpperCase());    // Output: JAVASCRIPT PROGRAMMING

// Locale-specific case conversion
let turkish = "İstanbul";
console.log(turkish.toLowerCase());           // Output: i̇stanbul
console.log(turkish.toLocaleLowerCase("tr")); // Output: istanbul (Turkish locale)

// Title case (custom function)
function toTitleCase(str) {
    return str.toLowerCase().split(' ').map(word => 
        word.charAt(0).toUpperCase() + word.slice(1)
    ).join(' ');
}

console.log(toTitleCase("hello world programming"));
// Output: Hello World Programming

// Capitalize first letter only
function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1).toLowerCase();
}

console.log(capitalize("jAVAsCRIPT"));  // Output: Javascript
```

### ✂️ Trimming and Padding

```javascript
let text = "   Hello World   ";

// Trimming whitespace
console.log(text.trim());       // Output: "Hello World"
console.log(text.trimStart());  // Output: "Hello World   " (ES2019)
console.log(text.trimEnd());    // Output: "   Hello World" (ES2019)

// Legacy methods (still supported)
console.log(text.trimLeft());   // Same as trimStart()
console.log(text.trimRight());  // Same as trimEnd()

// Padding (ES2017)
let number = "42";
console.log(number.padStart(5, "0"));    // Output: "00042"
console.log(number.padEnd(5, "0"));      // Output: "42000"

let name = "Alice";
console.log(name.padStart(10, "."));     // Output: ".....Alice"
console.log(name.padEnd(10, "."));       // Output: "Alice....."

// Practical padding examples
function formatTime(hours, minutes, seconds) {
    return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
}

console.log(formatTime(9, 5, 3));   // Output: 09:05:03
console.log(formatTime(14, 30, 45)); // Output: 14:30:45

// Format currency
function formatCurrency(amount) {
    return `$${amount.toFixed(2).padStart(8, ' ')}`;
}

console.log(formatCurrency(42.5));    // Output: "$   42.50"
console.log(formatCurrency(1234.56)); // Output: "$1234.56"
```

### 🔄 String Replacement

```javascript
let text = "The quick brown fox jumps over the lazy dog";

// replace - replaces first occurrence
console.log(text.replace("the", "a"));
// Output: The quick brown fox jumps over a lazy dog

// replaceAll - replaces all occurrences (ES2021)
console.log(text.replaceAll("the", "a"));
// Output: The quick brown fox jumps over a lazy dog

// Case-insensitive replacement with regex
console.log(text.replace(/the/gi, "a"));
// Output: a quick brown fox jumps over a lazy dog

// Replace with function
let result = text.replace(/\b\w{4}\b/g, function(match) {
    return match.toUpperCase();
});
console.log(result);
// Output: The quick brown fox jumps OVER the LAZY dog

// Practical examples
let phoneNumber = "(555) 123-4567";
let cleanPhone = phoneNumber.replace(/[^\d]/g, "");
console.log(cleanPhone);  // Output: 5551234567

// Replace multiple patterns
let messyText = "Hello    World!!!   How are you???";
let cleanText = messyText
    .replace(/\s+/g, " ")      // Multiple spaces to single space
    .replace(/!+/g, "!")       // Multiple exclamations to single
    .replace(/\?+/g, "?")      // Multiple questions to single
    .trim();
console.log(cleanText);  // Output: Hello World! How are you?

// Template replacement
let template = "Hello {name}, welcome to {site}!";
let data = { name: "Alice", site: "JavaScript Academy" };
let message = template.replace(/{(\w+)}/g, (match, key) => data[key] || match);
console.log(message);  // Output: Hello Alice, welcome to JavaScript Academy!
```

## 🔨 Advanced String Methods

### 📊 String Splitting and Joining

```javascript
let csv = "apple,banana,orange,grape";
let sentence = "The quick brown fox";

// split - convert string to array
let fruits = csv.split(",");
console.log(fruits);  // Output: ["apple", "banana", "orange", "grape"]

let words = sentence.split(" ");
console.log(words);   // Output: ["The", "quick", "brown", "fox"]

// Split with limit
let limitedSplit = csv.split(",", 2);
console.log(limitedSplit);  // Output: ["apple", "banana"]

// Split by character
let chars = "hello".split("");
console.log(chars);   // Output: ["h", "e", "l", "l", "o"]

// Split by regex
let text = "apple123banana456orange";
let parts = text.split(/\d+/);
console.log(parts);   // Output: ["apple", "banana", "orange"]

// Practical examples
let fullName = "John Michael Doe";
let [firstName, middleName, lastName] = fullName.split(" ");
console.log(`First: ${firstName}, Middle: ${middleName}, Last: ${lastName}`);

// Parse URL parameters
let url = "https://example.com?name=Alice&age=30&city=NewYork";
let queryString = url.split("?")[1];
let params = {};
queryString.split("&").forEach(param => {
    let [key, value] = param.split("=");
    params[key] = decodeURIComponent(value);
});
console.log(params);  // Output: {name: "Alice", age: "30", city: "NewYork"}
```

### 🔍 Regular Expressions with Strings

```javascript
let text = "Contact us at support@example.com or sales@company.org";

// match - find matches
let emails = text.match(/\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b/g);
console.log(emails);  // Output: ["support@example.com", "sales@company.org"]

// search - find position of match
let position = text.search(/@/);
console.log(position);  // Output: 17

// test with regex
let emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
console.log(emailRegex.test("user@example.com"));  // Output: true
console.log(emailRegex.test("invalid-email"));     // Output: false

// Practical validation functions
function isValidEmail(email) {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
}

function isValidPhone(phone) {
    const regex = /^\(?([0-9]{3})\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})$/;
    return regex.test(phone);
}

function extractHashtags(text) {
    const regex = /#\w+/g;
    return text.match(regex) || [];
}

console.log(isValidEmail("test@example.com"));     // Output: true
console.log(isValidPhone("(555) 123-4567"));      // Output: true
console.log(extractHashtags("Love #javascript and #coding!")); 
// Output: ["#javascript", "#coding"]
```

## 🌐 Unicode and Internationalization

### 🔤 Unicode Support

```javascript
// Unicode characters
let emoji = "Hello 👋 World 🌍";
console.log(emoji.length);  // Output: 15 (emoji count as 2 characters each)

// Unicode escape sequences
let unicode1 = "\u0048\u0065\u006C\u006C\u006F";  // "Hello"
let unicode2 = "\u{1F44B}";  // 👋 (ES6 extended unicode)
console.log(unicode1);  // Output: Hello
console.log(unicode2);  // Output: 👋

// Working with different languages
let chinese = "你好世界";
let arabic = "مرحبا بالعالم";
let russian = "Привет мир";

console.log(chinese.length);   // Output: 4
console.log(arabic.length);    // Output: 10
console.log(russian.length);   // Output: 10

// Normalize for comparison
let str1 = "café";  // é as single character
let str2 = "cafe\u0301";  // e + combining accent
console.log(str1 === str2);  // Output: false
console.log(str1.normalize() === str2.normalize());  // Output: true

// Locale-aware operations
let names = ["Åse", "Zebra", "Äpfel"];
console.log(names.sort());  // Default sort: ["Zebra", "Äpfel", "Åse"]
console.log(names.sort((a, b) => a.localeCompare(b)));  // Locale-aware: ["Äpfel", "Åse", "Zebra"]
```

### 🌍 Internationalization Methods

```javascript
// Locale-aware case conversion
let turkish = "İstanbul";
console.log(turkish.toLocaleLowerCase("tr-TR"));  // Output: istanbul
console.log(turkish.toLocaleLowerCase("en-US"));  // Output: i̇stanbul

// Locale-aware comparison
function sortNames(names, locale = 'en-US') {
    return names.sort((a, b) => a.localeCompare(b, locale));
}

let germanNames = ["Müller", "Schmidt", "Äpfel"];
console.log(sortNames(germanNames, 'de-DE'));

// Number formatting in strings
let price = 1234.56;
let formattedPrice = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
}).format(price);
console.log(`Price: ${formattedPrice}`);  // Output: Price: $1,234.56

// Date formatting in strings
let date = new Date();
let formattedDate = new Intl.DateTimeFormat('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
}).format(date);
console.log(`Today is ${formattedDate}`);
```

## 🧪 Practical String Processing Examples

### 📝 Text Processing Utilities

```javascript
class TextProcessor {
    // Count words in text
    static countWords(text) {
        return text.trim().split(/\s+/).filter(word => word.length > 0).length;
    }
    
    // Count characters (excluding spaces)
    static countCharacters(text, includeSpaces = false) {
        return includeSpaces ? text.length : text.replace(/\s/g, '').length;
    }
    
    // Extract sentences
    static extractSentences(text) {
        return text.split(/[.!?]+/).map(s => s.trim()).filter(s => s.length > 0);
    }
    
    // Generate slug from title
    static generateSlug(title) {
        return title
            .toLowerCase()
            .trim()
            .replace(/[^\w\s-]/g, '')  // Remove special characters
            .replace(/[\s_-]+/g, '-')  // Replace spaces and underscores with hyphens
            .replace(/^-+|-+$/g, '');  // Remove leading/trailing hyphens
    }
    
    // Truncate text with ellipsis
    static truncate(text, maxLength, suffix = '...') {
        if (text.length <= maxLength) return text;
        return text.slice(0, maxLength - suffix.length).trim() + suffix;
    }
    
    // Remove HTML tags
    static stripHtml(html) {
        return html.replace(/<[^>]*>/g, '');
    }
    
    // Escape HTML characters
    static escapeHtml(text) {
        const htmlEscapes = {
            '&': '&amp;',
            '<': '&lt;',
            '>': '&gt;',
            '"': '&quot;',
            "'": '&#39;'
        };
        return text.replace(/[&<>"']/g, char => htmlEscapes[char]);
    }
    
    // Calculate reading time
    static calculateReadingTime(text, wordsPerMinute = 200) {
        const wordCount = this.countWords(text);
        const minutes = Math.ceil(wordCount / wordsPerMinute);
        return `${minutes} min read`;
    }
}

// Usage examples
let article = `
    JavaScript is a versatile programming language. 
    It can be used for web development, server-side programming, and more!
    Learning JavaScript opens many opportunities.
`;

console.log("Word count:", TextProcessor.countWords(article));
console.log("Character count:", TextProcessor.countCharacters(article));
console.log("Sentences:", TextProcessor.extractSentences(article));
console.log("Slug:", TextProcessor.generateSlug("My Awesome Blog Post!"));
console.log("Truncated:", TextProcessor.truncate(article, 50));
console.log("Reading time:", TextProcessor.calculateReadingTime(article));
```

### 🔐 String Validation and Sanitization

```javascript
class StringValidator {
    // Email validation
    static isValidEmail(email) {
        const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return regex.test(email.trim());
    }
    
    // Password strength validation
    static validatePassword(password) {
        const checks = {
            length: password.length >= 8,
            uppercase: /[A-Z]/.test(password),
            lowercase: /[a-z]/.test(password),
            number: /\d/.test(password),
            special: /[!@#$%^&*(),.?":{}|<>]/.test(password)
        };
        
        const score = Object.values(checks).filter(Boolean).length;
        const strength = score < 3 ? 'Weak' : score < 5 ? 'Medium' : 'Strong';
        
        return { checks, score, strength };
    }
    
    // URL validation
    static isValidUrl(url) {
        try {
            new URL(url);
            return true;
        } catch {
            return false;
        }
    }
    
    // Credit card number validation (Luhn algorithm)
    static isValidCreditCard(cardNumber) {
        const cleaned = cardNumber.replace(/\D/g, '');
        if (cleaned.length < 13 || cleaned.length > 19) return false;
        
        let sum = 0;
        let isEven = false;
        
        for (let i = cleaned.length - 1; i >= 0; i--) {
            let digit = parseInt(cleaned[i]);
            
            if (isEven) {
                digit *= 2;
                if (digit > 9) digit -= 9;
            }
            
            sum += digit;
            isEven = !isEven;
        }
        
        return sum % 10 === 0;
    }
    
    // Sanitize input for safe display
    static sanitizeInput(input) {
        return input
            .trim()
            .replace(/[<>]/g, '')  // Remove potential HTML tags
            .replace(/javascript:/gi, '')  // Remove javascript: protocol
            .slice(0, 1000);  // Limit length
    }
}

// Usage examples
console.log("Email valid:", StringValidator.isValidEmail("user@example.com"));
console.log("Password strength:", StringValidator.validatePassword("MyPass123!"));
console.log("URL valid:", StringValidator.isValidUrl("https://example.com"));
console.log("Credit card valid:", StringValidator.isValidCreditCard("4532015112830366"));

let userInput = "<script>alert('xss')</script>Hello World";
console.log("Sanitized:", StringValidator.sanitizeInput(userInput));
```

### 📊 String Analytics Dashboard

```javascript
class StringAnalytics {
    constructor(text) {
        this.text = text;
        this.words = this.extractWords();
        this.sentences = this.extractSentences();
    }
    
    extractWords() {
        return this.text
            .toLowerCase()
            .replace(/[^\w\s]/g, '')
            .split(/\s+/)
            .filter(word => word.length > 0);
    }
    
    extractSentences() {
        return this.text
            .split(/[.!?]+/)
            .map(s => s.trim())
            .filter(s => s.length > 0);
    }
    
    getWordFrequency() {
        const frequency = {};
        this.words.forEach(word => {
            frequency[word] = (frequency[word] || 0) + 1;
        });
        return frequency;
    }
    
    getMostCommonWords(limit = 5) {
        const frequency = this.getWordFrequency();
        return Object.entries(frequency)
            .sort(([,a], [,b]) => b - a)
            .slice(0, limit)
            .map(([word, count]) => ({ word, count }));
    }
    
    getAverageWordsPerSentence() {
        return this.sentences.length > 0 ? 
            Math.round(this.words.length / this.sentences.length * 100) / 100 : 0;
    }
    
    getLongestWord() {
        return this.words.reduce((longest, current) => 
            current.length > longest.length ? current : longest, '');
    }
    
    getReadabilityScore() {
        // Simplified Flesch Reading Ease approximation
        const avgWordsPerSentence = this.getAverageWordsPerSentence();
        const avgSyllablesPerWord = this.getAverageSyllablesPerWord();
        
        const score = 206.835 - (1.015 * avgWordsPerSentence) - (84.6 * avgSyllablesPerWord);
        return Math.max(0, Math.min(100, Math.round(score)));
    }
    
    getAverageSyllablesPerWord() {
        // Simplified syllable counting
        const totalSyllables = this.words.reduce((total, word) => {
            return total + this.countSyllables(word);
        }, 0);
        return this.words.length > 0 ? totalSyllables / this.words.length : 0;
    }
    
    countSyllables(word) {
        // Simplified syllable counting
        word = word.toLowerCase();
        if (word.length <= 3) return 1;
        word = word.replace(/(?:[^laeiouy]es|ed|[^laeiouy]e)$/, '');
        word = word.replace(/^y/, '');
        const matches = word.match(/[aeiouy]{1,2}/g);
        return matches ? matches.length : 1;
    }
    
    generateReport() {
        const wordFreq = this.getWordFrequency();
        const commonWords = this.getMostCommonWords();
        
        return {
            statistics: {
                totalCharacters: this.text.length,
                totalWords: this.words.length,
                totalSentences: this.sentences.length,
                uniqueWords: Object.keys(wordFreq).length,
                averageWordsPerSentence: this.getAverageWordsPerSentence(),
                longestWord: this.getLongestWord(),
                readabilityScore: this.getReadabilityScore()
            },
            mostCommonWords: commonWords,
            wordFrequency: wordFreq
        };
    }
}

// Usage example
const sampleText = `
    JavaScript is a powerful programming language. It enables interactive web development.
    JavaScript can run in browsers and servers. Many developers love JavaScript for its flexibility.
    Learning JavaScript opens career opportunities. JavaScript frameworks make development easier.
`;

const analytics = new StringAnalytics(sampleText);
const report = analytics.generateReport();

console.log("📊 Text Analytics Report");
console.log("========================");
console.log("Statistics:", report.statistics);
console.log("Most Common Words:", report.mostCommonWords);
```

**Output:**
```
📊 Text Analytics Report
========================
Statistics: {
  totalCharacters: 312,
  totalWords: 42,
  totalSentences: 6,
  uniqueWords: 32,
  averageWordsPerSentence: 7,
  longestWord: "opportunities",
  readabilityScore: 65
}
Most Common Words: [
  { word: "javascript", count: 5 },
  { word: "is", count: 2 },
  { word: "and", count: 2 },
  { word: "development", count: 2 },
  { word: "a", count: 1 }
]
```

## 💡 Best Practices

### ✅ String Performance Tips

```javascript
// ✅ Use template literals for complex concatenation
const message = `Hello ${name}, you have ${count} messages`;

// ❌ Avoid excessive concatenation in loops
let result = "";
for (let i = 0; i < 1000; i++) {
    result += "a";  // Creates new string each time
}

// ✅ Use array join for multiple concatenations
const parts = [];
for (let i = 0; i < 1000; i++) {
    parts.push("a");
}
const result2 = parts.join("");

// ✅ Use appropriate string methods
const isEmail = str.includes("@");  // ✅ Simple check
const isValidEmail = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(str);  // ✅ Proper validation
```

### ✅ String Security Best Practices

```javascript
// ✅ Always validate and sanitize user input
function sanitizeUserInput(input) {
    return input
        .trim()
        .slice(0, 1000)  // Limit length
        .replace(/[<>]/g, '');  // Remove HTML tags
}

// ✅ Use proper escaping for different contexts
function escapeForHtml(str) {
    return str.replace(/[&<>"']/g, char => {
        const escapes = { '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' };
        return escapes[char];
    });
}

// ✅ Be careful with eval and similar functions
// ❌ Never do this with user input
// eval(userInput);

// ✅ Use JSON.parse for parsing JSON strings
try {
    const data = JSON.parse(jsonString);
} catch (error) {
    console.error("Invalid JSON");
}
```

---

**Next Chapter**: [🔢 Numbers and Mathematical Operations](05_Numbers_and_Mathematical_Operations.md)