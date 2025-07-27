# 🏗️ Objects and Properties

## 📦 Object Fundamentals

Objects are collections of **key-value pairs** where keys are strings (or Symbols) and values can be any data type. Objects are the foundation of JavaScript and represent real-world entities with properties and behaviors.

### 🎯 Object Creation Methods

```javascript
// Object literal (most common)
let person = {
    name: "Alice",
    age: 30,
    city: "New York",
    isEmployed: true
};

// Empty object
let emptyObj = {};

// Object constructor
let obj1 = new Object();
obj1.name = "Bob";
obj1.age = 25;

// Object.create() - create with specific prototype
let prototypeObj = { species: "human" };
let person2 = Object.create(prototypeObj);
person2.name = "Charlie";

console.log(person2.species); // Output: human (inherited)
console.log(person2.name);    // Output: Charlie (own property)

// Constructor function (traditional OOP)
function Person(name, age) {
    this.name = name;
    this.age = age;
}
let person3 = new Person("Diana", 28);

// ES6 Class (modern OOP)
class PersonClass {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}
let person4 = new PersonClass("Eve", 32);

console.log(person);   // Output: {name: "Alice", age: 30, city: "New York", isEmployed: true}
console.log(person3);  // Output: Person {name: "Diana", age: 28}
console.log(person4);  // Output: PersonClass {name: "Eve", age: 32}
```

### 🔑 Property Access Methods

```javascript
let user = {
    firstName: "John",
    lastName: "Doe",
    age: 35,
    "email-address": "john@example.com",
    "123": "numeric key",
    address: {
        street: "123 Main St",
        city: "Boston"
    }
};

// Dot notation (most common)
console.log(user.firstName);    // Output: John
console.log(user.age);          // Output: 35

// Bracket notation (for dynamic keys or special characters)
console.log(user["lastName"]);       // Output: Doe
console.log(user["email-address"]);  // Output: john@example.com
console.log(user["123"]);            // Output: numeric key

// Dynamic property access
let propertyName = "age";
console.log(user[propertyName]);     // Output: 35

// Nested object access
console.log(user.address.city);      // Output: Boston
console.log(user["address"]["street"]); // Output: 123 Main St

// Mixed notation
console.log(user.address["city"]);   // Output: Boston

// Property assignment
user.phone = "555-1234";             // Add new property
user["country"] = "USA";             // Add with bracket notation
user.age = 36;                       // Update existing property

console.log(user.phone);   // Output: 555-1234
console.log(user.country); // Output: USA
console.log(user.age);     // Output: 36
```

### 🔍 Property Existence and Enumeration

```javascript
let product = {
    name: "Laptop",
    price: 999,
    category: "Electronics",
    inStock: true
};

// Check if property exists
console.log("name" in product);           // Output: true
console.log("color" in product);          // Output: false

// hasOwnProperty (own properties only, not inherited)
console.log(product.hasOwnProperty("name"));     // Output: true
console.log(product.hasOwnProperty("toString")); // Output: false (inherited)

// Object.hasOwn() (ES2022) - safer alternative
console.log(Object.hasOwn(product, "name"));     // Output: true

// Check for undefined vs non-existent
product.description = undefined;
console.log("description" in product);           // Output: true
console.log(product.description);                // Output: undefined
console.log(product.nonExistent);                // Output: undefined

// Get all property names
console.log(Object.keys(product));               // Own enumerable properties
console.log(Object.getOwnPropertyNames(product)); // All own properties

// Get property values
console.log(Object.values(product));             // Values of own enumerable properties

// Get key-value pairs
console.log(Object.entries(product));            // [key, value] pairs

// Iterate over properties
for (let key in product) {
    console.log(`${key}: ${product[key]}`);
}

// Iterate over own properties only
for (let key in product) {
    if (product.hasOwnProperty(key)) {
        console.log(`${key}: ${product[key]}`);
    }
}

// Modern iteration with Object.keys()
Object.keys(product).forEach(key => {
    console.log(`${key}: ${product[key]}`);
});
```

## 🎨 Advanced Object Features

### 🧮 Computed Property Names

