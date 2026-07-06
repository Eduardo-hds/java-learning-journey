# Chapter 05 — Interface vs Inheritance (Design Comparison)

---

# 🧩 Why This Chapter Matters

Up to now, you’ve seen two powerful tools:

* **Inheritance (`extends`)**
* **Interfaces (`implements`)**

Both allow reuse and structure — but they solve *very different problems*.

Understanding when to use each is what separates beginner design from professional Java design.

---

# 🔷 1. Inheritance (`extends`)

## 🧠 What it is

Inheritance is used when one class **is a type of another class**.

```java id="inh1"
class Animal {
    void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Barking...");
    }
}
```

---

## 💡 Meaning

Dog **is an** Animal.

So it inherits:

* behavior
* structure
* base logic

---

## 🧠 Why inheritance exists

* reuse code
* create hierarchy
* model natural relationships

---

## ⚠️ Limitation

Java only allows:

> ❌ One class can extend only one class

This creates rigid structure.

---

# 🔷 2. Interfaces (`implements`)

## 🧠 What it is

Interfaces define **capabilities or contracts**.

```java id="int1"
interface PaymentMethod {
    void processPayment(double amount);
}
```

---

## 💡 Meaning

CreditCard **can perform** PaymentMethod behavior.

It is NOT a type hierarchy — it's a capability.

---

## 🧠 Why interfaces exist

* define rules without forcing structure
* allow multiple behaviors
* enable loose coupling

---

## ✔️ Advantage

A class can implement multiple interfaces:

```java id="multi1"
class Robot implements Walkable, Chargeable, Programmable {
}
```

---

# ⚖️ 3. Key Differences (Very Important)

| Feature      | Inheritance | Interface            |
| ------------ | ----------- | -------------------- |
| Keyword      | extends     | implements           |
| Relationship | "is-a"      | "can-do"             |
| Code reuse   | Yes         | No (mostly contract) |
| Multiple use | No          | Yes                  |
| Coupling     | Strong      | Weak                 |
| Flexibility  | Low         | High                 |

---

# 🧠 4. Design Thinking Difference

## Inheritance mindset:

> “What does this object *inherit*?”

Focus:

* structure
* hierarchy
* shared behavior

---

## Interface mindset:

> “What can this object *do*?”

Focus:

* behavior
* capability
* flexibility

---

# 🌍 5. Real-World Example

## Inheritance example:

```java id="real1"
class Vehicle {
    void start() {
        System.out.println("Starting vehicle...");
    }
}

class Car extends Vehicle {
}
```

✔ Car **is a** Vehicle

---

## Interface example:

```java id="real2"
interface Drivable {
    void drive();
}

interface Flyable {
    void fly();
}

class Drone implements Drivable, Flyable {
}
```

✔ Drone **can do** multiple things

---

# 🔥 6. When to Use Each

## ✔ Use inheritance when:

* strong hierarchy exists
* shared base behavior is needed
* relationship is clearly “is-a”

Example:

* Dog → Animal
* Manager → Employee

---

## ✔ Use interfaces when:

* multiple behaviors are needed
* system must be flexible
* implementations may vary
* you want decoupling

Example:

* Payment systems
* Notifications
* Transport modes

---

# ❌ 7. Common Mistakes

### ❌ Overusing inheritance

* leads to deep class trees
* hard to maintain
* rigid architecture

---

### ❌ Using interfaces for everything

* unnecessary complexity
* over-engineering simple systems

---

# 🧠 8. Professional Rule of Thumb

> Prefer interfaces for design flexibility.
> Use inheritance only when there is a strong natural hierarchy.

This is the rule used in most real systems.

---

# 🎯 Core Insight

> Inheritance is about structure.
> Interfaces are about behavior.

---

# 🚀 Next Step

Now that you understand design differences, we move into real application:

> **Chapter 06 — Real-World Design with Interfaces**

Where we will:

* model real systems
* design flexible architectures
* prepare for the final project structure

Proceed when ready.
