# 📚 Day 21 — SOLID Design Principles in Software Development

## 🎯 Why I Studied This Topic

As a Computer Science student learning software development, writing code that works is only the first step. I also need to write code that is easy to understand, test, maintain, and extend.

As projects grow, poorly structured code can become difficult to modify. A small change in one part of the application may unexpectedly break another part.

**SOLID** is a set of five software design principles that helps developers design more maintainable, flexible, and testable object-oriented systems.

The five principles are:

- **S** — Single Responsibility Principle (SRP)
- **O** — Open-Closed Principle (OCP)
- **L** — Liskov Substitution Principle (LSP)
- **I** — Interface Segregation Principle (ISP)
- **D** — Dependency Inversion Principle (DIP)

These principles are associated with Robert C. Martin, also known as Uncle Bob. The Liskov Substitution Principle is named after computer scientist Barbara Liskov.

---

# 1. Single Responsibility Principle (SRP)

## Definition

A class, module, or function should have **one responsibility, or one reason to change**.

This does not necessarily mean that a class can contain only one method. It means its methods should belong to one cohesive responsibility.

### ❌ Example: One class doing too much

```javascript
class Animal {
  constructor(name, feedingType, soundMade) {
    this.name = name;
    this.feedingType = feedingType;
    this.soundMade = soundMade;
  }

  showName() {
    console.log(`The animal is ${this.name}`);
  }

  makeSound() {
    console.log(`${this.name} ${this.soundMade}s`);
  }

  showFeedingType() {
    console.log(`${this.name} is a ${this.feedingType}`);
  }
}
```

This class handles several different concerns: displaying the animal's name, describing its sound, and describing its feeding type.

As the application grows, these responsibilities may change for different reasons.

### ✅ Better approach

Separate distinct responsibilities when doing so improves cohesion and maintainability.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  showName() {
    console.log(`The animal is ${this.name}`);
  }
}

class AnimalSound {
  constructor(name, soundMade) {
    this.name = name;
    this.soundMade = soundMade;
  }

  makeSound() {
    console.log(`${this.name} ${this.soundMade}s`);
  }
}

class AnimalFeeding {
  constructor(name, feedingType) {
    this.name = name;
    this.feedingType = feedingType;
  }

  showFeedingType() {
    console.log(`${this.name} is a ${this.feedingType}`);
  }
}
```

### CS lesson

A class that handles unrelated responsibilities becomes harder to modify and test.

**Practical application:** In a backend application, avoid making one controller responsible for request validation, database queries, business logic, email delivery, and response formatting. Separate responsibilities where appropriate.

---

# 2. Open-Closed Principle (OCP)

## Definition

Software entities should be **open for extension but closed for modification**.

This means we should be able to introduce new behavior without repeatedly changing stable, existing code.

### ❌ Example: Modifying a switch statement for every new type

```javascript
class Animal {
  constructor(name, type) {
    this.name = name;
    this.type = type;
  }

  getSpeed() {
    switch (this.type) {
      case "cheetah":
        return 130;
      case "lion":
        return 80;
      case "elephant":
        return 40;
      default:
        throw new Error("Unsupported animal type");
    }
  }
}
```

Every time a new animal type is added, the `getSpeed()` method must be modified.

A `switch` statement does not automatically violate OCP, but this particular design makes adding new types require changes to existing logic.

### ✅ Better approach: Use polymorphism

```javascript
class Animal {
  constructor(name, speed) {
    this.name = name;
    this.speed = speed;
  }

  getSpeed() {
    return this.speed;
  }
}

const cheetah = new Animal("Cheetah", 130);
const lion = new Animal("Lion", 80);
const elephant = new Animal("Elephant", 40);

console.log(cheetah.getSpeed());  // 130
console.log(lion.getSpeed());     // 80
console.log(elephant.getSpeed()); // 40
```

Here, the speed is supplied as data rather than being hardcoded into a conditional method. New animals can be created without modifying `getSpeed()`.

For more complex behavior, separate strategy objects or subclasses can provide different implementations.

### CS lesson

Design systems so that new requirements can be accommodated without unnecessarily rewriting existing, reliable code.

**Practical application:** A payment system could support new payment providers through a common interface instead of adding more provider-specific conditions throughout the codebase.

---

# 3. Liskov Substitution Principle (LSP)

## Definition

Objects of a subtype should be usable wherever objects of the parent type are expected **without breaking the expected behavior of the program**.

In simple terms, a subclass should honor the contract of its parent type.

### ✅ Example: Correct substitution

```javascript
class Animal {
  makeSound() {
    console.log("The animal makes a sound");
  }
}

