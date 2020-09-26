---
title: Typescript Utility Types Cheatsheet
date: "2020-09-26T16:51:00.000Z"
layout: post
draft: false
path: "/posts/typescript-cheatsheet/"
category: "typescript"
tags:
  - "typescript"
description: "Recap of some of the most common utility types"
---

**keyof**

- Queries the set of keys for a given type
- Get union of known public property names

```typescript
interface Todo {
	id: number;
	text: string;
	due: Date
}

type TodoKeys = keyof Todo; // "id" | "text" | "due"
```

**in**

- Iterate over all the items in a union of keys

```typescript
interface Person {
    name: string;
    age: number;
}
type Partial<T> = {
    [P in keyof T]?: T[P]; // P will be each key of T
}
type PersonPartial = Partial<Person>; // same as { name?: string;  age?: number; }
```

**PickByValue**

- Pick a set of properties from a type which match a certain type such as Function, String, Boolean

```typescript
type Props = { req: number; reqUndef: number | undefined; opt?: string; };

type Props = PickByValue<Props, number | undefined>; // { req: number; reqUndef: number | undefined }
```

**Partial**

- Make all properties optional

```typescript
type Person = {name: string, nickName: string};

type OptionalPerson = Partial<Person>; // {name?: string, nickName?: string}
```

**Required**

- The reverse of the above
- Make all properties required

**Readonly**

- Similar to above but make them all readonly

**Pick**

- Pick set of properties from a type

```typescript
interface Todo {
    title: string;
    description: string;
    completed: boolean;
}

type TodoPreview = Pick<Todo, 'title' | 'completed'>;

const todo: TodoPreview = {
    title: 'Clean room',
    completed: false,
};
```

**Omit**

- Remove a set of properties but keep the rest

```typescript
interface Todo {
    title: string;
    description: string;
    completed: boolean;
}

type TodoPreview = Omit<Todo, 'description'>;

const todo: TodoPreview = {
    title: 'Clean room',
    completed: false,
};
```

**Exclude**

- Exclude properties from a type
- Used in Omit

```typescript
type T0 = Exclude<"a" | "b" | "c", "a">;  // "b" | "c"
type T1 = Exclude<"a" | "b" | "c", "a" | "b">;  // "c"
type T2 = Exclude<string | number | (() => void), Function>;  // string | number
```

**Extract**

- Extract all type that match an union

```typescript
type T0 = Extract<"a" | "b" | "c", "a" | "f">; // "a"
type T1 = Extract<"a" | "b" | "c", "a" | "b">; // "a" | "b"
type T2 = Extract<string | number | (() => void), Function>; // () => void

```

**ReturnType**

- Constructs a type consisting of the return type of function

**Intersection**

- `&`
- Combine two different type or interfaces

**Union**

- Any value in the union but not a combination of all