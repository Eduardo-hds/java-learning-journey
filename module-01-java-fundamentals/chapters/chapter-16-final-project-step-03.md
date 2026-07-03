Good.

Now we move into **Stage 3**, where your code starts to look less like an exercise and more like a real application.

---

# 🧩 Stage 3 — Constants + Business Rules

## Objective

Right now, your program has “magic values” like:

* `6.0` for approval
* hardcoded text logic
* rules scattered inside conditions

We’re going to fix that using **constants and clean structure thinking**.

---

# 📌 New Requirements

Update your `StudentSystem.java` to introduce **constants** for business rules.

---

## 1. Add Constants

At the top of your `main`, define:

```java id="c9xq1a"
final double APPROVAL_GRADE = 6.0;
```

---

## 2. Replace Magic Numbers

Instead of:

```java id="k3v9ma"
if (average >= 6.0)
```

Use:

```java id="m8q2pl"
if (average >= APPROVAL_GRADE)
```

---

## 3. Improve Status Logic

Keep your existing logic, but make it cleaner.

You can do:

```java id="z1k7td"
String status;
```

Then assign:

```java id="v6n2qs"
status = "Approved";
status = "Failed";
```

---

## 4. Keep Output Same Format

No formatting changes required, just cleaner internal structure.

---

# 📤 Expected Output (unchanged visually)

```text id="x7m2pq"
--- Student Data ---
Name: Eduardo
Age: 20
Grade 1: 8.5
Grade 2: 7.0
Average: 7.75
Status: Approved
```

---

# 🧠 What You Are Learning Here

This stage is not about new features — it's about:

* Removing magic numbers
* Introducing business rules as constants
* Improving maintainability
* Making code scalable
* Thinking like a developer, not a beginner

---

# ⚠️ Rules

* Do NOT restructure the whole program
* Do NOT use methods yet
* Do NOT add new features
* Only refactor what is requested

---

# 💡 Professional Insight

In real systems:

> The difference between junior and mid-level code is not complexity — it is **clarity and maintainability**.

This stage is exactly that mindset shift.

---

# 🚀 Your Task

Refactor your current program:

* Add constants
* Replace magic numbers
* Clean up status logic

---

When finished, proceed to:

👉 Stage 4 — Input Validation + Debugging Scenarios
