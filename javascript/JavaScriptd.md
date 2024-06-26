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

![[Pasted image 20240522005015.png]]
 ![[Pasted image 20240522005116.png]]
 ![[Pasted image 20240522005205.png]]
 foreach:
 ![[Pasted image 20240522005504.png]]
 map:
 ![[Pasted image 20240522005636.png]]
 filter:
 ![[Pasted image 20240522005817.png]]
 now just want to see the text section:
 ![[Pasted image 20240522013852.png]]

![[Pasted image 20240522021034.png]]

## Define Function

![[Pasted image 20240522022825.png]]
![[Pasted image 20240522022956.png]]

### Arrow function
![[Pasted image 20240522023203.png]]
![[Pasted image 20240522023415.png]]

object:
![[Pasted image 20240527010956.png]]

![[Pasted image 20240527105752.png]]

![[Pasted image 20240527105849.png]]prototype
![[Pasted image 20240527111316.png]]

define class