class Dog extends Animal {
  makeSound() {
    console.log("The dog barks");
  }
}

class Cat extends Animal {
  makeSound() {
    console.log("The cat meows");
  }
}

function makeAnimalSound(animal) {
  animal.makeSound();
}

makeAnimalSound(new Dog()); // The dog barks
makeAnimalSound(new Cat()); // The cat meows
```

Both `Dog` and `Cat` can be passed to `makeAnimalSound()` because each supports the expected `makeSound()` behavior.

### ❌ Example: Breaking the expected contract

Imagine a parent class requires a method called `makeSound()`, but a subclass overrides it by throwing an error or does something incompatible with what callers expect.

That subclass may technically inherit from the parent, but it cannot safely replace it in every context.

### CS lesson

Inheritance is not only about sharing code. A subtype must preserve the behavioral expectations of the type it extends.

**Practical application:** If different payment providers implement a shared `PaymentProcessor` contract, each implementation must behave according to that contract rather than unexpectedly breaking the caller's assumptions.

---

# 4. Interface Segregation Principle (ISP)

## Definition

Clients should not be forced to depend on methods or interfaces they do not use.

Instead of creating one large interface containing unrelated operations, separate it into smaller, more specific contracts.

JavaScript does not have traditional class-based interfaces built into its syntax, but the principle can still be applied through object shapes, classes, and composition.

### ❌ Example: A class with irrelevant methods

```javascript
class Animal {
  eat() {
    console.log("Eating");
  }

  swim() {
    console.log("Swimming");
  }

  fly() {
    console.log("Flying");
  }
}
```

If every animal inherits all these methods, a fish may have a `fly()` method and a bird may have a `swim()` method even when those operations are unsupported.

### ✅ Better approach: Separate capabilities

```javascript
class Swimmer {
  swim() {
    console.log("Swimming");
  }
}

class Flyer {
  fly() {
    console.log("Flying");
  }
}

class Fish extends Swimmer {
  eat() {
    console.log("Eating");
  }
}

class Bird extends Flyer {
  eat() {
    console.log("Eating");
  }
}
```

Now each class receives only the capability it needs.

For a larger application, composition or smaller interfaces can provide this separation without forcing unrelated classes into an inheritance hierarchy.

### CS lesson

A component should depend only on the functionality relevant to its job.

**Practical application:** A read-only reporting service should not be forced to implement database write operations if it never needs to modify data.

---

# 5. Dependency Inversion Principle (DIP)

## Definition

The Dependency Inversion Principle states:

1. High-level modules should not depend directly on low-level modules. Both should depend on abstractions.
2. Abstractions should not depend on implementation details. Implementation details should depend on abstractions.

In simpler terms, important business logic should not be tightly coupled to a particular technical implementation.

### ❌ Example: Tightly coupled code

```javascript
class MySQLDatabase {
  save(data) {
    console.log("Saving data to MySQL:", data);
  }
}

class UserService {
  constructor() {
    this.database = new MySQLDatabase();
  }

  createUser(user) {
    this.database.save(user);
  }
}
```

`UserService` directly creates a `MySQLDatabase`. Changing the storage implementation may require changing the service itself.

### ✅ Better approach: Inject the dependency

```javascript
class UserService {
  constructor(database) {
    this.database = database;
  }

  createUser(user) {
    this.database.save(user);
  }
}

class MySQLDatabase {
  save(data) {
    console.log("Saving data to MySQL:", data);
  }
}

class InMemoryDatabase {
  save(data) {
    console.log("Saving data in memory:", data);
  }
}

const database = new MySQLDatabase();
const userService = new UserService(database);

userService.createUser({ name: "Alex" });
```

`UserService` now receives its database dependency instead of creating a specific database implementation itself.

Both database implementations provide the expected `save()` operation, so the service can work with either one.

This example demonstrates **dependency injection**, a technique that can help implement the Dependency Inversion Principle. The principle and the technique are related, but they are not the same thing.

### CS lesson

Depending on an abstraction or expected contract makes components easier to test and change.

**Practical application:** In a Node.js backend, inject a repository, email service, or payment provider into the service that needs it instead of tightly coupling business logic to a particular implementation.

---

# 🧩 6. Comparing the Five SOLID Principles

| Principle | Main idea | Problem it helps prevent |
|---|---|---|
| SRP | One cohesive responsibility | Classes with unrelated reasons to change |
| OCP | Extend behavior without repeatedly modifying stable code | Fragile conditional logic |
| LSP | Subtypes preserve parent contracts | Unexpected behavior from subclasses |
| ISP | Keep interfaces small and focused | Unnecessary dependencies on unused methods |
| DIP | Depend on abstractions, not concrete details | Tightly coupled modules |

### Easy way to remember

- **S — Single:** Keep responsibilities focused.
- **O — Open:** Make extension possible.
- **L — Liskov:** Subtypes must remain substitutable.
- **I — Interface:** Keep contracts specific.
- **D — Dependency:** Depend on abstractions.

---

# 🏗️ 7. How SOLID Helps in Real Software Projects

Imagine I am building a full-stack application using the MERN stack.

Without careful design, a backend route might handle everything:

```text
HTTP Request
     ↓
