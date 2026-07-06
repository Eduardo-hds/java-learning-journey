# 📘 Chapter 9 — Final Project (Role-Based System)

---

# 🧠 1. What this phase is about

Now you will build a **real structured OOP system using inheritance**.

This is not just practice anymore — this is integration of everything:

* inheritance hierarchy
* constructors + `super()`
* method overriding
* class design decisions
* runtime behavior understanding

But we will still build it **progressively**, not all at once.

---

# 🎯 Project: Role-Based Employee System

---

## 🧱 Core Idea

We simulate different employee roles in a company.

All roles share common data, but behave differently.

---

# 📦 Project Structure (must follow)

```text id="proj_struct_06"
src/
 ├── Main.java
 ├── model/
 │    ├── Employee.java
 │    ├── Manager.java
 │    ├── Developer.java
 │    ├── Intern.java
 ├── service/
 └── util/
```

---

# 🧠 2. Base Class Design — Employee

---

## 🎯 What ALL employees share:

Think first:

* name
* base salary
* role title

---

## 💡 Behavior:

Every employee must have:

```java id="emp_base_method"
calculateSalary()
```

BUT each role will behave differently.

---

# 🧩 3. Child Classes

---

## 👔 Manager

* higher bonus
* manages team
* highest salary multiplier

---

## 💻 Developer

* bonus based on performance
* medium salary increase

---

## 🎓 Intern

* small fixed stipend
* limited salary growth

---

# ⚙️ 4. Required OOP concepts

You MUST use:

✔ inheritance (`extends`)
✔ constructor chaining (`super()`)
✔ method overriding (`calculateSalary`)
✔ runtime polymorphism (via base reference)

---

# 🧪 5. Build Plan (VERY IMPORTANT)

We build in steps:

---

## 🟢 Step 1 — Employee class only

Create:

* fields
* constructor
* base method `calculateSalary()`

DO NOT create children yet.

---

## 🟡 Step 2 — Manager class

* extend Employee
* override salary logic
* add bonus behavior

---

## 🟡 Step 3 — Developer class

* extend Employee
* override salary logic differently

---

## 🟡 Step 4 — Intern class

* simplest logic
* small salary behavior

---

## 🔵 Step 5 — Main testing

Create:

```java id="test_main_proj"
Employee e1 = new Manager(...);
Employee e2 = new Developer(...);
Employee e3 = new Intern(...);
```

Call:

```java id="call_salary"
e1.calculateSalary();
e2.calculateSalary();
e3.calculateSalary();
```

---

# 🧠 6. Key design rule

You MUST follow:

> Same method name, different behavior

This is the core of inheritance usage in real systems.

---

# ⚠️ 7. Common mistakes (DO NOT DO THESE)

* putting all logic in Employee (no overriding)
* using `if (role == ...)` instead of inheritance
* forgetting `super()` in constructors
* not using polymorphism (base reference usage)

---

# 💡 8. Expected learning outcome

After this project you should understand:

* how inheritance is used in real systems
* why overriding is powerful
* how constructors flow in hierarchy
* how Java decides which method to execute

---

# 🧪 9. Final Challenge Rule

You are NOT allowed to:

* flatten all logic into one class
* avoid inheritance
* skip overriding

You MUST use full hierarchy design.

---

# ✔️ Next Step

Once you finish building, we move to final evaluation and consolidation:

# 👉 Chapter 10 — Review & Consolidation
