# TypeScript Guide

# 0. Table of contents

# 1. First Steps

## 1.1. Installation

For installing the TS compiler, we run the following

```powershell
npm install -g typescript
```

## 1.2. Compilation

In order to compile the TS code, we run the following command

```powershell
tsc filename.ts
```

If we want to compile ALL the TS files inside our current dir. we simply execute:

```json
tsc
```

## 1.3. Execution

For executing the .js code generated from the compilation, we just simply run:

```powershell
node filename.js  # We use nodeJS to execute local JS files
```

## 1.4. Configuration file

For simplifying compilation, we create a new file named  as: ***tsconfig.json***

```json
// Inside tsconfig.json
{
	"compilerOptions": 
		{
			"target": "ES6",  // JS we'll compile to, nowadays it is recommended to use ES6
			"outDir": "build",  // Folder where the compiled files will be placed 
			"noEmitOnError": true;  // If error, no need to create the JS file
		}
}
```

# 2. Variables

## 2.1. Types by Inference

Setting a variable value by inference means that the variable type depends on the value we have initialized it with. Example:

```tsx
var example = 2;  // Variable of type number
var example2 = "hello World";  // Variable of type string
var example3 = true;  // Variable of type boolean
// or
var example3: any = true;  // Same as the above example
```

But if we modify the value of a variable already initialized with a different type, we’ll get an error as TypeScript does not permit changing types within the same variable.

```tsx
var example = 2;  // Variable of type int
var example = "hello World";  // ERROR: we already initialized the var. with number type
```

## 2.2. Types

But as it might seem, is a way better approach to type the variables directly from the beggining as we’ll control all the assigned types and values.

### 2.2.1. Boolean

```tsx
let booleanExample: boolean;

// We can also initialize the cariable with a certain value at start
let booleanExample: boolean = true;

// And then modify it as follows
booleanExample = false;
```

### 2.2.2 Number

Numbers in TypeScript (as in JS) are either **floating point values** or **BigIntegers**. These **floating point numbers** get the type ***number***, while **BigIntegers** get the type ***bignint**.*

**Number**
JavaScript does not have a special runtime value for integers, so there’s no equivalent to ***int*** or *float*; everything is simply *number*.

```tsx
let numberExampleDecimal: number = 10;  // Number in decimal base
let numberExampleHexadecimal: number = 0xA;  // Number in decimal base
let numberExampleBinary: number = 0b1010;  // Number in decimal base
let numberExampleOctal: number = 0o12;  // Number in decimal base
```

**BigIntegers**
They are slow and only recommended when surpassed range of Number.MAX_SAFE_INTEGER [-*9007199254740991,* *9007199254740991].*

```tsx
let bigInteger: bigint = 100n;
```

### 2.2.3. String

We can use both [“”] and [‘’] to surround string data.

```tsx
let stringName: string = 'charly';
stringName = "carlos";
```

**********Concatenate Strings**********

```tsx
let stringName: string = 'charly';
let stringSurName: string = 'charly';

let stringCompleteName: string = '${stringName} ${stringSurname}'

// As result we will obtain 'name surname' string as the value of stringCompleteName
```

### 2.2.4. Arrays

************************Number Array************************
Create a number of ONLY numbers

```tsx
let numbers0: number[] = [1, 2, 3];  // If any of the values is not a number -> ERROR
// A different way to create a number array
let numbers1: Array<number> = [1, 2, 3];
```

************************String Array************************

```tsx
let numbers0: string[] = ["1", "2", "3"];
// or
let numbers1: Array<string> = ["1", "2", "3"];
```

******************Any Array******************
This kind of array can contain whatever elements inside independently of their type.
Using `any` disables all further type checking, and it is assumed; also, by not specifying any type, TS will asume it is 'any' -> noImplicitAny

```tsx
let obj: any = { x: 0 };
// or
let obj: {x:0};
```

### 2.2.5. Tuples

<aside>
📝 Note: tuples are array of 2 elements

</aside>

```tsx
let places: [number, string] = [1201230, "calle Alcalá"];
```

### 2.2.6. Enum

Better numeric representations.

```tsx
enum States  // Autoincremental order of values
{
	On,  // Asigned to 0 
	Off,  // Asigned to 1
	Undefined  // Asigned to 2
}

let state: States = States.On;  // State is of type 'States', with value 0 (On)
console.log(stat);  // Will print value of On -> 0
```

We can also assign specific values to our enums:

```tsx
enum States  // Number specified by us
{
	On = 1,
	Off = -4,
	Undefined = 0
}
```

### 2.2.7. Unknown

With unknown values we can reuse the type of the variable we are using. Not recommended.

```tsx
let withoutType: unknown = "string";
withOutType = 10;
withOutType = true;
```

<aside>
📝 *******Unknown******* type variables cannot be assigned to other variables of type string or number.
Instead, use type ***any*** variables.

</aside>

### 2.2.8. Void

Used in functions in order to return nothing.

```tsx
function consoleLog: void ()
{
	console.log('This function does not return nothing');
}
```

# 3. Interfaces

Used to define rules/methods/functions which all variables from that interface need to follow/implement, summarizing it is useful to organize our code an to know exactly what parameters we are using.

```tsx
interface Human
{
	name: string;
	surname: string;
	age: number;
}

// Lets use above defined interface inside a function
// passing objects that need to follow 'human' interface (have name, surname, age)
function showHuman (humanInt: Human) 
{
	console.log(humanInt);	
}

showHuman({name: 'Carlos', surname: 'Iborra', age: 100});
```

**************************************Optional properties**************************************

```tsx
interface Human
{
	name: string;
	surname: string;
	age?: number;  // ? indicates it is an optional parameter an may not be used
}

function showHuman (humanInt: Human) 
{
	console.log('Name: ${humanInt.name}, Surname: ${humanInt.surname}');
	// We need to check if the optional parameter exists
	if (humanInt.age)
	{
		console.log('Age: ${humanInt.age}');
	} else {
		console.log('The person does not have color');
	}
}

showHuman({name: 'Carlos', surname: 'Iborra'});
showHuman({name: 'Carlos', surname: 'Iborra', age: 100});
```

****************************************Read-only properties****************************************
This make the variables (propierties) not modifiable, meaning that once they are assigned a value, we cannot change the variable value.

```tsx
interface Human
{
	readonly name: string;
	readonly surname: string;
}

let nameSurn0: Human = {name: 'Carlos', surname: 'Iborra'};
nameSurn0.name = 'Jorge';  // Once assigned a value to a readonly var. we cannot modify it
```

************************Declaring a function inside an interface************************

```tsx
// Any function/class that implements this interface must follow this structure
interface Human
{
	(name: string, age: string): boolean;
}

const searchHuman: Human = (n: string, age: string): boolean =>
{
	const result = n.search(age);
	return result > -1;
}

console.log(searchHuman("Carlos Iborra 20", 20));
```

<aside>
📝 Note: **`const` is a signal that the identifier won't be reassigned. `let` is a signal that the variable may be reassigned**, such as a counter in a loop

</aside>

**********************Using interface in a class**********************

```tsx