Validation
     ↓
Business Logic
     ↓
Database Query
     ↓
Email Delivery
     ↓
HTTP Response
```

As the application grows, this can make the route difficult to test and maintain.

A more modular design could be:

```text
Client Request
      ↓
Controller
      ↓
Service
      ↓
Repository
      ↓
Database
```

Additional components, such as an email service, can be injected into the service when needed.

- **Controller:** Handles HTTP request and response concerns.
- **Service:** Contains application or business logic.
- **Repository:** Encapsulates data access.
- **Database:** Stores persistent information.

This is one possible architecture, not a mandatory structure for every project. SOLID helps guide the boundaries between components, but the appropriate design depends on the application's size and requirements.

---

# ⚠️ 8. SOLID Does Not Mean Creating More Classes Everywhere

One important practical lesson is that following design principles should not become an excuse for unnecessary abstraction.

For example, if a small function performs one simple task, it may not need a separate class or elaborate inheritance hierarchy.

Overengineering can create:

- Too many files and abstractions
- More complexity than the problem requires
- Difficult navigation
- Unnecessary indirection
- More code to maintain

The goal is not to maximize the number of classes.

The goal is to make code easier to understand, test, and change.

> **Use SOLID to manage real complexity, not to create complexity where none exists.**

---

# 💻 9. What I Should Apply in My Own Projects

As a CS student learning full-stack development, I can apply these principles incrementally.

### In React

- Keep components focused on clear responsibilities.
- Extract reusable logic when it genuinely improves clarity.
- Pass dependencies and behavior through props when appropriate.
- Avoid components that manage too many unrelated concerns.

### In Node.js and Express

- Keep HTTP handling separate from business logic when useful.
- Separate data access from application rules when the project warrants it.
- Inject external services to make testing and replacement easier.
- Keep modules focused and avoid unnecessary coupling.

### In MongoDB applications

- Avoid mixing database-specific operations throughout the entire application.
- Use a repository or data-access layer when it meaningfully improves separation.
- Keep business rules from becoming inseparable from database implementation details.

### During code reviews

Ask myself:

1. Does this module have unrelated responsibilities?
2. Can I add a new behavior without rewriting stable code?
3. Do subclasses preserve the expected behavior of their parent?
4. Am I forcing components to depend on functionality they don't need?
5. Can I replace a dependency without rewriting the business logic?

---

# 📌 Key Takeaways

- SOLID is a collection of five design principles for maintainable object-oriented software.
- SRP encourages one cohesive responsibility per module or class.
- OCP encourages extension without unnecessary modification of stable code.
- LSP requires subtypes to preserve the behavioral expectations of their parent types.
- ISP encourages small, focused interfaces and contracts.
- DIP reduces coupling by making high-level and low-level modules depend on abstractions.
- Dependency injection is one technique for providing dependencies from outside a component.
- SOLID can improve testability, flexibility, and maintainability.
- SOLID principles are guidelines, not rigid rules that require the same architecture in every project.
- More classes and abstractions do not automatically mean better code.
- The goal is to make future changes safer and easier.

---

# 🔄 One-Minute Revision

```text
SOLID
│
├── S: Single Responsibility
│      One cohesive responsibility
│
├── O: Open-Closed
│      Extend behavior without unnecessary modification
│
├── L: Liskov Substitution
│      Subtypes preserve expected behavior
│
├── I: Interface Segregation
│      Depend only on relevant contracts
│
└── D: Dependency Inversion
       Depend on abstractions, not concrete details
```

---

# 🎯 Final Takeaway

> **Good software is not only code that works today. It is code that can be understood, tested, and changed safely tomorrow.**

SOLID gives me a way to think about software structure before a project becomes difficult to maintain.

As I continue building full-stack projects, I should focus not only on getting features working, but also on creating clear responsibilities, reducing unnecessary coupling, and choosing abstractions that solve real problems.

---

# 🔗 Source / Reference

**Article:** *SOLID Design Principles in Software Development*  
**Author:** Kolade Chris  
**Source:** Article provided for Day 21 learning notes  
**Main Topics:** SRP, OCP, LSP, ISP, and DIP
