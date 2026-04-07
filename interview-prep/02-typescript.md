# 2. TYPESCRIPT DEEP DIVE

## 2.1 What is TypeScript?
TypeScript is a **statically-typed superset of JavaScript** developed by Microsoft. It compiles to plain JavaScript and adds type safety, interfaces, generics, enums, and better tooling.

## 2.2 Core Concepts

### Basic Types
**What:** TypeScript's built-in type annotations for primitives, arrays, tuples, enums, and special types like `any`, `unknown`, `void`, and `never`.
**Why:** Knowing the type system fundamentals is the first thing interviewers check to see if you truly use TypeScript or just sprinkle `any` everywhere.

```typescript
// Primitives
let name: string = 'Saad';
let age: number = 28;
let active: boolean = true;

// Arrays
let ids: number[] = [1, 2, 3];
let names: Array<string> = ['a', 'b'];

// Tuples
let pair: [string, number] = ['Saad', 28];

// Enums
enum Status { Active = 'ACTIVE', Inactive = 'INACTIVE' }
let s: Status = Status.Active;

// Any vs Unknown
let a: any = 5;      // Disables type checking — AVOID
let u: unknown = 5;  // Safe — must type-check before using

// Void, Never
function log(msg: string): void { console.log(msg); }
function throwError(msg: string): never { throw new Error(msg); }
```

### Interfaces vs Types
**What:** Two ways to define custom types in TypeScript -- interfaces describe object shapes and support declaration merging, while type aliases handle unions, tuples, and more complex compositions.
**Why:** Interviewers frequently ask when to use one over the other to test your depth of TypeScript knowledge beyond basic annotations.

```typescript
// Interface — describes object shape, extendable
interface User {
  id: number;
  name: string;
  email?: string;         // optional
  readonly createdAt: Date; // cannot be modified
}

// Extending interfaces
interface Admin extends User {
  role: 'admin' | 'superadmin';
  permissions: string[];
}

// Type alias — more flexible, can represent unions, tuples, primitives
type ID = string | number;
type Status = 'active' | 'inactive' | 'banned';
type Pair = [string, number];

// Intersection types
type AdminUser = User & { role: string };
```

| Feature | `interface` | `type` |
|---------|------------|--------|
| Object shape | Yes | Yes |
| Extend/inherit | Yes (extends) | Yes (& intersection) |
| Union types | No | Yes |
| Tuple types | No | Yes |
| Declaration merging | Yes | No |
| Use case | Object contracts, APIs | Complex types, unions |

### Generics
**What:** Type parameters (like `<T>`) that allow you to write functions, classes, and interfaces that work with any type while preserving type safety.
**Why:** Generics are the key to writing reusable, type-safe utilities and are heavily tested in senior-level TypeScript interviews.

Generics let you write reusable code that works with multiple types.

```typescript
// Generic function
function getFirst<T>(arr: T[]): T {
  return arr[0];
}
getFirst<number>([1, 2, 3]);  // 1
getFirst<string>(['a', 'b']); // 'a'

// Generic interface
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

type UserResponse = ApiResponse<User>;
type PostResponse = ApiResponse<Post[]>;

// Generic constraints
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

// Generic class
class Repository<T extends { id: number }> {
  private items: T[] = [];

  add(item: T): void { this.items.push(item); }
  findById(id: number): T | undefined {
    return this.items.find(item => item.id === id);
  }
}
```

### Utility Types
**What:** Built-in generic types like `Partial`, `Pick`, `Omit`, `Record`, and `Readonly` that transform existing types without rewriting them.
**Why:** Utility types demonstrate advanced TypeScript fluency and are essential for writing clean DTOs, API responses, and update operations in real projects.

```typescript
// Partial — all properties become optional
type UpdateUser = Partial<User>;

// Required — all properties become required
type FullUser = Required<User>;

// Pick — select specific properties
type UserPreview = Pick<User, 'id' | 'name'>;

// Omit — exclude specific properties
type UserWithoutEmail = Omit<User, 'email'>;

// Record — define key-value pairs
type UserMap = Record<string, User>;

// Readonly — all properties become readonly
type FrozenUser = Readonly<User>;

// ReturnType — extract function return type
type Result = ReturnType<typeof fetchUser>;

// Exclude / Extract — for union types
type NonNull = Exclude<string | null | undefined, null | undefined>; // string
```

### Type Guards
**What:** Runtime checks (`typeof`, `instanceof`, or custom `is` predicates) that narrow a variable's type within a conditional block.
**Why:** Interviewers test type guards to see if you can safely handle union types at runtime while keeping TypeScript's compile-time guarantees.

```typescript
// typeof guard
function process(value: string | number) {
  if (typeof value === 'string') {
    return value.toUpperCase(); // TypeScript knows it's string here
  }
  return value.toFixed(2); // TypeScript knows it's number here
}

// instanceof guard
function handleError(error: Error | string) {
  if (error instanceof Error) {
    return error.message;
  }
  return error;
}

// Custom type guard
function isUser(obj: any): obj is User {
  return obj && typeof obj.name === 'string' && typeof obj.id === 'number';
}
```

### Decorators (Used Heavily in NestJS)
**What:** Special functions prefixed with `@` that attach metadata or modify classes, methods, and properties at design time.
**Why:** Decorators are the backbone of NestJS (and Angular), so interviewers expect you to explain how they work if you list these frameworks on your resume.

```typescript
// Class decorator
function Logger(target: Function) {
  console.log(`Class ${target.name} created`);
}

@Logger
class UserService { }

// Method decorator
function Log(target: any, key: string, descriptor: PropertyDescriptor) {
  const original = descriptor.value;
  descriptor.value = function(...args: any[]) {
    console.log(`Calling ${key} with`, args);
    return original.apply(this, args);
  };
}

class Service {
  @Log
  getData(id: number) { /* ... */ }
}
```

