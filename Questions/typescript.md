# TypeScript Interview Questions

## 1. Why TypeScript?

### Answer
TypeScript adds static typing to JavaScript, improving maintainability, tooling, and code reliability.

---

## 2. Interface vs Type

### Interface

```ts
interface User {
  id: number;
  name: string;
}
```

### Type

```ts
type User = {
  id: number;
  name: string;
};
```

### Interview Answer
Interfaces are preferred for object shapes and extension. Types are more flexible and support unions and intersections.

---

## 3. unknown vs any

### any

```ts
let value: any;
```

Disables type checking.

### unknown

```ts
let value: unknown;
```

Requires type checking before usage.

### Interview Answer
Prefer `unknown` because it is type-safe.

---

## 4. What are Generics?

### Answer
Generics allow reusable components and functions while preserving type safety.

### Example

```ts
function identity<T>(value: T): T {
  return value;
}
```

---

## 5. What is Partial<T>?

### Answer

Makes all properties optional.

```ts
interface User {
  id: number;
  name: string;
}

type PartialUser = Partial<User>;
```
