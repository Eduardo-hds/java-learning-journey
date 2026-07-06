# Chapter 1 — Introduction to Abstract Classes

---

# 🧠 1. What is an Abstract Class?

An **abstract class** in Java is a class that **cannot be instantiated directly** and is designed to be a **base class for other classes**.

It can contain:

* Abstract methods (no body)
* Concrete methods (with implementation)
* Fields (state)
* Constructors

```java
abstract class Animal {
    String name;

    void eat() {
        System.out.println("Eating...");
    }
}
```

---

# ❓ 2. Why Abstract Classes Exist

Abstract classes exist to solve a real design problem:

> “I want to define a common structure, but force subclasses to complete the behavior.”

Without abstract classes, you would either:

* Duplicate code across classes ❌
* Or create overly generic classes that don’t make sense on their own ❌

So abstract classes provide:

* Shared logic (reuse)
* Enforced rules (structure)
* Base modeling (real-world hierarchy)

---

# ⚙️ 3. How It Works (Conceptual JVM Behavior)

When Java compiles:

### If a class is abstract:

* JVM **prevents instantiation**
* It is treated as an **incomplete blueprint**

```java
Animal a = new Animal(); // ❌ Compile-time error
```

But subclasses work normally:

```java
class Dog extends Animal {
}
```

At runtime:

* JVM builds objects only from **complete classes**
* Abstract class exists only as a **parent reference type**

---

# 🏗️ 4. Abstract Class vs Concrete Class

## Concrete Class

A normal class that can be instantiated:

```java
class Dog {
}
Dog d = new Dog(); // ✅ OK
```

## Abstract Class

Cannot be instantiated:

```java
abstract class Animal {
}
Animal a = new Animal(); // ❌ NOT allowed
```

---

# 🎯 5. When to Use Abstract Classes

Use abstract classes when:

✔ You want to share **common code**
✔ You want to enforce a **base structure**
✔ Classes are strongly related (is-a relationship)
✔ You expect subclasses to reuse behavior

### Example:

* Animal → Dog, Cat
* Employee → Developer, Manager
* Account → Savings, Checking

---

# 🚫 6. When NOT to Use Abstract Classes

Avoid abstract classes when:

❌ You only need a contract (use interface instead)
❌ Classes are not strongly related
❌ You need multiple inheritance behavior
❌ You don’t share logic between subclasses

---

# 🔄 7. Abstract Class vs Interface (Deep Comparison)

| Feature               | Abstract Class       | Interface                 |
| --------------------- | -------------------- | ------------------------- |
| Purpose               | Shared base behavior | Contract definition       |
| State (variables)     | Yes                  | No (only constants)       |
| Constructors          | Yes                  | No                        |
| Method implementation | Yes                  | Limited (default methods) |
| Inheritance           | Single               | Multiple                  |
| Relationship          | "is-a base type"     | "can-do capability"       |

---

# 🌍 Real-World Mental Model

Think of it like this:

### Abstract Class = “Blueprint with partial building”

* Some rooms already built
* Some rooms must be completed

### Interface = “Contract”

* No building
* Just rules you must follow

---

# 🧪 Mini Concept Check (No coding yet)

Answer mentally:

1. Can you create an object from an abstract class?
2. Why would Animal be abstract but Dog is not?
3. What happens if a subclass does NOT implement required abstract methods?

---

# ✔️ Key Takeaways

* Abstract classes cannot be instantiated
* They define shared structure + behavior
* They enforce rules for subclasses
* They are used for strong hierarchical modeling
* They differ from interfaces by allowing state and shared logic

---

# ▶️ Next Step

Next we move to:

## Chapter 2 — Abstract Methods & Partial Abstraction
