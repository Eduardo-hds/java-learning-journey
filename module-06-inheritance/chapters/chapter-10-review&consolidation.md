# 📘 Chapter 10 — Review & Consolidation

---

# 🧠 1. What this chapter is about

Now we consolidate everything you built and learned in this module into a **clear mental model of inheritance in Java**.

You should leave this module able to:

* design inheritance hierarchies correctly
* implement `extends` structures
* use constructors with `super()`
* override methods properly
* use `super` when needed
* avoid bad design patterns

---

# 🧱 2. The full inheritance mental model

## 🔷 Inheritance in one sentence:

> A child class reuses and extends the behavior of a parent class while adding or customizing functionality.

---

## 🧠 Core structure model:

```text id="final_model"
Parent (Superclass)
   ↑
Child (Subclass)
```

---

# ⚙️ 3. What Java actually does (runtime model)

When you create:

```java id="final_runtime"
Employee e = new Manager();
e.calculateSalary();
```

Java does:

1. Looks at reference type (Employee)
2. Finds actual object (Manager)
3. Executes Manager version of method

👉 This is runtime decision-making (polymorphic behavior at a basic level)

---

# 🧩 4. Key concepts recap

---

## 🔷 1. `extends`

Used to create inheritance:

```java id="extends_final"
class Dog extends Animal
```

---

## 🔷 2. Constructor chaining (`super()`)

* parent constructor runs first
* child constructor runs second

Order is ALWAYS:

> Parent → Child

---

## 🔷 3. Method Overriding

Same method name, different behavior:

* Parent defines structure
* Child customizes behavior

---

## 🔷 4. `super`

Used to:

* call parent constructor → `super()`
* call parent method → `super.method()`
* access parent fields → `super.field`

---

# 🧠 5. When to use inheritance (final rule set)

Use inheritance when:

✔ clear IS-A relationship
✔ shared behavior exists
✔ specialization is needed
✔ hierarchy is logical

---

# ❌ 6. When NOT to use inheritance

Avoid when:

❌ relationship is HAS-A
❌ you are forcing reuse
❌ classes are unrelated
❌ hierarchy becomes deep/complex

---

# ⚠️ 7. Most common mistakes (important review)

### ❌ Mistake 1 — Wrong modeling

Using inheritance where composition should be used.

---

### ❌ Mistake 2 — No overriding

Putting all logic in parent class → no specialization.

---

### ❌ Mistake 3 — Forgetting constructor flow

Not understanding that parent always initializes first.

---

### ❌ Mistake 4 — Confusing reference vs object type

```java
Employee e = new Manager();
```

Reference ≠ object behavior

---

# 🧪 8. Final mental checklist

Before using inheritance, ask:

* Is this an IS-A relationship?
* Do I need shared behavior?
* Do subclasses need different behavior?
* Am I avoiding duplication correctly?
* Am I not forcing hierarchy?

---

# 🧩 9. What you should now be able to do

You should now confidently:

✔ design class hierarchies
✔ implement inheritance in Java
✔ use `super()` correctly
✔ override methods properly
✔ choose inheritance vs composition
✔ build real console-based systems

---

# 🎯 10. Module Completion Summary

You started with:

* no understanding of inheritance

You now have:

* full OOP inheritance model in Java
* practical system design experience
* real-world simulation projects
* constructor + override mastery

---

# 🧾 Final Result

You completed:

> ✔ Module 06 — Inheritance (Java Bootcamp Core Track)