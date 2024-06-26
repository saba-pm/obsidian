// → comment

### JavaScript Data types:
1. string : we can use =="“== for define string 
2. Number
3. Boolean
4. undefined
5. null
6. symbol
typeof "" → for understanding the entire of “” , what is the data type.

```
typeof "saba"   -> 'string'
typeof 43;      ->  'number'
typeof true;    ->  'boolean'
```

### VARIABLE
- if you want to define variable more than one world, you need to use camel case.
1. Let
		its block level scope
		you can do reassign value.
1. Const
		its block level scope
1. var
		Its globally scope. 
if you want to call, you should put `+` in begging of the env :
```
let name = 'saba';

let age= 28;

console.log ('My name is ' +name+' and I am '+age);
```

template string:
```
const hello= `My name is ' ${name} and I am ${age}`;
console.log (hello);
```

env length:

```
const s= 'hello';
console.log(s.length);
console.log(s.toUpperCase());
```

show just the first world and should be uppercase:
```
let name = 'hello world';
console.log(name.substring(0, 5).toUpperCase());
```

split the below string with comma:
```
let name = 'one,two.three,four';
console.log(name.split(','));

```

Array:
```
let numbers = new Array(1,2,3,4,5,6,);
console.log(numbers);


const numbers = ['one', 'two', 3, true];
console.log(numbers);
```

see first the value of array:
```
const numbers = ['one', 'two', 3, true];
console.log(numbers[1]);
```

we can assign value for specific arrays :
```
const numbers = ['one', 'two'];
numbers[2]= 'three';
console.log(numbers);
```

when you don't know the length of the array, but you want to add env to the end of the array, you can use push method:
```
const numbers = ['one', 'two'];
numbers.push('three');
console.log(numbers);
```

now if you want to add at the begging use unshift : 
```
const numbers = ['one', 'two'];
numbers.unshift('zero');
console.log(numbers);
```

remove the last character:  (remove two )
```
const numbers = ['one', 'two'];
numbers.pop();
console.log(numbers);
```

check is it array or not:
```
const numbers = ['one', 'two'];
console.log(Array.isArray(numbers));
console.log(numbers);
```

find the value index number :
```
const numbers = ['one', 'two'];
console.log(numbers.indexOf('two'));
console.log(numbers);
```

### Object
we define an object with `{}`  like this:
```
const person = {

	firstName: 'saba',
	
	lastName: 'pardazi',
	
	age: 28,
	
	// we can define array in object
	
	hobbies: ['music', 'movies', 'sports'],
	
	// we can define another object into the object
	
	address: {
	
		street: 'dovom',
		
		city: 'tehran'
	
		}
	
	  

} 
console.log(person);
```

select specific index we define in object:
```
const person = {
	firstName: 'saba',
	lastName: 'pardazi',
	age: 28,
	// we can define array in object
	hobbies: ['music', 'movies', 'sports'],
	// we can define another object into the object
	address: {
		street: 'dovom',
		city: 'tehran'
		} 
}
console.log(person.hobbies[1]);
//call object in object
console.log(person.address.city);
```
 if you want to call the env simply,  you pull the env:
```
const person = {

	firstName: 'saba',
	lastName: 'pardazi',
	age: 28,
	// we can define array in object
	hobbies: ['music', 'movies', 'sports'],
	// we can define another object into the object
	address: {
		street: 'dovom',
		city: 'tehran'
	}
}

const {firstName, lastName, address:{city}} =person;

console.log(firstName);

console.log(city);
```
add new env in object:
```
const person = {

	firstName: 'saba',
	lastName: 'pardazi',
	age: 28,
	// we can define array in object
	hobbies: ['music', 'movies', 'sports'],
	// we can define another object into the object
	address: {
		street: 'dovom',
		city: 'tehran'
	}
}
person.email = saba@gmail.com
console.log(person);
```

define array but each index is object:
```
const test = [
	{
	id: 1,
	text: 'first'
	},
	{
	id: 2,
	text: 'second'
	},
	{
	id: 3,
	text: 'tird'
	}
]
console.log(test);
```

we can see out put in json format:
```
const testJson = JSON.stringify(test);
console.log(testJson);
```

## Loops
 **For**
need parameters:
 1. first is going to assignment of the iterator 
 2. condition
 3.  increment

 **While** 
we define variable out side of the loop

```
// For loop example
for (let i = 0; i <= 10; i++) { // Initialize i to 0, run the loop as long as i is less than or equal to 10, and increment i by 1 after each iteration
    console.log(`For Loop Number: ${i}`); // Log the current value of i to the console
}

