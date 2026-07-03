Good. Now your code is starting to look like something closer to real production structure.

---

# 🧩 Stage 4 — Input Validation + Debugging Scenarios

## Objective

Up to now, your program assumes the user always enters correct data.

Real applications **cannot trust user input**.

So now we introduce:

* Basic validation
* Handling incorrect input behavior
* Using logic + conditions to prevent bad results
* Thinking like a debugger

(No exception handling yet — that comes later.)

---

# 📌 New Requirements

Update your `StudentSystem.java` with the following improvements:

---

## 1. Validate Grade Range

Grades must be between:

```text
0.0 → 10.0
```

If the user enters invalid values:

* Print an error message
* Stop the program (you can use `return;` inside `main`)

---

### Example logic:

```java id="v8k2mx"
if (grade1 < 0 || grade1 > 10) {
    System.out.println("Invalid grade 1");
    return;
}
```

---

## 2. Apply Same Validation for grade2

Both grades must be validated separately.

---

## 3. Improve Error Messages

Make them clear and professional:

Good:

```text
Invalid input: grade must be between 0 and 10
```

Bad:

```text
error
```

---

## 4. Ensure Program Stops on Invalid Input

Do NOT continue calculations if data is invalid.

This is important.

---

# 🧠 What You Are Practicing

This stage is about thinking like a developer:

* Defensive programming
* Input validation
* Flow control with `if`
* Early exit strategy (`return`)
* Preventing invalid state propagation
* Debug mindset (anticipating wrong input)

---

# ⚠️ Important Rules

* Do NOT use loops
* Do NOT use methods
* Do NOT use exception handling (`try/catch`)
* Keep it simple and linear
* Validate immediately after input

---

# 💡 Mental Model

Think of your program like a pipeline:

```text
INPUT → VALIDATION → PROCESSING → OUTPUT
```

If input is invalid, the pipeline stops immediately.

---

# 🚀 Your Task

Implement:

* Grade validation (0–10)
* Error messages
* Early exit on invalid input

---

When done, proceed to:

👉 Stage 5 — Final Polish (clean structure, professional output, and mini real-world simulation)