```javascript
// ES6 computed property names
let prefix = "user";
let id = 123;

let dynamicObj = {
    [prefix + "Id"]: id,
    [prefix + "Name"]: "Alice",
    [`${prefix}Email`]: "alice@example.com",
    [Date.now()]: "timestamp property"
};

console.log(dynamicObj);
// Output: {userId: 123, userName: "Alice", userEmail: "alice@example.com", 1737705600000: "timestamp property"}

// Function-generated property names
function createPropertyName(base, suffix) {
    return `${base}_${suffix}`;
}

let configObj = {
    [createPropertyName("api", "url")]: "https://api.example.com",
    [createPropertyName("api", "key")]: "secret123",
    [createPropertyName("db", "host")]: "localhost"
};

console.log(configObj);
// Output: {api_url: "https://api.example.com", api_key: "secret123", db_host: "localhost"}

// Using variables as property names
let fields = ["name", "email", "phone"];
let formData = {};

fields.forEach((field, index) => {
    formData[field] = `value${index + 1}`;
});

console.log(formData); // Output: {name: "value1", email: "value2", phone: "value3"}
```

### 🏷️ Symbol Properties

```javascript
// Symbols as property keys
let nameSymbol = Symbol("name");
let ageSymbol = Symbol("age");
let secretSymbol = Symbol("secret");

let person = {
    [nameSymbol]: "Alice",
    [ageSymbol]: 30,
    regularProperty: "visible",
    [secretSymbol]: "hidden data"
};

console.log(person[nameSymbol]);        // Output: Alice
console.log(person.regularProperty);    // Output: visible

// Symbol properties are not enumerable in normal iteration
console.log(Object.keys(person));       // Output: ["regularProperty"]
console.log(Object.values(person));     // Output: ["visible"]

// Get symbol properties
console.log(Object.getOwnPropertySymbols(person)); // [Symbol(name), Symbol(age), Symbol(secret)]

// Well-known symbols
let iterableObj = {
    data: [1, 2, 3],
    [Symbol.iterator]: function* () {
        for (let item of this.data) {
            yield item;
        }
    }
};

// Now the object is iterable
for (let value of iterableObj) {
    console.log(value); // Output: 1, 2, 3
}

// Symbol for private-like properties
const PRIVATE_DATA = Symbol("privateData");

class User {
    constructor(name, email) {
        this.name = name;
        this.email = email;
        this[PRIVATE_DATA] = {
            id: Math.random(),
            createdAt: new Date()
        };
    }
    
    getPrivateData() {
        return this[PRIVATE_DATA];
    }
}

let user = new User("Bob", "bob@example.com");
console.log(user.name);                    // Output: Bob
console.log(user[PRIVATE_DATA]);           // Accessible but not obvious
console.log(Object.keys(user));            // Output: ["name", "email"] (symbol not included)
```

## 🔧 Object Manipulation Methods

### 📋 Copying and Cloning Objects

```javascript
let original = {
    name: "Alice",
    age: 30,
    address: {
        city: "New York",
        country: "USA"
    },
    hobbies: ["reading", "swimming"]
};

// Shallow copy methods
let shallowCopy1 = Object.assign({}, original);
let shallowCopy2 = { ...original };  // Spread operator (ES2018)

// Modify nested object in copy
shallowCopy1.address.city = "Boston";
console.log(original.address.city);    // Output: Boston (original affected!)
console.log(shallowCopy1.address.city); // Output: Boston

// Deep copy (simple objects only)
let deepCopy1 = JSON.parse(JSON.stringify(original));
deepCopy1.address.city = "Chicago";
console.log(original.address.city);    // Output: Boston (original not affected)
console.log(deepCopy1.address.city);   // Output: Chicago

// Custom deep copy function
function deepCopy(obj) {
    if (obj === null || typeof obj !== "object") {
        return obj;
    }
    
    if (obj instanceof Date) {
        return new Date(obj.getTime());
    }
    
    if (obj instanceof Array) {
        return obj.map(item => deepCopy(item));
    }
    
    if (typeof obj === "object") {
        const copy = {};
        Object.keys(obj).forEach(key => {
            copy[key] = deepCopy(obj[key]);
        });
        return copy;
    }
}

let deepCopy2 = deepCopy(original);
deepCopy2.address.city = "Miami";
deepCopy2.hobbies.push("cycling");

console.log(original.address.city);     // Output: Boston (unchanged)
console.log(original.hobbies);          // Output: ["reading", "swimming"] (unchanged)
console.log(deepCopy2.address.city);    // Output: Miami
console.log(deepCopy2.hobbies);         // Output: ["reading", "swimming", "cycling"]
```

### 🔗 Merging Objects

