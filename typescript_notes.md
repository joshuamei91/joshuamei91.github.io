---
layout: page
title: Typescript Notes
permalink: /ts-cheatcheet/
---

## Useful logic
- Return `true` if `true` and return `false` if `false` or `undefined`: `!!trueFalseUndef`

## Tidbits

### [Union Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)
> A union type is a type formed from two or more other types, representing values that may be any one of those types. TypeScript will only allow you to do things with the union if that thing is valid for every member of the union.
``` typescript
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}
```

### [Narrowing union types](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
``` typescript
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return new Array(padding + 1).join(" ") + input;
  }
  return padding + input;
}
```
If every member in a union has a property in common, you can use that property without narrowing:
``` typescript
// Return type is inferred as number[] | string
function getFirstThree(x: number[] | string) {
  return x.slice(0, 3);
}
```
***`in` operator narrowing***

The “true” branch narrows x’s types which have either an optional or required property value, and the “false” branch narrows to types which have an optional or missing property value.
``` typescript
type Fish = { swim: () => void };
type Bird = { fly: () => void };
type Human = {  swim?: () => void, fly?: () => void };

function move(animal: Fish | Bird | Human) {
  if ("swim" in animal) { 
    animal // (parameter) animal: Fish | Human
  } else {
    animal // (parameter) animal: Bird | Human
  }
}
```
***`instanceof` narrowing***

`x instanceof Foo` checks whether the prototype chain of `x` contains `Foo.prototype`
``` typescript
function logValue(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString()); // (parameter) x: Date
  } else {
    console.log(x.toUpperCase()); // (parameter) x: string
  }
}
```

### User defined type guard for narrowing

To define a user-defined type guard, we simply need to define a function whose return type is a type predicate. A predicate takes the form `parameterName is Type`.
``` typescript
// user defined type guard
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}

// usage
if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```
### Exclude property from type
`Omit<T, 'property1'|'property2'>`

### Truthiness

The following values coerce to `false`:
- `0`
- `Nan`
- `""` (empty string)
- `0n` (bigint version of zero)
- `null`
- `undefined`

### [Barrel](https://basarat.gitbook.io/typescript/main-1/barrel)
> A barrel is a way to rollup exports from several modules into a single convenient module. The barrel itself is a module file that re-exports selected exports of other modules.

``` typescript
// test/foo.ts
export class Foo()
// test/bar.ts
export class Bar()

// test/index.ts - this is the barrel
// re-export all from this file
export * from './foo'
export * from './bar'

// usage
import { Foo, Bar } from '../test' // test/index.ts is implied 
```

### [Use async/await in array.map instead of array.forEach for parallel processing](https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop)
``` typescript
async function printFiles () {
  const files = await getFilePaths();

  await Promise.all(files.map(async (file) => {
    const contents = await fs.readFile(file, 'utf8')
    console.log(contents)
  }));
}
```


### [@ symbol in import](https://stackoverflow.com/questions/42711175/what-does-the-symbol-do-in-javascript-imports)
> Refers to the root of the project and it is usually configured in the .babelrc of the babel plugin


