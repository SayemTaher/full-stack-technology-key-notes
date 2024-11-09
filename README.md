
# TypeScript Fundamentals: Key Concepts and Examples

This document provides an overview of fundamental TypeScript concepts, including type guards, object manipulation, 
data validation, and other core functionalities. Each section includes explanations and examples to aid understanding.

---

## Table of Contents

- [1. Type Guards](#1-type-guards)
  - [`typeof` Operator](#typeof-operator)
  - [`instanceof` Operator](#instanceof-operator)
  - [`in` Operator](#in-operator)
- [2. Object Manipulation](#2-object-manipulation)
- [3. Data Validation](#3-data-validation)
- [4. Utility Types](#4-utility-types)
- [Overview](#overview)

---

## 1. Type Guards

Type guards are TypeScript expressions that allow narrowing down types at runtime, ensuring that a variable meets specific 
criteria before executing operations on it. Below are common type guards and their usage.

### `typeof` Operator

The `typeof` operator checks if a variable is a specific primitive type, such as `string`, `number`, or `boolean`.

#### Example:

```typescript
const processValue = (value: string | number): string => {
    if (typeof value === "string") {
        return `String value: ${value}`;
    } else if (typeof value === "number") {
        return `Number value: ${value * 10}`;
    }
    return "Unknown type";
};
```

This function uses `typeof` to check if the input `value` is a `string` or a `number`, performing operations accordingly.

### `instanceof` Operator

The `instanceof` operator checks if an object is an instance of a particular class, useful when working with class instances.

#### Example:

```typescript
class Animal {
    constructor(public name: string) {}
}

class Dog extends Animal {
    bark() {
        return `${this.name} says Woof!`;
    }
}

const identifyAnimal = (pet: Animal) => {
    if (pet instanceof Dog) {
        return pet.bark();
    }
    return `Unknown animal: ${pet.name}`;
};

const dog = new Dog("Buddy");
identifyAnimal(dog); // "Buddy says Woof!"
```

This example checks if `pet` is an instance of `Dog` before calling the `bark` method, ensuring type safety.

### `in` Operator

The `in` operator checks if a property exists in an object, useful for conditionally accessing optional properties.

#### Example:

```typescript
type User = { name: string; role?: string };

const greetUser = (user: User) => {
    if ("role" in user) {
        return `Hello, ${user.name}, you are logged in as ${user.role}`;
    }
    return `Hello, ${user.name}`;
};

const adminUser = { name: "Alice", role: "Admin" };
greetUser(adminUser); // "Hello, Alice, you are logged in as Admin"
```

Here, `in` checks if the `role` property exists, allowing the function to respond based on user type.

---

## 2. Object Manipulation

TypeScript allows various ways to manipulate objects safely by combining type definitions with object-related operations.

#### Example:

```typescript
type Product = { id: number; name: string; price?: number };

const formatProduct = (product: Product): string => {
    const priceInfo = product.price ? `$${product.price}` : "Price not available";
    return `Product: ${product.name} (ID: ${product.id}) - ${priceInfo}`;
};

const product = { id: 1, name: "Laptop" };
formatProduct(product); // "Product: Laptop (ID: 1) - Price not available"
```

In this example, optional properties are handled with conditional logic, making the function flexible to varying data.

---

## 3. Data Validation

Data validation ensures that inputs meet required criteria before processing, often using type guards to verify structure.

#### Example:

```typescript
type Person = { name: string; age: number };

const validatePerson = (person: any): person is Person => {
    return typeof person.name === "string" && typeof person.age === "number";
};

const processPerson = (person: any) => {
    if (validatePerson(person)) {
        return `Valid person: ${person.name}, age ${person.age}`;
    }
    return "Invalid data structure";
};

const person = { name: "John", age: 30 };
processPerson(person); // "Valid person: John, age 30"
```

This function validates that the input has the required structure and types before processing, avoiding runtime errors.

---

## 4. Utility Types

TypeScript provides utility types like `Partial`, `Readonly`, and `Record` to simplify and enhance type management.

### Examples:

1. **Partial**: Makes all properties of a type optional.

    ```typescript
    type User = { id: number; name: string };
    const updateUser = (user: Partial<User>) => {
        if (user.name) {
            console.log(`Updating user name to ${user.name}`);
        }
    };
    updateUser({ id: 1 }); // Partial update allowed
    ```

2. **Readonly**: Makes all properties of a type read-only.

    ```typescript
    type Config = Readonly<{ apiUrl: string }>;
    const config: Config = { apiUrl: "https://api.example.com" };
    // config.apiUrl = "new_url"; // Error: cannot modify readonly property
    ```

3. **Record**: Defines a type with a specific set of keys and a uniform value type.

    ```typescript
    type RolePermissions = Record<string, string[]>;
    const permissions: RolePermissions = {
        admin: ["create", "delete"],
        user: ["read", "write"],
    };
    ```

---

## Overview

This document provides an overview of key TypeScript concepts essential for building reliable applications. 
From type guards and object manipulation to data validation and utility types, these fundamentals help maintain type safety, 
prevent errors, and improve code readability in TypeScript projects.
