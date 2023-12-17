# TypeScript notes


## Development Environment


### Installing

```
npm i -g typescript
```

verify by checking version.

```
tsc -v
```


## Configuring the TypeScript Compiler


Creating the configuration file

```
tsc --init
```

### Edit configs 

In the tsconfig.json file. change target

```json
"strict": true
// configurations
"target": "ES2016	// Specifiying the version of javascript to generate.
// configurations
"rootDir": "./src"	// Set root directory to src folder
// configurations
"outDir": "./dist",	// Set javascript files to be compiled to dist folder
"removeComments": true, // Don't copy the typescript comments to javascript
"noEmitOneError": true, // Only generate javascript when there's no error
```

Now we can compile code like this.

```
tsc
```

## Writing Typescript

### A Hello world

In index.ts

```typescript
console.log('Hello World');
```

Comple down to javascript.

```
tsc index.ts
```


## Data Types


### Primitive types

```typescript
let sales: number = 123456789;
let newsales: number = 123_456_789;
let percent: number = 2.358;
let course: string = 'TypeScript';
let is_published: boolean = true;
```

### The any Type

a type that can be any type of variable.However you're advised not to use it as it defeats the purpose of typescript.

```typescript
let level;

level = 1;
level = 'a';

function render(document: any){
	console.log(document); 
}
```

### Arrays

```typescript
let numbers: number[] = [];
let words: string[] = [];
```

### Tuples

Fixed length array

```typescript
let user: [number, string] = [1, 'Mosh'];
```

### Enums

A built in type. A list of related constants.

```typescripts
const enum Size { Small = 1, Medium = 2, Large = 3 };

let mySize: Size = Size.Medium;

console.log(mysize)
```

Output

```
2
```

### Functions

```typescript
// taxYear has a default value
function calculateTax(income: number, taxYear = 2022): number {		// Return type of number
	if (income < 50000){
		return income * 1.2;
	}
	return income * 1.3;
}
```

Some configs to inable in the config file for better function writing

```json
//configs
"noUnusedLocals": true,
"noUnusedParameters": true,
"noImplicitReturns": true,
//configs
```

### Objects

```typescript
let employee: {
	readonly id: number,			// id can't be changed/modified
	name: string
// Defining signature of retire Method (Date is a date object)
	retire: (date: Date) => void	// Retire method
} =  { 
		id: 1, 
		name: 'Brian' 
		retire: (date: Date) => {
			console.log(date);
		}
	};
```


## Advanced Types


### Type aliases

Is used to create a custom type.In the following example we'll make an Employee type for making Employee objects

```typescript
type Employee = {	
	readonly id: number,			
	name: string
	retire: (date: Date) => void	
}

let JuniorBackend: Employee = {
	id: 1,
	name:, 'Jhonathon',
	retire: (date: Date) => {
		console.log(date);
	}
};
```

### Unions Types 

Union Types: Used to give a variable or function parameter more than one type.

```typescript
function kgToLbs(weight: number | String): number {
	// Narrowing
	if ( typeof weight === 'number')
		return weight * 2.2;
	else
		return parseINt(weight) * 2.2;	
}

kgToLbs(10);
kgToLbs('10kg');
```

### Intersection Types

Inersection types: Used to define objects that are two types at once

```typescript
type Draggable = {
 drag: () => void
}

type Resizable = {
	resize: () => void
}

type UIWidget = Draggable && Resizable

let textBox = UIWidget = {
	drag: () => {},
	resize: () => {}
}
```

### Literal Types

Used to limit variables to exact or specific values

```typescript
type Quantity = 50 | 100;

let quantity: Quantity = 50;
```

### Nullable Types

Allows to pass the null type into a function

```typescript
function greet(name: string | null){
 	if(name)
		console.log(name.toUpperCase());
	else
		console.log('Hola!');
}

greet(null);
```

### Optional Chaining

```typescript
type Customer = {
 birthday: Date
}

function getCustomer(id: number): Customer | null | undefined {
	if(id === 0){
		return null
	}else{
		let newCustomer = { birthday: new Date() };
		return newCustomer
	}
}

let customer = getCustomer(0);

// Usint the opional property access operator(?.) to replace the if statement
// if ( customer !== null && customer !== undefined)
 console.log(customer?.birthday)

// Optional element access operator
// customer?.[0]

// Optional call 
let log: any = null;
log?.('a');					
```
