# Chapter 2 — Abstract Methods & Partial Abstraction

---

# 🧠 1. What is an Abstract Method?

An **abstract method** is a method that:

* Has **no body (no implementation)**
* Only defines the **signature**
* Must be implemented by subclasses

```java
abstract class Animal {

    abstract void makeSound();
}
```

Here:

* `makeSound()` has no `{ }`
* It only defines *what must exist*, not *how it works*

---

# ❓ 2. Why Abstract Methods Exist

Abstract methods exist to enforce rules:

> “Every subclass MUST implement this behavior, but each one can do it differently.”

Example:

* Dog → bark()
* Cat → meow()
* Cow → moo()

They all “make sound”, but in different ways.

Without abstract methods:

* You would forget to implement important behavior ❌
* Or use empty methods (bad design) ❌

---

# ⚙️ 3. How It Works Internally (Conceptual JVM View)

When Java compiles:

### Abstract method rule:

* JVM does NOT assign memory implementation for it
* It acts like a **required contract entry**

If a subclass fails to implement it:

```java
class Dog extends Animal {
}
```

❌ Compile-time error:

> Dog must implement abstract method makeSound()

So enforcement happens at **compile time**, not runtime.

---

# 🧩 4. Partial Abstraction (Very Important Concept)

An abstract class can have:

### ✔ Abstract methods (no body)

### ✔ Concrete methods (with body)

This is called:

> **Partial Abstraction**

Example:

```java
abstract class Animal {

    abstract void makeSound();

    void sleep() {
        System.out.println("Sleeping...");
    }
}
```

Meaning:

* Part of the class is defined (sleep behavior)
* Part must be completed (makeSound)

---

# 🏗️ 5. Example in Practice

```java
abstract class Animal {

    abstract void makeSound();

    void sleep() {
        System.out.println("Sleeping...");
    }
}

class Dog extends Animal {

    @Override
    void makeSound() {
        System.out.println("Bark");
    }
}
```

Usage:

```java
Dog dog = new Dog();
dog.makeSound(); // Bark
dog.sleep();     // Sleeping...
```

---

# 🔥 6. What Happens If You Don’t Implement?

```java
class Cat extends Animal {
}
```

❌ Result:

> Class Cat must implement inherited abstract method makeSound()

Java forces correctness at compile time.

---

# 🎯 7. When to Use Abstract Methods

Use abstract methods when:

✔ You want to enforce behavior
✔ You want different implementations per subclass
✔ The method is logically required for all subclasses

---

# 🚫 8. When NOT to Use Abstract Methods

Avoid abstract methods when:

❌ Behavior is optional
❌ You already have a good default implementation
❌ The method does not apply to all subclasses

---

# 🔄 9. Abstract Method vs Normal Method

| Feature       | Abstract Method | Normal Method    |
| ------------- | --------------- | ---------------- |
| Body          | ❌ No            | ✅ Yes            |
| Must override | ✅ Yes           | ❌ Optional       |
| Purpose       | Force structure | Provide behavior |

---

# 🌍 Real-World Analogy

Think of a contract:

### Abstract Method = “You MUST do this”

* Every employee must “calculate salary”
* Every shape must “calculate area”

But how they do it is different.

---

# 🧠 Key Idea Summary

* Abstract methods define **what must exist**
* Subclasses define **how it works**
* They enforce strict structure
* They enable polymorphism later
* They are core to clean OOP design

---

# ✔️ Mini Check (Mental Exercise)

1. Can an abstract method have a body?
2. Who is responsible for implementing abstract methods?
3. What happens if a subclass ignores them?
4. What is “partial abstraction”?

---

# ▶️ Next Step

Next we move to:

## Chapter 3 — Abstract Class Behavior (Concrete Methods + Shared Logic)
