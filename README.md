# ts-xors

Compose custom types containing multiple mutually exclusive type.

[![npm version](https://badge.fury.io/js/ts-xors.svg)](https://badge.fury.io/js/ts-xors)

## Description

### The problem

Using mutually exclusives types _(XOR)_ is not a default feature in Typescript, [see this](https://github.com/Microsoft/TypeScript/issues/14094)

### The solution

**This package allow it by introducing the new type `XORS` type**

```typescript
let usage: XORS<[A, B, C, ...]>
```

`XORS` type take an array of type without size restriction.
_Check the examples for more comprehension_

### The implementation

There is multiple way of achieving the same result, be for this specific problem we're using the work of [tjjfvi](https://stackoverflow.com/users/11860232/tjjfvi). As he show in [this Stackoverflow](https://stackoverflow.com/questions/42123407/does-typescript-support-mutually-exclusive-types)

We are ending up with this truth table.
| A | B | C | ... | Result |
| :-: | :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | ... | 0 |
| 1 | 0 | 0 | ... | 1 |
| 0 | 1 | 0 | ... | 1 |
| 0 | 0 | 1 | ... | 1 |
| 1 | 1 | 0 | ... | 0 |
| 1 | 0 | 1 | ... | 0 |
| 0 | 1 | 1 | ... | 0 |
| 1 | 1 | 1 | ... | 0 |

## Installation

In your typescript project, run:

```sh
npm install -D ts-xors
# or
yarn add -D ts-xors
```

## Examples

### 1 - Default Case

```typescript
import XORS from "ts-xors"

interface A {
  a: string
}
interface B {
  b: string
}
interface C {
  c: string
}

let defaultExample: XORS<[A, B, C]>

defaultExample = {} // FAILS
defaultExample = {a: ""} // WORK
defaultExample = {b: ""} // WORK
defaultExample = {c: ""} // WORK
defaultExample = {a: "", b: ""} // FAILS
defaultExample = {b: "", c: ""} // FAILS
...
```

### 2 - Simple Case

```typescript
import XORS from "ts-xors";

interface A {
  a: string;
}
interface B {
  b: string;
}

let simpleExample: XORS<[A, B]>;
simpleExample = {}; // FAILS
simpleExample = { a: "" }; // WORK
simpleExample = { b: "" }; // WORK
simpleExample = { a: "", b: "" }; // FAILS
```

## Licence

Distributed under the MIT license. See [`LICENSE.md`](https://github.com/Timeo1210/ts-xors/blob/master/LICENSE.md) for more information.

## Links

This library is [published on NPM](https://www.npmjs.com/package/ts-xors).
Check me on [Twitter](https://twitter.com/TimeoBoulhol)