```javascript
let defaults = {
    theme: "light",
    language: "en",
    notifications: true,
    autoSave: false
};

let userPreferences = {
    theme: "dark",
    language: "es",
    fontSize: 14
};

// Object.assign() - mutates first object
let config1 = Object.assign({}, defaults, userPreferences);
console.log(config1);
// Output: {theme: "dark", language: "es", notifications: true, autoSave: false, fontSize: 14}

// Spread operator - creates new object
let config2 = { ...defaults, ...userPreferences };
console.log(config2);
// Output: {theme: "dark", language: "es", notifications: true, autoSave: false, fontSize: 14}

// Multiple object merging
let systemDefaults = { version: "1.0", debug: false };
let appConfig = { name: "MyApp", version: "2.0" };
let userConfig = { theme: "custom", debug: true };

let finalConfig = { ...systemDefaults, ...appConfig, ...userConfig };
console.log(finalConfig);
// Output: {version: "2.0", debug: true, name: "MyApp", theme: "custom"}

// Conditional merging
let optionalConfig = userPreferences.premium ? { premiumFeatures: true } : {};
let mergedConfig = { ...defaults, ...userPreferences, ...optionalConfig };

// Deep merging function
function deepMerge(target, source) {
    const result = { ...target };
    
    for (let key in source) {
        if (source.hasOwnProperty(key)) {
            if (typeof source[key] === 'object' && source[key] !== null && !Array.isArray(source[key])) {
                result[key] = deepMerge(result[key] || {}, source[key]);
            } else {
                result[key] = source[key];
            }
        }
    }
    
    return result;
}

let nestedDefaults = {
    ui: { theme: "light", sidebar: { width: 200, collapsed: false } },
    api: { timeout: 5000, retries: 3 }
};

let nestedUserPrefs = {
    ui: { theme: "dark", sidebar: { collapsed: true } },
    api: { timeout: 10000 }
};

let deepMerged = deepMerge(nestedDefaults, nestedUserPrefs);
console.log(deepMerged);
// Output: {ui: {theme: "dark", sidebar: {width: 200, collapsed: true}}, api: {timeout: 10000, retries: 3}}
```

### 🔒 Object Property Descriptors

```javascript
let obj = {};

// Define property with descriptor
Object.defineProperty(obj, "name", {
    value: "Alice",
    writable: true,      // Can be changed
    enumerable: true,    // Shows up in for...in and Object.keys()
    configurable: true   // Can be deleted or reconfigured
});

// Define read-only property
Object.defineProperty(obj, "id", {
    value: 123,
    writable: false,     // Cannot be changed
    enumerable: true,
    configurable: false  // Cannot be deleted
});

// Define computed property (getter/setter)
Object.defineProperty(obj, "fullName", {
    get: function() {
        return `${this.firstName} ${this.lastName}`;
    },
    set: function(value) {
        [this.firstName, this.lastName] = value.split(" ");
    },
    enumerable: true,
    configurable: true
});

obj.firstName = "John";
obj.lastName = "Doe";
console.log(obj.fullName);  // Output: John Doe

obj.fullName = "Jane Smith";
console.log(obj.firstName); // Output: Jane
console.log(obj.lastName);  // Output: Smith

// Get property descriptor
console.log(Object.getOwnPropertyDescriptor(obj, "name"));
// Output: {value: "Alice", writable: true, enumerable: true, configurable: true}

// Define multiple properties
Object.defineProperties(obj, {
    age: {
        value: 30,
        writable: true,
        enumerable: true
    },
    email: {
        value: "john@example.com",
        writable: false,
        enumerable: true
    }
});

// Prevent extensions, sealing, and freezing
let mutableObj = { name: "Test", value: 42 };

// Prevent adding new properties
Object.preventExtensions(mutableObj);
mutableObj.newProp = "won't work";
console.log(mutableObj.newProp); // Output: undefined

// Seal object (prevent add/delete, allow modify)
let sealedObj = { name: "Sealed", value: 100 };
Object.seal(sealedObj);
sealedObj.value = 200;        // Works
sealedObj.newProp = "no";     // Doesn't work
delete sealedObj.name;        // Doesn't work
console.log(sealedObj.value); // Output: 200

// Freeze object (completely immutable)
let frozenObj = { name: "Frozen", value: 300 };
Object.freeze(frozenObj);
frozenObj.value = 400;        // Doesn't work
frozenObj.newProp = "no";     // Doesn't work
console.log(frozenObj.value); // Output: 300

// Check object state
console.log(Object.isExtensible(mutableObj)); // Output: false
console.log(Object.isSealed(sealedObj));      // Output: true
console.log(Object.isFrozen(frozenObj));      // Output: true
```

