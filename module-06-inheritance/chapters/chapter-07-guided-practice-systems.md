# 📘 Chapter 7 — Guided Practice Systems

---

# 🧠 1. What this chapter is about

Now we apply everything you learned so far:

* inheritance
* `extends`
* constructors + `super()`
* method overriding
* `super` usage
* class hierarchy design

But in a controlled way — step by step systems.

We will NOT jump to full solutions. We will build each system gradually.

---

# 🧩 SYSTEM 1 — Animal Hierarchy

---

## 🎯 Goal

Model a simple hierarchy:

* Animal (base class)
* Dog (child)
* Cat (child)

---

## 🧱 Step 1 — What should ALL animals have?

Think:

* name
* age
* eat()
* sleep()

This goes in the parent class.

---

## 🐾 Your task (conceptual)

Before coding anything:

👉 Identify:

* What is shared?
* What is specific?

---

## 🧠 Expected design

### Shared (Animal)

* name
* age
* eat()
* sleep()

### Specific

* Dog → bark()
* Cat → meow()

---

## ⚙️ Step 2 — Behavior thinking

Ask:

> Should bark() exist in Animal?

❌ No → only Dog

---

## 🧪 Exercise 1 (you build next step)

Create:

* Animal class with shared fields
* Dog extends Animal
* Cat extends Animal

BUT:

* do NOT implement everything yet
* focus on structure only

---

# 🧩 SYSTEM 2 — Employee System

---

## 🎯 Goal

Build a real-world hierarchy:

* Employee (base)
* Manager (child)
* Developer (child)

---

## 🧠 Shared behavior:

* name
* salary
* work()

---

## 💡 Special behavior:

* Manager → manages team
* Developer → writes code

---

## ⚙️ Design question

Should Manager extend Developer?

❌ No.

Why?

* both are Employees
* not related to each other directly

Correct:

```text id="emp_tree"
Employee
 ├── Manager
 └── Developer
```

---

## 🧪 Exercise 2

You will later implement:

* salary calculation differences
* method overriding of work()

---

# 🧩 SYSTEM 3 — Vehicle System

---

## 🎯 Goal

Model different vehicles:

* Vehicle (base)
* Car
* Motorcycle

---

## 🧠 Shared behavior:

* start()
* stop()

---

## 💡 Special behavior:

* Car → has doors
* Motorcycle → has helmet requirement

---

## ⚙️ Key idea

Even if behavior is similar, output may differ → override methods.

---

# 🧩 SYSTEM 4 — Shape System

---

## 🎯 Goal

Introduce polymorphic-like thinking (light version)

* Shape (base)
* Circle
* Rectangle

---

## 🧠 Shared:

* calculateArea()

---

## 💡 Important idea:

Each shape calculates area differently.

---

## Example thinking:

* Circle → π * r²
* Rectangle → width * height

---

# 🧠 8. What you should focus on now

For ALL systems:

You must always answer:

### 1. What is shared?

### 2. What is different?

### 3. Does it follow IS-A?

### 4. Should this be inheritance or composition?

---

# ⚠️ 9. Common mistakes in this phase

* putting everything in parent class
* creating too many levels of inheritance
* mixing unrelated responsibilities
* forgetting specialization logic

---

# 🧪 Your progression rule

We are NOT coding everything at once.

We go:

1. Structure
2. Fields
3. Methods
4. Constructors
5. Overriding
6. `super`

Step by step.

---

# ✔️ Next Step

Now we go into the first full guided implementation:

# 👉 Chapter 8 — Constructor & Overriding Practice Lab