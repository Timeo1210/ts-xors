# ts-xors

Compose custom types containing multiple mutually exclusive type.

[![npm version](https://badge.fury.io/js/ts-xors.svg)](https://badge.fury.io/js/ts-xors)

## Description

I wanted to combine multiples types but that cannot be together at the same time so i look online for a XOR operator on typescript.

### Little explanation

Take the members `A.a`, `B.b` and `C.c`. Given `type D = A | B | C` but we don't want to be the three at the same time.

I found that Typescript doesn't support this feature yet. [see this](https://github.com/Microsoft/TypeScript/issues/6579)
So i continue my research and i found a npm package call `ts-xor` that solve my problem but only in half.
I wanted to combine **multiple** types. This package cannot resolve this probleme.

Again, I continue my research and i found [this stackoverflow](https://stackoverflow.com/questions/42123407/does-typescript-support-mutually-exclusive-types)
which contain a little comments from [tjjfvi](https://stackoverflow.com/users/11860232/tjjfvi) that find the way of solving this feature.
_This package use the work of [tjjfvi](https://stackoverflow.com/users/11860232/tjjfvi)._

**This package introduces the new type `XORS` operator from boolean algebra as defined by the following truth table:**
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

## Usage

```typescript
const usage: XORS<[A, B, C, ...]>
```

`XORS` type take an array of type without restriction on the size.

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

## NPM

This library is [published on NPM](https://www.npmjs.com/package/ts-xors).

## Licence

Distributed under the MIT license. See [`LICENSE.md`](https://github.com/Timeo1210/ts-xors/blob/master/LICENSE.md) for more information.
