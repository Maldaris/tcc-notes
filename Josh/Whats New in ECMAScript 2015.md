- Not updated in 10 years, cause fuck you.
- Slideshare: [Link](http://goo.gl/BfkdZ6)

# Class
- Finaly a formal class syntax
- Note, everything is essentially public

```js
class Animal {
    constructor(name) {
        this.name = name;
        this.birthday = new Date();
    }

    get age() {
        return new Date() - this.birthday;
    }

    toString() {
        return this.name + " born on " + this.birthday;
    }
}

```
- Inheritance 

```js
class Cat extends Animal {
    constructor(name) {
        super(name);
        this._lives = 9;
    }

    get lives() {
        return this._lives;
    }

    set lives(numberOfLives) {
        if(numberOfLives > this._lives || numberOfLives < 0) {
            throw new Error("Invalid number of lives")
        }
        else {
            this._lives = numberOfLives
        }
    }

    toString() {
        return super.toString() + " has " + this._lives + " lives.";
    }
}
```

- Static
```js
class Animal {
    constructor(name) {
        this.name = name;
        this.birthday = new Date();
    }

    get age() {
        return new Date() - this.birthday;
    }

    toString() {
        return this.name + " born on " + this.birthday;
    }

    static oldest(animal, animal2) {
        if(!(animal instanceof Animal || animal2 instanceof Animal)
        {
            throw new Error("paramaters must be instances of Animal");
        }
        else {
            return animal.age > animal2.age ? animal : animal2;
        }
    }
}
```

- Default parameters
```js
class Animal {
    constructor(name = 'Albert') {
        this.name = name;
        this.birthday = new Date();
    }

    get age() {
        return new Date() - this.birthday;
    }

    toString() {
        return this.name + " born on " + this.birthday;
    }
}

```

# Arrow functions
- Mostly syntactic sugar
- Like C# lambda

```js
var animalStrings + this.animals.map(a => a.toString());
```

- Implicitly bound to the context in which they are defined

```js
class Animal {
    construct(name = "Albert", millisendsPerYear = 1000) {
        this.years = 0;
        this.name = name;
        window.setInterval( () => {
            this.years++;
        }, millisecondsPerYear); // Normal window.setInterval would set "this" to the window in the function, but using arrow it is bound to Animal
    }
}
```

# Template Literals
- Allows you to refer to variables inside of a string

Old:
```js
toString() {
    return this.name + ' is ' + this.age + ' years old.'
}
```

New:
```js
toString() {
    return `${this.name} is ${this.age} years old.'
}
```

# Spread Operator
- Allows you to split an array into multiple parameters

```js
function calculateTotalCost(ammount1, ammount2, ammount3) {
    return ammount1 + ammount2 + ammount3;
}

var temp = {10,23,61};
calculateTotalCost(...temp);
```

# Destructuring Assigment

- With an array:
```js
function calculateTotalCost(ammounts) {
    var {year1,year2,year3} = ammounts;
    // Can now access the variables in ammounts as year1,year2,year3
    return year1 + year2 + year3;
}
```

- With an object:
```js
var client = {"name":"Albert","total":400}
var {name,total} = client;
// Can now access client.name and client.total from name and total variables
```

# Let
- The new var!
- var is weird.

```js
function old() {
    y = 5;
    var y;
    for( var x = 0; x < 2; x+) {}
    if(true) {
        var z = '100'
    }
    return y + " " + x + " " + z;
}
```

- This works because of hoisting, all variables are actually defined at the top of the function no matter where you put it

```js
function new() {
    y = 5;
    let y;
    for(let x = 0; x < 2; x++) {}
    if(true) {
        let z = '100'
    }
    return y + " " + x + " " + z; // Throws uncaught exception!! Let scopes like normal languages.
    // Note, in switch statements the whole switch is the scope not each case.
}
```

#const 
- Exactly what you think.

# Object.assign
- Use to merge multiple objects into one
- If the same property is defined in two paramaters, right most value wins
- Very first parameter is what you are merging into, usually uses an empty object

# Iterators and Generators
- Generator is a function that has an astric either as first character of func name or right after word function
    - Allows pausing and resuming
    - Returns an iterator
- Iterators have one function, next, which returns the next value of the generator.

```js
function balance(initialDeposit = 500) {
    const INTEREST_RATE = .001;
    let balance = initialDeposit;
    yield balance;
    while(true) {
        balance *= (1 + INTEREST_RATE);
        balance = balance.toFixed(2); // Fix to 2 decimal places
        yield balance;
    }
}

let balanceCalculator = balance(100);
console.log("Account created: " + balanceCalculator.next().value)
let x = 10;
while(x > 0) {
    console.log(`${x}`)
    x--;
}
let months = 10;
for(let b of balanceCalculator) {
    ++months;
    if (b > 5000) {
        console.log(`Goal hit after ${months} months");
    }
}
```

# Set
- like an array but only unique values

```js
let ids = new Set(); // Create empty set
let names = new Set(prepopulatedNames); // Create using an array, will auto remove dupes.

// add 
ids.add(100);

// remove
ids.delete(100);

// has
ids.has(100);
```

# WeakMap
- Key value pairs where keys are objects
- Also map

# Symbols
- Could force in a property, but if another dev adds property in actually implmentation problems happen
- Symbols ensure there is a unique name

```js
let buyers = Symbols("buyers");
obj[buyers] = {"Buyer1","Buyer2"}
```

# Modules
- Finally built in "requires"

```js
// Utilities.js
export default class Utilities {
    static log(message) {
        console.log(message);
    }
}

// CommonFunctions.js
import Utilities from './Utilities.js'

export logFakeError() {
    Utilities.log(repeat("error"));
}

export function logFakeMessage() {
    Utilities.log("message");
}

function repeat(msg) {
    return `${msg} ${msg} ${msg}`
}


// main.js
import {logFakeError, logFakeMessage as log} from './CommonFunctions.js'
log() // message message message
logFakeError() // error error error
```

# Use in production?
- No browsers support all features
- Use a JS transpiler
    - Translates ES6 to ES5 so all browsers support it
    - [Babel](https://babeljs.io/)
- Use a module bundler
    - support CommonJS modules instead of native
    - Browserify + babelify = use imports and bundle
- Polyfills
    - adds 'native' functionality that isn't actually in browsers
    - search for feature, there is usually a polyfill on mdn if you need it 