// While loop example
let i = 0; // Initialize i to 0
while (i < 10) { // Run the loop as long as i is less than 10
    console.log(`While Loop Number: ${i}`); // Log the current value of i to the console
    i++; // Increment i by 1 after each iteration
}

```

- **For Loop**:
    
    - **Initialization**: `let i = 0` sets the starting value of the loop counter `i` to 0.
    - **Condition**: `i <= 10` is checked before each iteration of the loop. If the condition is `true`, the loop body is executed. If `false`, the loop stops.
    - **Increment**: `i++` increases the value of `i` by 1 after each iteration.
    - **Body**: `console.log(\`For Loop Number: ${i}`)`prints the current value of`i` to the console.
- **While Loop**:
    
    - **Initialization**: `let i = 0` sets the starting value of the loop counter `i` to 0.
    - **Condition**: `i < 10` is checked before each iteration of the loop. If the condition is `true`, the loop body is executed. If `false`, the loop stops.
    - **Body**: `console.log(\`While Loop Number: ${i}`)`prints the current value of`i` to the console.

```
// Define an array of todo objects
const todos = [
    {
        id: 1, // Unique identifier for the first todo item
        text: 'Take out trash', // Description of the first todo item
        isCompleted: true // Indicates if the first todo item is completed
    },
    {
        id: 2, // Unique identifier for the second todo item
        text: 'Meeting with boss', // Description of the second todo item
        isCompleted: true // Indicates if the second todo item is completed
    },
    {
        id: 3, // Unique identifier for the third todo item
        text: 'Dentist appt', // Description of the third todo item
        isCompleted: false // Indicates if the third todo item is completed
    }
];

// Iterate through the todos array using a for loop
for (let i = 0; i < todos.length; i++) { // Initialize i to 0, run the loop as long as i is less than the length of the todos array, and increment i by 1 after each iteration
    console.log(`For Loop Number: ${i}`); // Log the current value of i to the console
}

```

- **Array of Objects**:
    
    - The `todos` array contains three objects, each representing a todo item with properties `id`, `text`, and `isCompleted`.
    - Each object has a unique `id`, a `text` field describing the task, and an `isCompleted` field indicating whether the task is done.
- **For Loop**:
    
    - **Initialization**: `let i = 0` sets the starting value of the loop counter `i` to 0.
    - **Condition**: `i < todos.length` ensures the loop runs as long as `i` is less than the length of the `todos` array. Since there are three items, the loop will run three times.
    - **Increment**: `i++` increases the value of `i` by 1 after each iteration.
    - **Body**: `console.log(\`For Loop Number: ${i}`)`prints the current value of`i` to the console, showing the iteration number.

```
// Define an array of to-do items, each represented as an object with properties: id, text, and isCompleted
const todos = [
    {
        id: 1, // Unique identifier for the first to-do item
        text: 'Take out trash', // Description of the to-do item
        isCompleted: true // Boolean indicating if the to-do item is completed
    },
    {
        id: 2, // Unique identifier for the second to-do item
        text: 'Meeting with boss', // Description of the to-do item
        isCompleted: true // Boolean indicating if the to-do item is completed
    },
    {
        id: 3, // Unique identifier for the third to-do item
        text: 'Dentist appt', // Description of the to-do item
        isCompleted: false // Boolean indicating if the to-do item is completed
    }
];

// Loop through each to-do item in the todos array
for (let todo of todos) {
    // Log the text property of each to-do item to the console
    console.log(todo.text);
}

```

1. **Array Definition:**
    - `const todos = [...]`: Defines a constant array named `todos` which contains three objects. Each object represents a to-do item with three properties: `id`, `text`, and `isCompleted`.
2. **Object Properties:**
    - `id`: A unique identifier for each to-do item.
    - `text`: A string describing the to-do item.
    - `isCompleted`: A boolean value indicating whether the to-do item is completed (`true`) or not (`false`).
3. **Loop Through Array:**
    - `for (let todo of todos) {...}`: A `for...of` loop that iterates over each object in the `todos` array.
    - `console.log(todo.text);`: Logs the `text` property of each to-do item to the console. This will output:
        - "Take out trash"
        - "Meeting with boss"
        - "Dentist appt"

This code snippet effectively logs the description of each to-do item in the `todos` array to the console.

 foreach:
```
const todos = [
    {
        id: 1,
        text: 'Take out trash',
        isCompleted: true
    },
    {
        id: 2,
        text: 'Meeting with boss',
        isCompleted: true
    },
    {
        id: 3,
        text: 'Dentist appt',
        isCompleted: false
    }
];

