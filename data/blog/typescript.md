---
title: TypeScript notes
date: '2021-01-05'
tags: ['TypeScript', 'code']
draft: false
summary: Notes from learning TypeScript
---

In TypeScript, two types are compatible if their internal structure is compatible. This allows us to implement an interface just by having the shape the interface requires, without an explicit `implements` clause.

There are two syntaxes for building types: [Interfaces and Types](https://www.typescriptlang.org/play/?e=83#example/types-vs-interfaces). You should prefer `interface`. Use `type` when you need specific features.

Calling `Date()` in JavaScript returns a string. On the other hand, constructing a `Date` with `new Date()` actually gives us a `Date` object.

It’s best not to add annotations when the type system would end up inferring the same type anyway.

## Optional properties

Object types can also specify that some or all of their properties are optional. To do this, add a `?` after the property name.

```ts
function printName(obj: { first: string; last?: string }) {
  // ...
}
// Both OK
printName({ first: 'Bob' })
printName({ first: 'Alice', last: 'Alison' })
```

In JavaScript, if you access a property that doesn’t exist, you’ll get the value undefined rather than a runtime error. Because of this, when you read from an optional property, you’ll have to check for undefined before using it.

```ts
function printName(obj: { first: string; last?: string }) {
  // Error - might crash if 'obj.last' wasn't provided!
  console.log(obj.last.toUpperCase());
Object is possibly 'undefined'.
  if (obj.last !== undefined) {
    // OK
    console.log(obj.last.toUpperCase());
  }

  // A safe alternative using modern JavaScript syntax:
  console.log(obj.last?.toUpperCase());
}
```