## 🎯 Object Patterns and Techniques

### 🏭 Factory Pattern

```javascript
// Factory function for creating objects
function createUser(name, email, role = "user") {
    return {
        name,
        email,
        role,
        createdAt: new Date(),
        
        // Methods
        getInfo() {
            return `${this.name} (${this.email}) - ${this.role}`;
        },
        
        updateEmail(newEmail) {
            this.email = newEmail;
            this.updatedAt = new Date();
        },
        
        hasPermission(permission) {
            const permissions = {
                user: ["read"],
                admin: ["read", "write", "delete"],
                moderator: ["read", "write"]
            };
            return permissions[this.role]?.includes(permission) || false;
        }
    };
}

// Usage
let user1 = createUser("Alice", "alice@example.com");
let admin1 = createUser("Bob", "bob@example.com", "admin");

console.log(user1.getInfo());                    // Output: Alice (alice@example.com) - user
console.log(admin1.hasPermission("delete"));     // Output: true
console.log(user1.hasPermission("delete"));      // Output: false

// Advanced factory with configuration
function createProduct(config) {
    const defaults = {
        name: "Unnamed Product",
        price: 0,
        category: "General",
        inStock: true,
        tags: []
    };
    
    const product = { ...defaults, ...config };
    
    return {
        ...product,
        
        // Computed properties
        get displayPrice() {
            return `$${this.price.toFixed(2)}`;
        },
        
        get isAffordable() {
            return this.price < 100;
        },
        
        // Methods
        addTag(tag) {
            if (!this.tags.includes(tag)) {
                this.tags.push(tag);
            }
        },
        
        removeTag(tag) {
            this.tags = this.tags.filter(t => t !== tag);
        },
        
        applyDiscount(percentage) {
            this.price *= (1 - percentage / 100);
        },
        
        toJSON() {
            return {
                name: this.name,
                price: this.price,
                category: this.category,
                inStock: this.inStock,
                tags: [...this.tags]
            };
        }
    };
}

let laptop = createProduct({
    name: "Gaming Laptop",
    price: 1299.99,
    category: "Electronics",
    tags: ["gaming", "portable"]
});

laptop.addTag("high-performance");
laptop.applyDiscount(10);
console.log(laptop.displayPrice);  // Output: $1169.99
console.log(laptop.toJSON());
```

### 🔧 Mixin Pattern

```javascript
// Mixin objects with reusable functionality
const Timestamped = {
    addTimestamp() {
        this.createdAt = new Date();
        return this;
    },
    
    updateTimestamp() {
        this.updatedAt = new Date();
        return this;
    },
    
    getAge() {
        return this.createdAt ? Date.now() - this.createdAt.getTime() : 0;
    }
};

const Validatable = {
    addValidation(field, validator) {
        if (!this._validators) this._validators = {};
        this._validators[field] = validator;
        return this;
    },
    
    validate() {
        if (!this._validators) return { valid: true, errors: [] };
        
        const errors = [];
        for (let field in this._validators) {
            const validator = this._validators[field];
            if (!validator(this[field])) {
                errors.push(`Invalid ${field}: ${this[field]}`);
            }
        }
        
        return {
            valid: errors.length === 0,
            errors
        };
    }
};

const Serializable = {
    toJSON() {
        const result = {};
        for (let key in this) {
            if (this.hasOwnProperty(key) && !key.startsWith('_')) {
                result[key] = this[key];
            }
        }
        return result;
    },
    
    fromJSON(json) {
        Object.assign(this, json);
        return this;
    }
};

// Create object with mixins
function createValidatedUser(name, email) {
    const user = {
        name,
        email
    };
    
    // Apply mixins
    Object.assign(user, Timestamped, Validatable, Serializable);
    
    // Add validations
    user.addValidation('name', name => name && name.length > 0);
    user.addValidation('email', email => email && email.includes('@'));
    
    // Initialize timestamp
    user.addTimestamp();
    
    return user;
}

let user = createValidatedUser("Alice", "alice@example.com");
console.log(user.validate());        // Output: {valid: true, errors: []}
console.log(user.toJSON());

let invalidUser = createValidatedUser("", "invalid-email");
console.log(invalidUser.validate()); // Output: {valid: false, errors: [...]}
```

