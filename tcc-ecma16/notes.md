## ECMA 2016

### Classes

 - explicit "constructor" function for instancing
 - no pre-definition usage
   - you have to define the class a-la C requirements, but in completion
 - uses `super` syntax
 - supports `static` methods
 - (op-ed) still no typed arguments...
 - Ctor supports **default parameters**

### Arrow Functions
  ```js
    var animalStrings = this.animals.map(a => a.toString());
  ```
  #### Syntax
  1. arguments
  2. `=>` (arrow declaration)
  3. expression


  #### Features

  - Has implicit lexical "this" based on context
  - replaces `.bind(this)`
    - (op-ed) `var self = this;` is apparently "old"!
  -  binds to container scope, works with nested classes

### Template Literals
  - uses backticks &amp; JSP syntax for variable accessors.

### Spread Operator
  - replaces `.apply(array)`
  ```js
    var obj = {
      function doSingleOperation(arg1, arg2, arg3){
        return arg1 + arg2 + arg3
      }
    }
    var listOfVariables = [ 1, 2, 3]
    obj.doSingleOperation(...listOfVariables) // == 6
  ```

### Destructuring Assignment

 - maps an array to variables from idx 0

```js
var amounts = [1 ,2 ,3]

var [year1, year2, year3] = amounts;

```

### `let` (The New `var`)

  - designed to supplant var in conjunction with `const`
  - Built to explicitly ignore "hoisting"
    - Hoisting: `var`s are moved to the top of the highest defined scope (functions, files etc)
    - Defined well before they're initialized
  - `let` is scoped to the nearest curly brace (a la most languages)

### `const`
  - Read the tin.

### `Object.assign()`
  - *finally* a merge function
  - left-to-right assign.
  - Right wins the  doubly defined assignment case
  - arg0 is the resultant

### Iterators &amp; Generators
  - defined by `function* foo` or `function *foo`
  - Returns an iterator.
  - uses `yield` keyword with argument to return a value
  - accessed with `.next().value`
```js
  let balanceCalculator;
  document.getElementById('calculateBalance').style.display = 'none';

  function* balance(initialDeposit = 500){
  const INTEREST_RATE = .001;
  let balance = initialDeposit;
  yield balance;
  while(true){
      balance *= (1 + INTEREST_RATE);
      balance = balance.toFixed(2);
      yield balance;
    }
  }

  function createAccount(){
     let initialDeposit = parseFloat(document.getElementById('deposit').value);
     balanceCalculator = balance(initialDeposit);
     document.getElementById('result').innerHTML = `Account created $${balanceCalculator.next().value}`;
     document.getElementById('initialForm').style.display = 'none';
     document.getElementById('calculateBalance').style.display = 'block';
  }

   function calculateBalance(){
   let newBalance = balanceCalculator.next().value;
   document.getElementById('result').innerHTML +=  `<br/>${newBalance}`;
  }
```


### `for .. of` syntax
- uses a generator to iterate
- variable bound in statement is the result of `.next().value`

### Set
- "Array-like" object.
- No duplicates
