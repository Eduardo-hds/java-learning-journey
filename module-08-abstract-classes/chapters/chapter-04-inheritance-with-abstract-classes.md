# Chapter 4 — Inheritance with Abstract Classes

---

# 🧠 1. Core Idea of This Chapter

Now we combine two concepts:

* **Inheritance**
* **Abstract classes**

This is where abstract classes become truly powerful:

> They define a base structure AND enforce behavior across a class hierarchy.

---

# ⚙️ 2. Extending Abstract Classes

A concrete class can extend an abstract class using `extends`.

```java id="a1k9d2"
abstract class Animal {

    abstract void makeSound();

    void sleep() {
        System.out.println("Sleeping...");
    }
}
```

```java id="b7m2q8"
class Dog extends Animal {

    @Override
    void makeSound() {
        System.out.println("Bark");
    }
}
```

---

# ❓ 3. Why This Works

Even though `Animal` is abstract:

* It still defines a **base type**
* It still provides **shared behavior**
* It still forces **implementation rules**

So inheritance here is:

> “inherit structure + inherit shared logic + complete missing parts”

---

# ⚙️ 4. Constructor Behavior in Abstract Classes

Yes — abstract classes **can have constructors**.

But they are NEVER called directly.

They are called through subclass construction.

---

## Example:

```java id="c9n4t1"
abstract class Animal {

    String name;

    Animal(String name) {
        this.name = name;
        System.out.println("Animal constructor executed");
    }

    abstract void makeSound();
}
```

```java id="d3p8x6"
class Dog extends Animal {

    Dog(String name) {
        super(name); // calls Animal constructor
        System.out.println("Dog constructor executed");
    }

    @Override
    void makeSound() {
        System.out.println(name + " barks");
    }
}
```

---

## Usage:

```java id="e5q1z9"
Dog dog = new Dog("Rex");
```

### Output:

```
Animal constructor executed
Dog constructor executed
```

---

# 🧠 5. What is Happening Internally (JVM Concept)

When you do:

```java
new Dog("Rex");
```

JVM does this:

1. Allocate memory for `Dog`
2. Call `Dog constructor`
3. First line is `super(name)`
4. JVM executes `Animal constructor`
5. Then returns to `Dog constructor`

So:

> Abstract class constructor is ALWAYS part of object creation chain

---

# 🧩 6. Method Overriding in Abstract Hierarchies

Overriding works the same as normal inheritance:

```java id="f8r2k4"
class Cat extends Animal {

    Cat(String name) {
        super(name);
    }

    @Override
    void makeSound() {
        System.out.println(name + " meows");
    }
}
```

Rules:

* Must implement abstract methods
* Can override concrete methods (optional)
* Must respect method signature

---

# 🔥 7. Why Abstract + Inheritance Together Is Powerful

You get 3 layers:

### 1. Structure (Abstract Class)

* Defines rules

### 2. Shared Behavior

* Avoid duplication

### 3. Specialization (Subclasses)

* Each class customizes behavior

---

# 🏗️ 8. Real-World Example

### Employee System

```java id="g1h3k7"
abstract class Employee {

    String name;

    Employee(String name) {
        this.name = name;
    }

    void clockIn() {
        System.out.println(name + " clocked in");
    }

    abstract void work();
}
```

```java id="h6j9m2"
class Developer extends Employee {

    Developer(String name) {
        super(name);
    }

    @Override
    void work() {
        System.out.println(name + " writes code");
    }
}
```

```java id="i4k8p1"
class Manager extends Employee {

    Manager(String name) {
        super(name);
    }

    @Override
    void work() {
        System.out.println(name + " manages team");
    }
}
```

---

# 🎯 9. When to Use This Structure

Use abstract inheritance when:

✔ You have a strong base concept (Animal, Employee, Shape)
✔ You need shared fields and logic
✔ You need enforced behavior
✔ You want clean hierarchy design

---

# 🚫 10. When NOT to Use It

Avoid when:

❌ Classes are unrelated
❌ No shared behavior exists
❌ You only need a contract (interface is better)
❌ You are forcing hierarchy just to reuse code

---

# 🔄 11. Abstract Class vs Interface (Deepened Understanding)

| Feature        | Abstract Class          | Interface             |
| -------------- | ----------------------- | --------------------- |
| Constructor    | ✔ Yes                   | ❌ No                  |
| State (fields) | ✔ Yes                   | ❌ No (constants only) |
| Inheritance    | Single                  | Multiple              |
| Purpose        | Shared base + structure | Contract / capability |
| Real use       | Hierarchies             | Behavior types        |

---

# 🌍 Mental Model

Think of:

### Abstract Class = “Parent blueprint with unfinished parts”

* Gives identity
* Gives partial functionality
* Forces completion

### Inheritance = “Specialized versions of that blueprint”

* Dog is a type of Animal
* Developer is a type of Employee

---

# ✔️ Key Takeaways

* Abstract classes participate fully in inheritance
* They can have constructors (called via `super`)
* Subclasses MUST complete abstract methods
* They combine structure + reuse + enforcement
* JVM builds objects through constructor chain

---

# ▶️ Next Step

Next we move to:

## Chapter 5 — Design Decisions (When to use vs NOT use abstract classes + deeper comparison with interfaces)