### 🎭 Proxy Pattern

```javascript
// Proxy for object property access control
function createSecureObject(target, allowedKeys = []) {
    return new Proxy(target, {
        get(obj, prop) {
            if (allowedKeys.length > 0 && !allowedKeys.includes(prop)) {
                throw new Error(`Access denied to property: ${prop}`);
            }
            return obj[prop];
        },
        
        set(obj, prop, value) {
            if (allowedKeys.length > 0 && !allowedKeys.includes(prop)) {
                throw new Error(`Cannot set property: ${prop}`);
            }
            obj[prop] = value;
            return true;
        },
        
        has(obj, prop) {
            return allowedKeys.length === 0 || allowedKeys.includes(prop);
        },
        
        ownKeys(obj) {
            return allowedKeys.length > 0 ? allowedKeys : Object.keys(obj);
        }
    });
}

let secureData = createSecureObject(
    { name: "Alice", age: 30, secret: "hidden" },
    ["name", "age"]
);

console.log(secureData.name);  // Output: Alice
// console.log(secureData.secret); // Error: Access denied to property: secret

// Proxy for default values
function createDefaultObject(defaults) {
    return new Proxy({}, {
        get(obj, prop) {
            return prop in obj ? obj[prop] : defaults[prop];
        }
    });
}

let config = createDefaultObject({
    theme: "light",
    language: "en",
    timeout: 5000
});

config.theme = "dark";
console.log(config.theme);    // Output: dark
console.log(config.language); // Output: en (default)
console.log(config.timeout);  // Output: 5000 (default)

// Proxy for property change tracking
function createObservableObject(target, onChange) {
    return new Proxy(target, {
        set(obj, prop, value) {
            const oldValue = obj[prop];
            obj[prop] = value;
            onChange(prop, value, oldValue);
            return true;
        }
    });
}

let observedUser = createObservableObject(
    { name: "Bob", age: 25 },
    (prop, newValue, oldValue) => {
        console.log(`Property ${prop} changed from ${oldValue} to ${newValue}`);
    }
);

observedUser.age = 26;  // Output: Property age changed from 25 to 26
observedUser.name = "Robert";  // Output: Property name changed from Bob to Robert
```

## 🧪 Practical Object Applications

### 📊 Configuration Management

```javascript
class ConfigManager {
    constructor(defaults = {}) {
        this._config = { ...defaults };
        this._listeners = {};
    }
    
    get(key, defaultValue = undefined) {
        return this._getNestedValue(this._config, key, defaultValue);
    }
    
    set(key, value) {
        const oldValue = this.get(key);
        this._setNestedValue(this._config, key, value);
        this._notifyListeners(key, value, oldValue);
    }
    
    update(updates) {
        Object.keys(updates).forEach(key => {
            this.set(key, updates[key]);
        });
    }
    
    reset(key) {
        if (key) {
            delete this._config[key];
        } else {
            this._config = {};
        }
    }
    
    onChange(key, callback) {
        if (!this._listeners[key]) {
            this._listeners[key] = [];
        }
        this._listeners[key].push(callback);
    }
    
    _getNestedValue(obj, path, defaultValue) {
        const keys = path.split('.');
        let current = obj;
        
        for (let key of keys) {
            if (current === null || current === undefined || !(key in current)) {
                return defaultValue;
            }
            current = current[key];
        }
        
        return current;
    }
    
    _setNestedValue(obj, path, value) {
        const keys = path.split('.');
        const lastKey = keys.pop();
        let current = obj;
        
        for (let key of keys) {
            if (!(key in current) || typeof current[key] !== 'object') {
                current[key] = {};
            }
            current = current[key];
        }
        
        current[lastKey] = value;
    }
    
    _notifyListeners(key, newValue, oldValue) {
        if (this._listeners[key]) {
            this._listeners[key].forEach(callback => {
                callback(newValue, oldValue, key);
            });
        }
    }
    
    toJSON() {
        return JSON.parse(JSON.stringify(this._config));
    }
    
    fromJSON(json) {
        this._config = JSON.parse(JSON.stringify(json));
    }
}

// Usage
const config = new ConfigManager({
    app: {
        name: "MyApp",
        version: "1.0.0"
    },
    ui: {
        theme: "light",
        language: "en"
    }
});

// Listen for changes
config.onChange('ui.theme', (newTheme, oldTheme) => {
    console.log(`Theme changed from ${oldTheme} to ${newTheme}`);
});

console.log(config.get('app.name'));        // Output: MyApp
console.log(config.get('ui.theme'));        // Output: light
console.log(config.get('nonexistent', 'default')); // Output: default

config.set('ui.theme', 'dark');             // Triggers listener
config.update({
    'app.version': '1.1.0',
    'ui.language': 'es'
});

console.log(config.toJSON());
```

