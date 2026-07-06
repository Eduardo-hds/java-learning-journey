# Chapter 3 — Abstract Class Behavior (Concrete Methods + Shared Logic)

---

# 🧠 1. Key Idea of This Chapter

Abstract classes are not only about forcing rules.

They also solve a second problem:

> “How do we reuse common logic across multiple related classes?”

This is where **concrete methods inside abstract classes** become important.

---

# ⚙️ 2. What Are Concrete Methods in Abstract Classes?

An abstract class can contain **normal methods with full implementation**.

```java id="a1b2c3"
abstract class Animal {

    abstract void makeSound();

    void sleep() {
        System.out.println("Sleeping...");
    }
}
```

Here:

* `makeSound()` → must be implemented (abstract)
* `sleep()` → already implemented (concrete)

---

# ❓ 3. Why This Exists

Without this feature, you would:

* Repeat the same code in every subclass ❌
* Or create utility classes that break OOP structure ❌

Instead, abstract classes allow:

✔ Code reuse
✔ Shared behavior
✔ Consistent logic across subclasses

---

# ⚙️ 4. How It Works Internally (Conceptual JVM View)

* Abstract class is loaded normally by JVM
* Concrete methods are stored in the parent class bytecode
* Subclasses inherit them automatically
* No duplication happens in memory logic (method sharing via inheritance)

So:

> Only one implementation exists (in the parent class)

---

# 🧩 5. Example — Shared Behavior in Practice

```java id="b9d8e1"
abstract class Animal {

    String name;

    abstract void makeSound();

    void sleep() {
        System.out.println(name + " is sleeping...");
    }
}
```

```java id="c4f7a2"
class Dog extends Animal {

    Dog(String name) {
        this.name = name;
    }

    @Override
    void makeSound() {
        System.out.println(name + " says: Bark!");
    }
}
```

Usage:

```java id="d8e2f1"
Dog dog = new Dog("Rex");

dog.makeSound();
dog.sleep();
```

Output:

```
Rex says: Bark!
Rex is sleeping...
```

---

# 🔥 6. Why This Is Powerful

Without abstract class shared methods:

You would do this in every class:

```java
System.out.println(name + " is sleeping...");
```

That causes:

* Duplication ❌
* Hard maintenance ❌
* Inconsistent behavior ❌

With abstract class:

* One place to define shared logic ✔
* All subclasses automatically benefit ✔

---

# 🏗️ 7. Real-World Modeling Example

Think of a system:

### Employee System

All employees:

* Have a name
* Have a login process
* Have a work routine

But:

* Developer writes code
* Manager manages teams

```java id="e1k2p9"
abstract class Employee {

    String name;

    void login() {
        System.out.println(name + " logged in.");
    }

    abstract void work();
}
```

---

# 🎯 8. When to Use Concrete Methods in Abstract Classes

Use them when:

✔ Behavior is shared by all subclasses
✔ Logic does NOT change across subclasses
✔ You want to avoid duplication
✔ You want consistent system behavior

---

# 🚫 9. When NOT to Use Them

Avoid when:

❌ Behavior changes significantly per subclass
❌ Logic is not universal
❌ You are forcing unrelated classes into one hierarchy

---

# 🔄 10. Abstract Class Strategy Pattern (Conceptual Awareness Only)

(Not implementing patterns, just understanding)

Sometimes:

* Abstract class = shared structure
* Concrete methods = reusable workflow steps

This creates a **consistent skeleton behavior** across subclasses.

---

# 🧠 Key Comparison

| Feature           | Abstract Method      | Concrete Method |
| ----------------- | -------------------- | --------------- |
| Has body          | ❌ No                 | ✅ Yes           |
| Purpose           | Force implementation | Reuse logic     |
| Override required | Yes                  | Optional        |
| Flexibility       | High                 | Shared behavior |

---

# 🌍 Mental Model

Think of an abstract class like:

> A partially built machine

* Some parts are missing (abstract methods)
* Some parts are already assembled (concrete methods)

---

# ✔️ Key Takeaways

* Abstract classes can contain full methods
* Concrete methods provide shared logic
* This avoids duplication across subclasses
* Abstract methods + concrete methods = partial abstraction power
* This is essential for clean OOP architecture

---

# ▶️ Next Step

Next we move to:

## Chapter 4 — Inheritance with Abstract Classes (Constructor behavior + overriding rules)