// forEach, map, filter
todos.forEach(function(todo) {
    console.log(todo.text);
});

```

- **Array Definition:** Defines an array `todos` with three objects.
- **forEach Method:** The `forEach` method executes a provided function once for each array element.
    - `todos.forEach(function(todo) {...});`: Iterates over each `todo` in the `todos` array.
    - `console.log(todo.text);`: Logs the `text` property of each `todo` to the console.

 map:
 ```
 const todos = [
    {
        id: 1,
        text: 'Take out trash',
        isCompleted: true
    },
    {
        id: 2,
        text: 'Meeting with boss',
        isCompleted: true
    },
    {
        id: 3,
        text: 'Dentist appt',
        isCompleted: false
    }
];

// forEach, map, filter
const todoText = todos.map(function(todo) {
    return todo.text;
});
console.log(todoText);

```

- **Array Definition:** Same as above.
- **map Method:** The `map` method creates a new array populated with the results of calling a provided function on every element in the calling array.
    - `const todoText = todos.map(function(todo) {...});`: Creates a new array `todoText` containing the `text` property of each `todo` in the `todos` array.
    - `return todo.text;`: Returns the `text` property of each `todo`.
    - `console.log(todoText);`: Logs the new array `todoText` to the console. Output: `["Take out trash", "Meeting with boss", "Dentist appt"]`.


 filter:
```
const todos = [
    {
        id: 1,
        text: 'Take out trash',
        isCompleted: true
    },
    {
        id: 2,
        text: 'Meeting with boss',
        isCompleted: true
    },
    {
        id: 3,
        text: 'Dentist appt',
        isCompleted: false
    }
];

// forEach, map, filter
const todoCompleted = todos.filter(function(todo) {
    return todo.isCompleted === true;
});
console.log(todoCompleted);

```

- **Array Definition:** Same as above.
- **filter Method:** The `filter` method creates a new array with all elements that pass the test implemented by the provided function.
    - `const todoCompleted = todos.filter(function(todo) {...});`: Creates a new array `todoCompleted` containing only the `todo` objects where `isCompleted` is `true`.
    - `return todo.isCompleted === true;`: Returns `true` if `isCompleted` is `true`, otherwise returns `false`.
    - `console.log(todoCompleted);`: Logs the new array `todoCompleted` to the console. Output: `[ { id: 1, text: 'Take out trash', isCompleted: true }, { id: 2, text: 'Meeting with boss', isCompleted: true } ]`.

These methods (`forEach`, `map`, `filter`) are commonly used to iterate over arrays and perform operations on their elements in JavaScript.


### Filter and Map Combination:
 ```
 const todos = [
    {
        id: 1,
        text: 'Take out trash',
        isCompleted: true
    },
    {
        id: 2,
        text: 'Meeting with boss',
        isCompleted: true
    },
    {
        id: 3,
        text: 'Dentist appt',
        isCompleted: false
    }
];

// Filter the todos to only include completed tasks, then map to get the text of those tasks
const todoCompleted = todos.filter(function(todo) {
    return todo.isCompleted === true;
}).map(function(todo) {
    return todo.text;
});

console.log(todoCompleted);

```

- **Array Definition:** Defines an array `todos` with three objects.
- **filter Method:** Filters the `todos` array to include only the objects where `isCompleted` is `true`.
- **map Method:** Maps the filtered array to a new array containing only the `text` property of each object.
- **console.log(todoCompleted);**: Logs the resulting array to the console. Output: `["Take out trash", "Meeting with boss"]`.


### Ternary Operator and Switch Statement:

```
const x = 11;

// Use a ternary operator to set the color based on the value of x
const color = x > 10 ? 'red' : 'blue';

switch(color) {
    case 'red':
        console.log('color is red');
        break;
    case 'blue':
        console.log('color is blue');
        break;
    default:
        console.log('color is NOT red or blue');
        break;
}

```

- **Ternary Operator:**
    - `const color = x > 10 ? 'red' : 'blue';`: Uses a ternary operator to set the value of `color` to `'red'` if `x` is greater than 10, otherwise sets it to `'blue'`.
- **Switch Statement:**
    - `switch(color) {...}`: Checks the value of `color` and executes the corresponding `case` block.
    - `case 'red': console.log('color is red'); break;`: Logs "color is red" if `color` is `'red'`.
    - `case 'blue': console.log('color is blue'); break;`: Logs "color is blue" if `color` is `'blue'`.
    - `default: console.log('color is NOT red or blue'); break;`: Logs "color is NOT red or blue" if `color` is neither `'red'` nor `'blue'`.
## Define Function

First Code Block:

```
// Define a function named addNums that takes two parameters: num1 and num2
function addNums(num1, num2) {
    // Log the sum of num1 and num2 to the console
    console.log(num1 + num2);
}