### 🎮 Game Entity System

```javascript
// Component-based entity system
class Entity {
    constructor(id) {
        this.id = id;
        this.components = new Map();
        this.active = true;
    }
    
    addComponent(name, component) {
        this.components.set(name, component);
        return this;
    }
    
    getComponent(name) {
        return this.components.get(name);
    }
    
    hasComponent(name) {
        return this.components.has(name);
    }
    
    removeComponent(name) {
        return this.components.delete(name);
    }
    
    update(deltaTime) {
        if (!this.active) return;
        
        for (let [name, component] of this.components) {
            if (component.update) {
                component.update(deltaTime, this);
            }
        }
    }
}

// Component factories
const Components = {
    Position: (x = 0, y = 0) => ({
        x, y,
        moveTo(newX, newY) {
            this.x = newX;
            this.y = newY;
        }
    }),
    
    Velocity: (vx = 0, vy = 0) => ({
        vx, vy,
        update(deltaTime, entity) {
            const pos = entity.getComponent('position');
            if (pos) {
                pos.x += this.vx * deltaTime;
                pos.y += this.vy * deltaTime;
            }
        }
    }),
    
    Health: (maxHealth = 100) => ({
        current: maxHealth,
        max: maxHealth,
        
        takeDamage(amount) {
            this.current = Math.max(0, this.current - amount);
            return this.current === 0;
        },
        
        heal(amount) {
            this.current = Math.min(this.max, this.current + amount);
        },
        
        getPercentage() {
            return (this.current / this.max) * 100;
        }
    }),
    
    Renderer: (sprite, color = 'blue') => ({
        sprite, color,
        
        render(ctx, entity) {
            const pos = entity.getComponent('position');
            if (pos) {
                ctx.fillStyle = this.color;
                ctx.fillRect(pos.x, pos.y, 32, 32);
            }
        }
    })
};

// Entity factory
function createPlayer(x, y) {
    return new Entity('player')
        .addComponent('position', Components.Position(x, y))
        .addComponent('velocity', Components.Velocity(0, 0))
        .addComponent('health', Components.Health(100))
        .addComponent('renderer', Components.Renderer('player', 'green'));
}

function createEnemy(x, y) {
    return new Entity(`enemy_${Date.now()}`)
        .addComponent('position', Components.Position(x, y))
        .addComponent('velocity', Components.Velocity(-50, 0))
        .addComponent('health', Components.Health(50))
        .addComponent('renderer', Components.Renderer('enemy', 'red'));
}

// Game world
class GameWorld {
    constructor() {
        this.entities = new Map();
    }
    
    addEntity(entity) {
        this.entities.set(entity.id, entity);
    }
    
    removeEntity(id) {
        return this.entities.delete(id);
    }
    
    getEntitiesWithComponent(componentName) {
        const result = [];
        for (let entity of this.entities.values()) {
            if (entity.hasComponent(componentName)) {
                result.push(entity);
            }
        }
        return result;
    }
    
    update(deltaTime) {
        for (let entity of this.entities.values()) {
            entity.update(deltaTime);
        }
    }
    
    render(ctx) {
        const renderableEntities = this.getEntitiesWithComponent('renderer');
        renderableEntities.forEach(entity => {
            const renderer = entity.getComponent('renderer');
            renderer.render(ctx, entity);
        });
    }
}

// Usage
const world = new GameWorld();
const player = createPlayer(100, 100);
const enemy = createEnemy(300, 100);

world.addEntity(player);
world.addEntity(enemy);

// Move player
player.getComponent('velocity').vx = 50;

// Simulate game loop
setInterval(() => {
    world.update(1/60); // 60 FPS
    
    // Check collision, damage, etc.
    const playerPos = player.getComponent('position');
    const enemyPos = enemy.getComponent('position');
    
    if (Math.abs(playerPos.x - enemyPos.x) < 32 && Math.abs(playerPos.y - enemyPos.y) < 32) {
        const playerHealth = player.getComponent('health');
        if (playerHealth.takeDamage(10)) {
            console.log("Player died!");
        }
    }
}, 1000/60);
```

