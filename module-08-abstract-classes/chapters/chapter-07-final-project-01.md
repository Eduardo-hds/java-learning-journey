# Chapter 7 — Final Project Design (Abstract System Architecture)

---

# 🧠 1. What This Chapter Is About

Now you are moving from **small exercises → system design thinking**.

Instead of focusing on one class at a time, we design:

> A complete structure using abstract classes + inheritance

No full implementation yet — only architecture and decisions.

---

# 🎯 2. Final Project Goal

You will build a console-based system that includes:

* ✔ At least **2 abstract classes**
* ✔ At least **4 concrete classes**
* ✔ Strong inheritance hierarchy
* ✔ Shared behavior + enforced methods
* ✔ Clean package separation

---

# 🧩 3. Choose Your Project Direction

Pick ONE of these architectures:

---

## 🏦 Option A — Banking System

### Abstract Classes:

* `Account`

### Concrete Classes:

* `SavingsAccount`
* `CheckingAccount`
* `BusinessAccount`
* `PremiumAccount`

### Concepts:

* balance management
* withdrawal rules differ
* shared deposit logic

---

## 👨‍💼 Option B — Employee System

### Abstract Classes:

* `Employee`

### Concrete Classes:

* `Developer`
* `Manager`
* `Designer`
* `Intern`

### Concepts:

* work() behavior differs
* shared login/clock-in
* salary logic variation

---

## 🧮 Option C — Shape System

### Abstract Classes:

* `Shape`

### Concrete Classes:

* `Circle`
* `Rectangle`
* `Triangle`
* `Square`

### Concepts:

* area() enforced
* shared geometry rules
* different formulas

---

# 🏗️ 4. Required Architecture Rules

No matter which project you choose:

---

## ✔ Must include:

### 1. Abstract Class with:

* at least 1 abstract method
* at least 1 concrete method

### 2. Subclasses:

* override abstract methods
* optionally override shared behavior

### 3. Proper hierarchy:

* clean “is-a” relationship

---

# 📦 5. Package Structure (MANDATORY)

You must organize like this:

```text id="pkg1"
src/
 ├── Main.java
 ├── model/
 │    ├── (abstract classes)
 │    ├── (concrete classes)
 ├── service/
 └── util/
```

---

# 🧠 6. Design Thinking (VERY IMPORTANT)

Before coding, answer:

### 1. What is the base concept?

* Account? Employee? Shape?

### 2. What is shared?

* Fields?
* Methods?
* Logic?

### 3. What MUST change per subclass?

* behavior?
* calculations?

---

# ⚙️ 7. Example Design (Banking System)

### Abstract Class:

```java id="abs1"
abstract class Account {

    double balance;

    void deposit(double amount) {
        balance += amount;
    }

    abstract void withdraw(double amount);
}
```

---

### Subclasses:

* SavingsAccount → limited withdrawals
* CheckingAccount → flexible withdrawals

---

# 🔥 8. What Makes a Good Design

✔ Minimal duplication
✔ Clear responsibility per class
✔ Abstract class holds shared logic
✔ Subclasses only specialize behavior

---

# 🚫 9. Common Mistakes

Avoid:

❌ Putting everything in abstract class
❌ No real differences between subclasses
❌ Using inheritance without logic reason
❌ Overcomplicating hierarchy

---

# 🌍 10. Mental Model

Think like this:

### Abstract Class = “Blueprint”

* defines structure
* provides shared logic

### Subclasses = “Specialized Versions”

* complete missing behavior
* define unique rules

---

# 🧪 11. Your Task Before Coding

Choose ONE project and answer:

1. What is your abstract class?
2. What are your 4 subclasses?
3. What behavior is shared?
4. What behavior changes?

---

# ✔️ Key Takeaway

This is no longer just Java syntax.

This is:

> “Designing systems using abstraction and inheritance”

---

# ▶️ Next Step

After you choose your project direction, we move to:

## 🚀 Chapter 7.1 — Project Implementation (Step-by-step guided build)
