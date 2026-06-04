# TypeScript Fundamentals — Quick Reference Notes

> **Goal:** 10–20 min refresh. Each section has the concept, the why, and a quick code example.

---

## 1. Welcome to TypeScript

TypeScript is an **open-source, typed superset of JavaScript** that compiles to clean, readable JS.

**Three parts:**
- **Language** — the syntax you write (types, generics, etc.)
- **Compiler (`tsc`)** — strips types and emits JS
- **Language Server** — powers editor intellisense (VS Code, etc.)

**Mental model:** TypeScript is a fancy linter that catches bugs *at build time*, not runtime. The compiled JS has zero type information.

**File types:**
| File | Contains |
|------|----------|
| `.ts` | Types + runnable code |
| `.js` | Only runnable code |
| `.d.ts` | Only type information (declaration files) |

**Minimal project anatomy:**
```
package.json   # package manifest
tsconfig.json  # TS compiler settings
src/index.ts   # entry point
```

**Why TypeScript?** JS is fine with everything until the call stack blows up at runtime. TS surfaces those errors before they ship.

---

## 2. Variables and Values

**Variables are born with types** at the point of initialization — TS infers the type from the value.

```ts
const humidity = 79       // type: 79  (literal type, not `number`)
let temperature = 72      // type: number
```

**Literal types** — when a value is immutable (e.g., `const`), TS locks the type to that exact value.
```ts
const direction = "north"  // type: "north", not string
```

**`as const`** — forces a `let` variable to behave like a `const` (narrows to literal type):
```ts
let humidity = 79 as const  // type: 79
```

Think of types as **sets of allowed values**: `79` is a subset of `number`, making `79` a *subtype* of `number`.

**Implicit `any`** — if a `let` variable is declared without an initial value, TS falls back to `any` (the JS default):
```ts
let value          // type: any — avoid this
let value: string  // explicit, preferred
```

**Type casting** — forcing the compiler to treat a value as a different type. Use sparingly:
```ts
let date = "oops" as any as Date  // TS thinks Date, actually a string — dangerous
```

**Function annotations:**
```ts
function add(a: number, b: number): number {
  return a + b
}
```

---

## 3. Objects, Arrays, and Tuples

### Objects
```ts
let car: {
  make: string
  model: string
  year: number
}
```

**Optional properties** — use `?` to mark a property as optional:
```ts
let config: {
  host: string
  port?: number  // may or may not be present
}
```

**Index signatures** — when you don't know all the keys upfront:
```ts
let phones: {
  [k: string]: {
    country: string
    area: string
    number: string
  }
}
```

### Arrays
```ts
let scores: number[] = [90, 85, 92]
let names: Array<string> = ["Alice", "Bob"]  // generic form, same thing
```

### Tuples
A fixed-length array where **each position has a known type**:
```ts
let myCar: [number, string, string] = [2002, "Toyota", "Corolla"]
```

**`readonly` tuple** — prevents mutation via `push`/`pop`:
```ts
const pair: readonly [number, number] = [4, 5]
pair.push(6)  // Error — cannot mutate a readonly tuple
```

---

## 4. Structural vs Nominal Types