// Call the addNums function with arguments 5 and 4
addNums(5, 4); // Output: 9

```

Second Code Block:
```
// Define a function named addNums that takes two parameters: num1 and num2
// Set default values for num1 and num2 to 1
function addNums(num1 = 1, num2 = 1) {
    // Return the sum of num1 and num2
    return num1 + num2;
}

// Call the addNums function with arguments 5 and 5 and log the result to the console
console.log(addNums(5, 5)); // Output: 10

```

1. **First Code Block:**
    
    - The `addNums` function is defined to accept two parameters, `num1` and `num2`.
    - Inside the function, it logs the sum of `num1` and `num2` to the console using `console.log(num1 + num2)`.
    - The function is called with the arguments `5` and `4`, so it logs `9` to the console.
2. **Second Code Block:**
    
    - The `addNums` function is redefined to accept two parameters, `num1` and `num2`, with default values of `1`.
    - Instead of logging the sum, it returns the sum of `num1` and `num2`.
    - The function is called with the arguments `5` and `5`, and the result is logged to the console using `console.log(addNums(5, 5))`, which logs `10`.

In both examples, the main difference is how the result is handled: the first example logs it directly within the function, while the second example returns the result to be logged outside the function.


### Arrow function

**First Code Block:**
```
// Define a constant named addNums and assign it an arrow function
// The arrow function takes two parameters, num1 and num2, with default values of 1
const addNums = (num1 = 1, num2 = 1) => {
    // Return the sum of num1 and num2
    return num1 + num2;
}

// Call the addNums function with arguments 5 and 5 and log the result to the console
console.log(addNums(5, 5)); // Output: 10

```

**Second Code Block:**
```
// Define a constant named addNums and assign it an arrow function
// The arrow function takes two parameters, num1 and num2, with default values of 1
// It directly returns the sum of num1 and num2 (implicit return)
const addNums = (num1 = 1, num2 = 1) => num1 + num2;

// Call the addNums function with arguments 5 and 5 and log the result to the console
console.log(addNums(5, 5)); // Output: 10

```

1. **First Code Block:**
    
    - A constant named `addNums` is defined and assigned an arrow function.
    - The arrow function takes two parameters, `num1` and `num2`, with default values of `1`.
    - Inside the function body, it explicitly returns the sum of `num1` and `num2`.
    - The function is called with the arguments `5` and `5`, and the result is logged to the console using `console.log(addNums(5, 5))`, which logs `10`.
2. **Second Code Block:**
    
    - Similar to the first code block, a constant named `addNums` is defined and assigned an arrow function.
    - The arrow function takes two parameters, `num1` and `num2`, with default values of `1`.
    - This time, the function directly returns the sum of `num1` and `num2` without using a return statement (implicit return).
    - The function is called with the arguments `5` and `5`, and the result is logged to the console using `console.log(addNums(5, 5))`, which logs `10`.

In both examples, the main difference is the usage of an explicit return in the first example and an implicit return in the second example.


#### Object

### Step 1: Basic Constructor Function

```
// Constructor function to create Person objects
function Person(firstName, lastName, dob) {
    this.firstName = firstName; // Assign firstName parameter to the object property
    this.lastName = lastName; // Assign lastName parameter to the object property
    this.dob = dob; // Assign dob parameter to the object property
}

// Instantiate a new Person object
const person1 = new Person('John', 'Doe', '4-3-1980');

// Log the created object to the console
console.log(person1);

```

- The `Person` function is a constructor function used to create new objects.
- `this.firstName`, `this.lastName`, and `this.dob` assign the function's parameters to properties of the object.
- `person1` is a new instance of `Person`, created with specific values.
- `console.log(person1)` prints the `person1` object, showing its properties.

### Step 2: Adding a Method to Get Birth Year

```
// Constructor function to create Person objects
function Person(firstName, lastName, dob) {
    this.firstName = firstName; // Assign firstName parameter to the object property
    this.lastName = lastName; // Assign lastName parameter to the object property
    this.dob = new Date(dob); // Convert dob string to a Date object

    // Method to get the birth year
    this.getBirthYear = function() {
        return this.dob.getFullYear(); // Return the year of the date of birth
    };
}

// Instantiate new Person objects
const person1 = new Person('John', 'Doe', '4-3-1980');
const person2 = new Person('Mary', 'Smith', '3-6-1970');

