# Chapter 5 — Design Decisions (Abstract Classes vs Interfaces)

---

# 🧠 1. Core Idea of This Chapter

Now we shift from **syntax** to **design thinking**.

The real question is:

> “Should I use an abstract class or an interface in this situation?”

This is where most beginners struggle — not in code, but in **decision making**.

---

# ⚙️ 2. When to Use Abstract Classes

Use an abstract class when you need:

### ✔ Shared state (fields)

### ✔ Shared implementation (code reuse)

### ✔ Strong relationship (is-a hierarchy)

### ✔ Base behavior + enforced rules

---

## Example mental model:

* Animal → Dog, Cat
* Employee → Developer, Manager
* Account → Savings, Checking

These are **natural hierarchies**

---

## Why abstract class fits:

Because they all:

* share data (name, balance, id)
* share behavior (login, sleep, etc.)
* but differ in specific actions

---

# 🧩 3. When NOT to Use Abstract Classes

Avoid abstract classes when:

### ❌ You don’t need shared logic

### ❌ Classes are unrelated

### ❌ You need multiple inheritance behavior

### ❌ You only want to define a “capability”

---

## Example of BAD use:

Forcing unrelated things:

* Car
* User
* DatabaseConnection

They don’t belong in one hierarchy → ❌ bad design

---

# ⚙️ 4. When to Use Interfaces Instead

Use interfaces when you want:

### ✔ A contract (what must be done)

### ✔ Multiple inheritance of behavior type

### ✔ No shared state required

---

## Example:

* Flyable
* Runnable
* Payable

These are not “things”, they are **capabilities**

---

# 🔄 5. Deep Comparison

| Feature        | Abstract Class            | Interface             |
| -------------- | ------------------------- | --------------------- |
| Purpose        | Base class + shared logic | Contract / capability |
| State (fields) | ✔ Yes                     | ❌ No                  |
| Constructors   | ✔ Yes                     | ❌ No                  |
| Inheritance    | Single                    | Multiple              |
| Code reuse     | ✔ High                    | Limited               |
| Flexibility    | Medium                    | High                  |

---

# 🧠 6. Real Decision Rule (VERY IMPORTANT)

Use this rule:

---

## 🟢 Use ABSTRACT CLASS if:

* You can say: **“This is a type of X”**
* You need shared code
* You need shared fields
* You want controlled inheritance

---

## 🔵 Use INTERFACE if:

* You can say: **“This can do X”**
* You only need behavior definition
* You want flexibility
* You expect multiple implementations

---

# 🏗️ 7. Real-World Example

## Abstract Class Example:

```java id="a1x9p3"
abstract class Employee {
    String name;

    void login() {
        System.out.println(name + " logged in");
    }

    abstract void work();
}
```

---

## Interface Example:

```java id="b7k2m8"
interface Payable {
    void calculateSalary();
}
```

A class can do both:

```java id="c4n8q1"
class Developer extends Employee implements Payable {

    @Override
    void work() {
        System.out.println("Writing code");
    }

    @Override
    public void calculateSalary() {
        System.out.println("Salary calculated");
    }
}
```

---

# 🔥 8. Common Mistake (IMPORTANT)

Beginners often:

❌ Use abstract class for everything
❌ Or use interface for everything

Correct thinking:

> Abstract class = structure + shared behavior
> Interface = capability definition

---

# 🌍 9. Mental Model (Very Important)

### Abstract Class = “Family Tree”

* You inherit traits
* You share DNA (fields + logic)
* You belong to a hierarchy

---

### Interface = “Ability Badge”

* You can fly
* You can pay
* You can log
* It does NOT define what you ARE

---

# 🎯 10. Key Takeaways

* Abstract classes are for **hierarchies**
* Interfaces are for **capabilities**
* Abstract classes provide **code reuse**
* Interfaces provide **flexibility**
* Good design depends on correct classification

---

# ✔️ Quick Self-Test

Ask yourself:

1. Is this a “type of something”? → abstract class
2. Is this a “can do something”? → interface
3. Do I need shared fields? → abstract class
4. Do I need multiple inheritance behavior? → interface

---

# ▶️ Next Step

Next we move to:

## Chapter 6 — Guided Practice Systems (Animal, Employee, Shape, Banking)
