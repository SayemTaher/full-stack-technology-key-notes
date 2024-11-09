
# TypeScript Fundamentals and Classes: Key Concepts and Examples

This document provides an overview of fundamental TypeScript concepts, including type guards, object manipulation, 
data validation, and class-related functionalities like inheritance, access modifiers, and abstract classes. 
Each section includes explanations and examples to aid understanding.

---

## Table of Contents

- [TypeScript Fundamentals](#typescript-fundamentals)
  - [1. Type Guards](#1-type-guards)
    - [`typeof` Operator](#typeof-operator)
    - [`instanceof` Operator](#instanceof-operator)
    - [`in` Operator](#in-operator)
  - [2. Object Manipulation](#2-object-manipulation)
  - [3. Data Validation](#3-data-validation)
  - [4. Utility Types](#4-utility-types)
- [TypeScript Classes](#typescript-classes)
  - [1. Defining a Class](#1-defining-a-class)
  - [2. Constructors](#2-constructors)
  - [3. Access Modifiers](#3-access-modifiers)
    - [Public](#public)
    - [Private](#private)
    - [Protected](#protected)
  - [4. Inheritance](#4-inheritance)
  - [5. Methods](#5-methods)
  - [6. Getters and Setters](#6-getters-and-setters)
  - [7. Abstract Classes](#7-abstract-classes)
- [Overview](#overview)

---

# TypeScript Fundamentals

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

# TypeScript Classes

This section provides an overview of essential TypeScript concepts related to classes, including inheritance, access modifiers, methods, 
constructors, and other core functionalities.

---

## 1. Defining a Class

A class in TypeScript is a blueprint for creating objects with properties and methods. It helps encapsulate related data and behaviors.

### Example:

```typescript
class Animal {
    name: string;
    constructor(name: string) {
        this.name = name;
    }

    speak() {
        console.log(`${this.name} makes a noise.`);
    }
}
```

This example defines a simple `Animal` class with a property `name` and a method `speak()`.

---

## 2. Constructors

The constructor is a special method in TypeScript that gets called when an instance of the class is created. It’s used to initialize the object’s properties.

### Example:

```typescript
class Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    introduce() {
        return `Hello, I'm ${this.name} and I'm ${this.age} years old.`;
    }
}

const person = new Person("Alice", 30);
person.introduce(); // "Hello, I'm Alice and I'm 30 years old."
```

The `constructor` initializes the `name` and `age` properties when a new `Person` instance is created.

---

## 3. Access Modifiers

Access modifiers determine the visibility of properties and methods within a class. TypeScript offers three primary modifiers:

### Public

`public` members are accessible from anywhere. By default, all members are `public`.

#### Example:

```typescript
class Car {
    public brand: string;

    constructor(brand: string) {
        this.brand = brand;
    }
}
```

### Private

`private` members are accessible only within the class they are defined in.

#### Example:

```typescript
class BankAccount {
    private balance: number = 0;

    deposit(amount: number) {
        this.balance += amount;
    }

    getBalance() {
        return this.balance;
    }
}
```

The `balance` property is private, so it can only be modified through the `deposit` method.

### Protected

`protected` members are accessible within the class and by subclasses but not from outside.

#### Example:

```typescript
class Employee {
    protected name: string;

    constructor(name: string) {
        this.name = name;
    }
}

class Manager extends Employee {
    display() {
        return `Manager: ${this.name}`;
    }
}
```

The `name` property is protected, so it’s accessible within `Employee` and any class that extends it.

---

## 4. Inheritance

Inheritance allows a class to inherit properties and methods from another class, promoting reusability.

### Example:

```typescript
class Animal {
    constructor(public name: string) {}

    move(distance: number) {
        console.log(`${this.name} moved ${distance} meters.`);
    }
}

class Bird extends Animal {
    fly(distance: number) {
        console.log(`${this.name} flew ${distance} meters.`);
    }
}

const bird = new Bird("Sparrow");
bird.move(5);
bird.fly(10);
```

In this example, `Bird` inherits the `move` method from `Animal` and also defines its own `fly` method.

---

## 5. Methods

Methods are functions defined within a class that can operate on the class’s properties.

### Example:

```typescript
class Calculator {
    add(x: number, y: number): number {
        return x + y;
    }

    multiply(x: number, y: number): number {
        return x * y;
    }
}

const calc = new Calculator();
calc.add(2, 3); // 5
calc.multiply(4, 5); // 20
```

The `Calculator` class has two methods, `add` and `multiply`, which perform basic arithmetic operations.

---

## 6. Getters and Setters

Getters and setters are special methods that allow controlled access to private properties.

### Example:

```typescript
class User {
    private _name: string;

    constructor(name: string) {
        this._name = name;
    }

    get name(): string {
        return this._name;
    }

    set name(newName: string) {
        if (newName.length > 0) {
            this._name = newName;
        }
    }
}

const user = new User("Alice");
console.log(user.name); // "Alice"
user.name = "Bob";
console.log(user.name); // "Bob"
```

Here, `name` is accessed via a getter, and it can be updated via a setter, adding control over its value.

---

## 7. Abstract Classes

An abstract class cannot be instantiated on its own and serves as a base class for other classes to extend. 
It can define abstract methods that must be implemented in derived classes.

### Example:

```typescript
abstract class Shape {
    abstract area(): number;

    display(): void {
        console.log("Displaying shape information.");
    }
}

class Circle extends Shape {
    constructor(public radius: number) {
        super();
    }

    area(): number {
        return Math.PI * this.radius ** 2;
    }
}

const circle = new Circle(5);
circle.display(); // "Displaying shape information."
console.log(circle.area()); // Area of the circle
```

The `Shape` class is abstract and defines an `area` method that must be implemented by any subclass, such as `Circle`.

---

## Overview

This document provides an overview of TypeScript class fundamentals, covering everything from defining classes and access modifiers 
to inheritance and abstract classes. By understanding these core concepts, developers can effectively use TypeScript’s class-based 
object-oriented programming features to create modular, organized, and maintainable code.