## 💡 Best Practices

### ✅ Object Design Best Practices

```javascript
// ✅ Use meaningful property names
const user = {
    firstName: "John",        // ✅ Clear
    lastName: "Doe",          // ✅ Clear
    emailAddress: "john@example.com"  // ✅ Clear
    // fn: "John",            // ❌ Unclear
    // ln: "Doe",             // ❌ Unclear
    // email: "john@example.com"  // ❌ Could be confusing
};

// ✅ Group related properties
const gameSettings = {
    graphics: {
        resolution: "1920x1080",
        quality: "high",
        vsync: true
    },
    audio: {
        masterVolume: 0.8,
        musicVolume: 0.6,
        sfxVolume: 0.7
    },
    controls: {
        mouseSensitivity: 0.5,
        keyBindings: {
            jump: "Space",
            attack: "LeftClick"
        }
    }
};

// ✅ Use consistent naming conventions
const apiResponse = {
    userId: 123,           // camelCase for properties
    userName: "alice",     // consistent casing
    userEmail: "alice@example.com",
    createdAt: new Date(), // consistent naming pattern
    updatedAt: new Date()
};

// ✅ Validate object structure
function createUser(userData) {
    const required = ['name', 'email'];
    const missing = required.filter(field => !userData[field]);
    
    if (missing.length > 0) {
        throw new Error(`Missing required fields: ${missing.join(', ')}`);
    }
    
    return {
        id: generateId(),
        name: userData.name,
        email: userData.email,
        role: userData.role || 'user',
        createdAt: new Date()
    };
}

// ✅ Use Object.freeze() for constants
const API_ENDPOINTS = Object.freeze({
    USERS: '/api/users',
    PRODUCTS: '/api/products',
    ORDERS: '/api/orders'
});

// ✅ Prefer composition over inheritance
function withLogging(obj) {
    return {
        ...obj,
        log(message) {
            console.log(`[${new Date().toISOString()}] ${message}`);
        }
    };
}

function withValidation(obj, validators) {
    return {
        ...obj,
        validate() {
            return Object.keys(validators).every(key => 
                validators[key](this[key])
            );
        }
    };
}

const validatedUser = withValidation(
    withLogging({ name: "Alice", email: "alice@example.com" }),
    {
        name: name => name && name.length > 0,
        email: email => email && email.includes('@')
    }
);
```

### ⚠️ Common Object Pitfalls

```javascript
// ❌ Modifying objects passed as parameters
function badUpdateUser(user, updates) {
    Object.assign(user, updates); // Mutates original object
    return user;
}

// ✅ Return new object instead
function goodUpdateUser(user, updates) {
    return { ...user, ...updates }; // Creates new object
}

// ❌ Assuming property existence
function badGetUserName(user) {
    return user.profile.name; // Could throw if profile is undefined
}

// ✅ Safe property access
function goodGetUserName(user) {
    return user?.profile?.name || 'Unknown'; // Optional chaining
}

// ❌ Using for...in without hasOwnProperty check
function badIterateProperties(obj) {
    for (let key in obj) {
        console.log(key, obj[key]); // Includes inherited properties
    }
}

// ✅ Check for own properties
function goodIterateProperties(obj) {
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            console.log(key, obj[key]);
        }
    }
}

// ✅ Or use Object.keys()
function betterIterateProperties(obj) {
    Object.keys(obj).forEach(key => {
        console.log(key, obj[key]);
    });
}

// ❌ Comparing objects by reference
const obj1 = { name: "Alice" };
const obj2 = { name: "Alice" };
console.log(obj1 === obj2); // false - different objects

// ✅ Deep comparison function
function deepEqual(obj1, obj2) {
    if (obj1 === obj2) return true;
    
    if (obj1 == null || obj2 == null) return false;
    
    if (typeof obj1 !== 'object' || typeof obj2 !== 'object') {
        return obj1 === obj2;
    }
    
    const keys1 = Object.keys(obj1);
    const keys2 = Object.keys(obj2);
    
    if (keys1.length !== keys2.length) return false;
    
    return keys1.every(key => deepEqual(obj1[key], obj2[key]));
}

console.log(deepEqual(obj1, obj2)); // true - same content
```

---

**Next Chapter**: [🔄 Control Flow Statements](09_Control_Flow_Statements.md)