### Nominal type system
Compatibility is determined by **type names**. Two types with the same shape but different names are *incompatible*. (Java, C# use this.)

### Structural type system (TypeScript's approach)
Compatibility is determined by **shape/structure**, not names. If it has the right properties, it's compatible — this is *duck typing*.

```ts
type Point2D = { x: number; y: number }
type Point3D = { x: number; y: number; z: number }

let p2: Point2D = { x: 1, y: 2 }
let p3: Point3D = { x: 1, y: 2, z: 3 }

p2 = p3  // OK — Point3D has everything Point2D needs (it's a superset)
p3 = p2  // Error — Point2D is missing `z`
```

**TS compatibility question:** "Is type A a *subset* of type B?" If yes → compatible.

---

## 5. Intersection and Union Types

### Union Types (`|`) — "OR"
A value can be **one of several types**. Useful for values that can take multiple forms.

```ts
type StringOrNumber = string | number

function format(val: string | number): string {
  if (typeof val === "string") return val.toUpperCase()  // narrowing
  return val.toFixed(2)
}
```

**Discriminated unions** — a union where a shared literal property helps TS narrow:
```ts
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number }

function area(shape: Shape) {
  if (shape.kind === "circle") return Math.PI * shape.radius ** 2
  return shape.side ** 2
}
```

### Intersection Types (`&`) — "AND"
Combines multiple types into one — the result must satisfy **all** of them:

```ts
type HasId = { id: string }
type HasTimestamp = { createdAt: Date }

type Record = HasId & HasTimestamp
// Record must have both `id` and `createdAt`

type SpecialDate = Date & { getDescription(): string }
const newYearsEve: SpecialDate = Object.assign(new Date(), {
  getDescription() { return "last day of the year" }
})
```

**Union** = broader (fewer guarantees), **Intersection** = narrower (more guarantees).

---

## 6. Interfaces and Type Aliases

Both let you name and reuse a type. The difference matters at the edges.

### Type Aliases (`type`)
Can represent **any type** — primitives, unions, intersections, tuples, etc.:
```ts
type ID = string | number
type Point = { x: number; y: number }
type Pair<T> = [T, T]
```

### Interfaces (`interface`)
Designed specifically for **object shapes**. Supports declaration merging and `extends`:
```ts
interface Animal {
  name: string
}

interface Dog extends Animal {
  breed: string
}
```

**Declaration merging** — interfaces with the same name are merged automatically (useful for augmenting third-party types):
```ts
interface Window { myCustomProp: string }
interface Window { anotherProp: number }
// Window now has both
```

**`implements`** — a class commits to satisfying an interface contract:
```ts
interface Serializable {
  serialize(): string
}
class User implements Serializable {
  serialize() { return JSON.stringify(this) }
}
```

**`extends` in interfaces** — inheritance; the child gets all parent members.

**Rule of thumb:** Use `interface` for object shapes that may be extended/implemented. Use `type` for everything else (unions, intersections, aliases for primitives).

---

## 7. JSON Types

JSON has a limited set of value types. Representing them accurately in TS:

```ts
type JSONPrimitive = string | number | boolean | null

type JSONObject = { [key: string]: JSONValue }

type JSONArray = JSONValue[]

type JSONValue = JSONPrimitive | JSONObject | JSONArray
```

This is a **recursive type** — `JSONValue` refers to itself through `JSONObject` and `JSONArray`.

**Why it matters:** When parsing `JSON.parse()`, TS returns `any`. If you want type safety, cast or validate after parsing:
```ts
const data = JSON.parse(rawString) as JSONValue  // at least constrains to valid JSON
```

**Practical use:** Validating API payloads, config files, or any data that comes from outside your system boundary.

---

## 8. Type Queries

Type queries let you **extract type information from existing values or types** rather than writing types by hand.

### `typeof` (type-level)
Capture the type of a value:
```ts
const config = { host: "localhost", port: 3000 }
type Config = typeof config  // { host: string; port: number }

function useConfig(c: typeof config) { ... }
```

### `keyof`
Extract all keys of an object type as a union:
```ts
type Config = { host: string; port: number }
type ConfigKey = keyof Config  // "host" | "port"

function getConfigValue(config: Config, key: keyof Config) {
  return config[key]
}
```

### `keyof typeof` (common combo)
Get the keys of a value's type:
```ts
const STATUS = { active: 1, inactive: 0, banned: -1 } as const
type StatusKey = keyof typeof STATUS  // "active" | "inactive" | "banned"
```

### Indexed Access Types (`T[K]`)
Look up the type of a specific property:
```ts
type Config = { host: string; port: number }
type PortType = Config["port"]   // number
type AnyValue = Config[keyof Config]  // string | number
```

### `ReturnType<T>` and `Parameters<T>`
Built-in utility types that query function types:
```ts
function fetchUser(id: string) { return { id, name: "Alice" } }

type User = ReturnType<typeof fetchUser>        // { id: string; name: string }
type FetchArgs = Parameters<typeof fetchUser>   // [id: string]
```

---

## Quick Cheat Sheet

| Concept | One-liner |
|---------|-----------|
| Literal type | Exact value as a type (`"north"`, `79`) |
| `as const` | Freeze a value to its literal type |
| Union `\|` | Value is one of several types |
| Intersection `&` | Value satisfies all types combined |
| `interface` | Named object shape, extendable, mergeable |
| `type` | Alias for any type expression |
| `typeof` (type-level) | Capture a value's type |
| `keyof` | Union of an object's keys |
| `T[K]` | Type of property `K` in `T` |
| Structural typing | Compatibility by shape, not name |
