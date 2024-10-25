<a href="https://araby.org/"><img src="https://i.imgur.com/5ZorFhe.png"/></a>
<div align="center">
    <img src="https://img.shields.io/badge/Araby Organization-%23000000">
    <img src="https://img.shields.io/github/stars/i3raby/araby-package">
</div>

## Installation

**Node.js 18 or newer is required.**

```
npm install araby
yarn add araby
pnpm add araby
bun add araby
```

### **`NodeError(options: NodeErrorOptions): ReturnNodeError`**

The `NodeError` function is a customizable error management system that allows you to define and throw specific error messages with associated codes. It provides a convenient way to handle different types of errors, such as *`TypeError`*, *`RangeError`*, *`Error`*, *`SyntaxError`*, and *`ReferenceError`*, along with user-defined messages and codes.
```js
const { NodeError } = require('araby');

const { Error } = NodeError({
    messages: {
        'InvalidNumber': 'Please check the number you entered and try again.',
        'InvalidID': (ID) => `Please check the ID number ${ID}`
    }
})

throw new Error('InvalidNumber') // Output: "Please check the number you entered and try again."
throw new Error('InvalidID', 0) // Output: "Please check the ID number 0"
```

### **`NodeWarning(messages: NodeWarningMessages): ReturnNodeWarning`**

The `NodeWarning` function is a custom warning system built around Node.js's *`process.emitWarning`*. It allows you to define and emit custom warnings with specific messages and tags, providing an easy way to manage and trigger warnings throughout your application.

```js
const { NodeWarning } = require('araby');

const Warnings = NodeWarning({
    InvalidUser: {
        message: 'This user is invalid, please check the user details.'
    },
    InvalidMessage: {
        message: (id) => `Please check the message with id ${id}.`,
        tag: 'APIMessage'
    }
})

Warnings('InvalidUser');
// Emits: (node:56338) InvalidUser: This user is invalid, please check the user details.

Warnings('InvalidMessage', '12345');
// Emits: (node:56338) [APIMessage] InvalidMessage: Please check the message with id 12345.
```

### **`NodeEnumeration(keys: NodeNodeEnumerationKeys[]): R`**

The `NodeEnumeration` function is used to create a two-way mapping between keys and values from an array. It generates an object where both the indices and the values of the array are accessible through each other, allowing for bidirectional lookup.

```js
const { NodeEnumeration } = require('araby');

const Keys = NodeEnumeration([
    undefined,
    'PRIVATE_PACKAGE',
    undefined,
    'PUBLIC_PACKAGE'
]);

console.log(Keys.PRIVATE_PACKAGE); // Output: 1
console.log(Keys[1]); // Output: PRIVATE_PACKAGE

console.log(Keys.PUBLIC_PACKAGE); // Output: 1
console.log(Keys[3]); // Output: PRIVATE_PACKAGE

console.log(Keys.ArabyPackage); // Output: undefined
console.log(Keys[0]); // Output: undefined
console.log(Keys[2]); // Output: undefined
```

### **`toObject(object: Object, props: ObjectProps): R`**

The `toObject` function takes an instance of a class and converts it into a plain JavaScript object. This is useful for extracting and working with the properties and values of a class instance in a simple object format, allowing for easier serialization (e.g., converting to JSON) or manipulation.

```js
const { toObject } = require('araby');

class NodeObject {
    constructor() {
        this.key = 'Key'
    }

    get classPropertyOne() {
        return 'classPropertyOne';
    }

    get classPropertyTwo() {
        return 'classPropertyTwo';
    }

    toObject() {
        return toObject(this, { 
            classPropertyOne: true,
            classPropertyTwo: true
        })
    }
}


const package = new NodeObject();

console.log(package.toObject()) // Output: { key: 'Key', classPropertyOne: 'classPropertyOne', classPropertyTwo: 'classPropertyTwo' }
```

### **`isNone(value: any): boolean`**
The `isNone` function checks if the provided value is `null`.

```js
const { isNone } = require('araby');

console.log(isNone('String')) // false
console.log(isNone(null)) // true
```

### **`ProcessBar(options: ProcessBarOptions): string`**

The `ProcessBar` function generates a visual representation of a progress bar based on the given options.

```js
const { ProcessBar } = require('araby');
console.log(ProcessBar({ value: 30, max: 100, size: 10 })); // Output: "███░░░░░░░"
```

### **`NumberGenerate(length: number): number`**

The `NumberGenerate` function generates a random number of a specified length.

```js
const { NumberGenerate } = require('araby');

const Number = NumberGenerate(4);
console.log(Number); // Outputs a random 4-digit number, e.g., 2357
```

### **`Colors`**

The `Colors` namespace provides a set of utility functions to format text with various colors and background colors for use in terminal environments. Each function applies a specific color or background color to a given text string, helping to enhance the readability and presentation of terminal output.

```js
const { Colors } = require('araby');

console.log(Colors.Red('Text'));
console.log(Colors.backgroundBrightRed('Text'));
console.log(Colors.backgroundRed('Text'));
```
