# ECMAScript proposal: `async do` expressions

`async do` expressions allow you to introduce an asynchronous context within synchronous code without needing an immediately-invoked async function expression.

This proposal builds off of the [`do` expressions proposal](https://github.com/tc39/proposal-do-expressions).

This proposal has [preliminary spec text](https://tc39.github.io/proposal-async-do-expressions/).

## Motivation

Currently the boundary between synchronous and asynchronous code requires defining and invoking an `async` function. In the case that you just want to perform a single operation, that's a lot of syntax for a relatively primitive operation: `(async () => {...})()`. This lets you write `async do {...}` instead.

## Examples

```js
// at the top level of a script

async do {
  await readFile('in.txt');
  let query = await ask('???');
  // etc
}
```

```js
Promise.all([
  async do {
    let result = await fetch('thing A');
    await result.json();
  },
  async do {
    let result = await fetch('thing B');
    await result.json();
  },
]).then(([a, b]) => console.log([a, b]));
```
