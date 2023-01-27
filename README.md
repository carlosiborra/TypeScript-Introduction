# TypeScript Introduction

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
```

But if we modify the value of a variable already initialized with a different type, we’ll get an error as TypeScript does not permit changing types within the same variable.

```tsx
var example = 2;  // Variable of type int
var example = "hello World";  // ERROR: we already initialized the var. with number type
```

## 2.2. Types

But as it might seem, is a way better approach to type the variables directly from a beggining as we’ll control all the assigned types and values.

### 2.2.1. Boolean

```tsx
let booleanExample: boolean;

// We can also initialize the cariable with a certain value at start
let booleanExample: boolean = true;

// And then modify it as follows
booleanExample = false;
```

### 2.2.2 ************Number************

Numbers in TypeScript (as in JS) are either **floating point values** or **BigIntegers**. These **floating point numbers** get the type ***number***, while **BigIntegers** get the type ***bignint**.*

**Floating point values**

```tsx
let numberExampleDecimal: number = 10;
let numberExampleHexadecimal: number = 0xA;
let numberExampleBinary: number = 0b1010;
let numberExampleOctal: number = 0o12;
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
let stringName: string = 'name';
let stringSurname: string = 'surname';

let stringCompleteName: string = '${stringName} ${stringSurname}'

// As result we will obtain 'name surname' string as the value of stringCompleteName
```