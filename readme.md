# ADEjs

ADEjs is a JavaScript library for **Context-Oriented Programming (COP)** that supports asynchronous processing. It is an extension of the existing JavaScript COP library, [ContextJs](https://github.com/LivelyKernel/ContextJS), designed to support a layer activation mechanism with a scoping strategy that accommodates all types of JavaScript asynchronous executions, including MicroTask, MacroTask, and EventTask.

This repository is an extension of the previous implementation of ADEjs, updated to support React’s JSX syntax and Function Components.
It does not include implementations that support the async/await syntax.

[previous implementation](https://github.com/kensan914/context-zone) includes the implementation that supports the async/await syntax.

## Usage

### Vanilla JavaScript

```javascript
import { layer } from "contextjs";
import { withLayersZone } from "adejs";

class Foo {
  print() {
    console.log("base");
  }
}
const L1 = layer("L1");
L1.refineClass(Foo, {
  print() {
    console.log("refined");
  },
});
let foo = new Foo();
withLayersZone(L1, () => {
  foo.print(); // prints 'refined'
  setTimeout(() => {
    foo.print(); // prints 'refined'
  }, 1000);
});
```

### JSX in React/React Native

If you want to apply layer activation to the behavior of UI components declared in JSX, please specify the jsx_runtime as ADEjs using the @jsxImportSource annotation.

```jsx
/** @jsxImportSource "../../../node_modules/adejs/lib/react */
withLayersZone(L1, () => {
  <View>
    <Foo />
  </View>;
});
```

### refine Function Components

Function Components that are not written using classes can also be modularized into layers.

```jsx
import { refineFunction } from "adejs";

function Foo() {
  return <Text>base</Text>;
}
const L1 = layer("L1");
Foo = refineFunction(Foo, L1, () => {
  return <Text>refined</Text>;
});
```

## Installation

```bash
npm install adejs
```
