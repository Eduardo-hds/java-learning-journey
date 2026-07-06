# 📘 Chapter 6 — Class Hierarchy Design (When to use / avoid inheritance)

---

# 🧠 1. What this chapter is about

Now you will learn something more important than syntax:

> How to design inheritance correctly.

Most bugs in OOP don’t come from code — they come from **bad hierarchy design**.

You will learn:

* When inheritance makes sense
* When it should NOT be used
* How to avoid bad class structures
* How to think like a system designer

---

# ⚙️ 2. The golden rule of inheritance

> Use inheritance only when there is a clear **IS-A relationship**

If you cannot say:

> “X is a Y”

Then inheritance is probably wrong.

---

# 🧱 3. Good inheritance examples

These are correct:

* Dog **is an** Animal
* Manager **is an** Employee
* Car **is a** Vehicle
* Circle **is a** Shape

✔ These represent real hierarchies

---

# ❌ 4. Bad inheritance examples

These look tempting but are WRONG:

* Car extends Engine ❌
* User extends Database ❌
* Order extends List ❌
* House extends Door ❌

---

## 🧠 Why they are wrong?

Because:

* They are NOT “is-a”
* They are “has-a”
* They represent **composition**, not inheritance

---

# ⚙️ 5. Inheritance vs Composition (critical thinking)

---

## 🔷 Inheritance (IS-A)

Used when:

* shared behavior exists
* hierarchy is natural
* specialization is needed

Example:

```text id="inherit_tree"
Animal
 ├── Dog
 └── Cat
```

---

## 🔶 Composition (HAS-A)

Used when:

* object is made of parts
* no hierarchy exists

Example:

```text id="compose_tree"
Car
 ├── Engine
 ├── Wheels
 └── GPS
```

---

# 🧠 6. Real-world modeling examples

---

## ✔ GOOD design

### Employee system

* Employee (base class)
* Manager extends Employee
* Developer extends Employee

Why?

* All share salary, name, work()

---

## ❌ BAD design

* Employee extends Salary ❌
* Developer extends Keyboard ❌

These break logic.

---

# ⚙️ 7. Signs your inheritance design is WRONG

If you see any of these:

### 🚨 1. “Just to reuse code”

You are forcing inheritance incorrectly.

---

### 🚨 2. Classes are unrelated

If connection is weak → don’t use inheritance.

---

### 🚨 3. Too deep hierarchy

```text id="bad_deep"
A → B → C → D → E
```

Problem:

* hard to debug
* fragile design
* unclear structure

---

### 🚨 4. Child does not behave like parent

If subclass breaks expectations → design is wrong.

---

# 💡 8. Better alternative: Composition

Instead of:

```java
class Car extends Engine ❌
```

Use:

```java id="composition_example"
class Car {
    Engine engine;
}
```

✔ Cleaner
✔ More flexible
✔ Easier to maintain

---

# 🧠 9. Mental model shift

Stop thinking:

> “How do I reuse code?”

Start thinking:

> “What is the relationship between these objects?”

---

# ⚠️ 10. Common mistakes

### Mistake 1: Using inheritance everywhere

Not everything is a hierarchy.

---

### Mistake 2: Confusing “has-a” with “is-a”

This is the most common design error.

---

### Mistake 3: Over-engineering early

Don’t build complex hierarchies too soon.

---

# 🧪 Quick check

Ask yourself:

* Is Dog really an Animal? ✔
* Is Manager really an Employee? ✔
* Is Engine really a Car? ❌

If you can answer correctly → you understand design logic.

---

# ✔️ Next Step

Now we move from theory → practice systems:

# 👉 Chapter 7 — Guided Practice Systems (Animal, Employee, Vehicle, Shape)