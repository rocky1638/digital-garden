---
title: "typescript"
type: concept
aliases: []
date: 2023-01-05
updated: 2024-05-10
---

## basics

- A wrapper around [[javascript]] to add typing and static analysis to JavaScript.
- We can **explicitly** type a variable like so `const a: number = 6`.
- Without a type, Typescript will implicitly assume the type of the variable.
- Common primitive types.
	- `boolean`, `number`, `string`, `any`.
	- `any` is a catch-all and shouldn’t be used typically.
- Common compound types.
	- `type[]`,
- We type a function with parameter types and a return type.
	- Common return types.
		- `void`: for when the function returns nothing.
		- `never`: for when the function will run forever/throw an error.
	- `const myFunction = (a: number, b: boolean): boolean => {}`.
- We can use generics to handle cases where we want a custom type to be a part of our type.

```javascript
interface CustomArray<T> {  
	[key: number]: T,  
	length: number,  
};

const b: CustomArray<number> = [5, 3, 246, 76];
const c: CustomArray<string> = ['allowed', 'allowed'];
```

## total typescript course

### type transformations

- `typeof` to turn a runtime object into a type.
- `keyof` to turn the keys of an object into a union of keys.
- Lots of utility types like `Extract`, `Pick`, `Omit`, etc.
- `as const` lets you convert a runtime item into a type, with all the strings as string literals and not just `string`.
- `ts-toolbelt` is a library that has extra fancy functions.
- We can use `{}` to tell Typescript to match anything that’s not `null` or `undefined`. This is because Typescript just checks to make sure the fields in the variable `a` match the fields required for type `Type`.
	- In Javascript, everything is technically an object, so everything that’s not `undefined` or `null` will satisfy `{}`.
- We can define local variables using `infer`.
	- `type MyType<T> = T extends { foo: infer TBar} ? TBar : never`
	- https://www.totaltypescript.com/workshops/type-transformations/conditional-types-and-infer/extract-the-result-of-an-async-function/solution