// Log the birth year of person1 to the console
console.log(person1.getBirthYear());

```

- The `dob` parameter is converted to a Date object.
- `getBirthYear` is a method that returns the birth year by calling `getFullYear` on the Date object.
- `console.log(person1.getBirthYear())` prints the birth year of `person1`.

### Step 3: Adding Another Method to Get Full Name

```
// Constructor function to create Person objects
function Person(firstName, lastName, dob) {
    this.firstName = firstName; // Assign firstName parameter to the object property
    this.lastName = lastName; // Assign lastName parameter to the object property
    this.dob = new Date(dob); // Convert dob string to a Date object

    // Method to get the birth year
    this.getBirthYear = function() {
        return this.dob.getFullYear(); // Return the year of the date of birth
    };

    // Method to get the full name
    this.getFullName = function() {
        return `${this.firstName} ${this.lastName}`; // Return the full name as a string
    };
}

// Instantiate new Person objects
const person1 = new Person('John', 'Doe', '4-3-1980');
const person2 = new Person('Mary', 'Smith', '3-6-1970');

// Log the birth year and full name of person1 to the console
console.log(person1.getBirthYear());
console.log(person1.getFullName());

```

- `getFullName` is a new method that returns the full name by concatenating `firstName` and `lastName`.
- `console.log(person1.getFullName())` prints the full name of `person1`.

### Summary of Each Step in the Screenshots:

1. **First Screenshot (Top):**
    
    - Basic constructor function with `firstName`, `lastName`, and `dob` properties.
    - Instantiates `person1` and logs it to the console.
2. **Second Screenshot (Middle):**
    
    - Adds the `getBirthYear` method to return the birth year.
    - Instantiates `person1` and `person2`, then logs the birth year of `person1`.
3. **Third Screenshot (Bottom):**
    
    - Adds the `getFullName` method to return the full name.
    - Logs the birth year and full name of `person1`.


prototype
```
// Constructor function to create Person objects
function Person(firstName, lastName, dob) {
    this.firstName = firstName; // Assign firstName parameter to the object property
    this.lastName = lastName; // Assign lastName parameter to the object property
    this.dob = new Date(dob); // Convert dob string to a Date object
}

// Adding getBirthYear method to the Person prototype
Person.prototype.getBirthYear = function() {
    return this.dob.getFullYear(); // Return the year of the date of birth
};

// Adding getFullName method to the Person prototype
Person.prototype.getFullName = function() {
    return `${this.firstName} ${this.lastName}`; // Return the full name as a string
};

// Instantiate new Person objects
const person1 = new Person('John', 'Doe', '4-3-1980');
const person2 = new Person('Mary', 'Smith', '3-6-1970');

// Log the full name of person2 to the console
console.log(person2.getFullName());

// Log the person1 object to the console
console.log(person1);

```

1. **Constructor Function (`Person`)**:
    
    - The `Person` function is defined to act as a constructor. It takes `firstName`, `lastName`, and `dob` (date of birth) as parameters.
    - Inside the constructor, `this.firstName`, `this.lastName`, and `this.dob` are set to the provided parameters.
    - `this.dob` is converted to a `Date` object for further date manipulations.
2. **Prototype Methods**:
    
    - `Person.prototype.getBirthYear`: This method is added to the `Person` prototype. It returns the year of birth by calling `getFullYear()` on the `dob` Date object.
    - `Person.prototype.getFullName`: This method is also added to the `Person` prototype. It returns the full name by concatenating `firstName` and `lastName`.
3. **Instantiating Objects**:
    
    - Two instances of the `Person` class are created: `person1` and `person2`.
    - `person1` is created with the values `'John'`, `'Doe'`, and `'4-3-1980'`.
    - `person2` is created with the values `'Mary'`, `'Smith'`, and `'3-6-1970'`.
4. **Logging Information**:
    
    - `console.log(person2.getFullName())` prints the full name of `person2` to the console. It outputs: `Mary Smith`.
    - `console.log(person1)` prints the `person1` object to the console, showing its properties and prototype methods.

### Benefits of Using Prototypes:

- **Memory Efficiency**: Methods defined on the prototype are shared among all instances of the constructor, rather than each instance having its own copy of the method. This makes the code more memory-efficient.
- **Code Organization**: Placing methods on the prototype separates the object's properties from its methods, making the code easier to manage and read.

In the provided screenshot, the `person1` object is expanded in the console, showing its properties (`firstName`, `lastName`, `dob`) and prototype methods (`getBirthYear`, `getFullName`) under `__proto__`. This demonstrates how prototype methods are associated with the object.

define class
