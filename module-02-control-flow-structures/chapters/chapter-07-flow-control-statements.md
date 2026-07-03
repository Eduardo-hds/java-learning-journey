# Chapter 07 — Flow Control Statements (Java)

## 🎯 Objective

In this chapter, you will learn how to **control the execution flow inside loops and methods** using:

* `break`
* `continue`
* `return`

These tools let you **stop, skip, or exit execution early**.

---

## 🧠 Core Concept

Normally, loops run until their condition becomes false.

Flow control statements let you:

* stop early (`break`)
* skip a step (`continue`)
* exit a method (`return`)

---

## 🔧 break

### 👉 Stops the loop completely

```java id="b1k9aa"
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;
    }
    System.out.println(i);
}
```

📌 Output: 0 to 4

---

## 🔧 continue

### 👉 Skips the current iteration

```java id="b2k9bb"
for (int i = 0; i < 5; i++) {
    if (i == 2) {
        continue;
    }
    System.out.println(i);
}
```

📌 Output: 0, 1, 3, 4

---

## 🔧 return

### 👉 Exits the method completely

```java id="b3k9cc"
public static void test() {
    System.out.println("Start");

    return;

    // code here will never run
}
```

---

## ⚙️ Summary

| Keyword  | Effect                       |
| -------- | ---------------------------- |
| break    | stops loop completely        |
| continue | skips current loop iteration |
| return   | exits method                 |

---

## 🧪 Mini Exercise 1 — Stop at Number

### Goal:

Loop from 1 to 10, but stop when reaching 7.

### Requirement:

* Use `break`

---

## 🧪 Mini Exercise 2 — Skip Even Numbers

### Goal:

Print only odd numbers from 1 to 10.

### Requirement:

* Use `continue`

---

## 🧪 Mini Exercise 3 — Login Exit

### Goal:

Simulate a login check:

* If password is correct → exit method using `return`
* Otherwise continue asking (combine with previous chapter logic if needed)

---

## 🧠 Challenge (Optional)

Combine all concepts:

* Loop numbers 1 to 20
* Skip multiples of 3 (`continue`)
* Stop completely at 17 (`break`)

---

## ⚠️ Common Mistakes

* Using `break` when you meant `continue`
* Overusing `return` inside loops
* Creating unreachable code after `return`

---

## 📌 What you should focus on

* Controlling loop behavior precisely
* Knowing when to stop vs skip
* Exiting methods cleanly

---

## 🏁 End of Module 02

You’ve now learned:

* Conditionals (`if`, `switch`)
* All loop types (`while`, `do while`, `for`, for-each)
* Flow control (`break`, `continue`, `return`)

---

## 🚀 Final Step

Now you should take everything learned in this chapter and apply it through practice.

Once you're comfortable with the concepts, proceed to the **Final Project of Module 02**, where you will combine all control flow structures into a complete console-based system.

👉 Continue to the **Module 02 Final Project**.
