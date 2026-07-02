# Chapter 9 — Debugging Java Applications

## Overview

Writing code is only part of software development. Understanding how code behaves during execution is just as important.

Professional developers spend a significant amount of time debugging applications to identify errors, understand program flow, and verify that the code behaves as expected.

In this chapter, we will learn how to use IntelliJ IDEA's built-in debugger to inspect program execution step by step.

---

## Objectives

By the end of this chapter, I will understand:

* What debugging is
* Why debugging is important
* What breakpoints are
* How to start a debugging session
* How to inspect variables
* The difference between Step Over, Step Into, and Step Out
* How the call stack works
* Why debugging is more effective than using print statements

---

## What is Debugging?

Debugging is the process of analyzing a program while it is running.

Instead of guessing what the code is doing, a debugger allows you to observe the execution in real time.

With a debugger, you can:

* Pause execution
* Execute code line by line
* Inspect variables
* Analyze method calls
* Identify logic errors

Debugging is one of the most valuable skills for any software developer.

---

## What is a Breakpoint?

A breakpoint is a marker placed on a specific line of code.

When the program reaches that line, execution pauses automatically.

This allows you to inspect the current state of the application before continuing.

Example:

```java
public class Main {

    public static void main(String[] args) {

        int number = 10; // Breakpoint here

        System.out.println(number);

    }

}
```

When the debugger reaches the breakpoint, the program stops before executing that line.

---

## Starting a Debug Session

In IntelliJ IDEA:

1. Open your Java project.
2. Place a breakpoint by clicking in the left margin of the editor.
3. Click the **Debug** button (bug icon) or use the keyboard shortcut.
4. The application starts and pauses at the breakpoint.

At this point, you can inspect the program before it continues.

---

## Inspecting Variables

While execution is paused, IntelliJ displays the current values of all visible variables.

Example:

```java
int age = 25;
String name = "Eduardo";
```

The debugger will show:

```text
age = 25
name = "Eduardo"
```

This allows you to verify whether the program is behaving correctly.

---

## Step Over

**Step Over** executes the current line and moves to the next one.

If the current line calls another method, the debugger executes the entire method without entering it.

Use Step Over when you trust the called method and only want to continue through the current method.

---

## Step Into

**Step Into** enters the method being called.

Example:

```java
calculateTotal();
```

Using Step Into takes you inside the `calculateTotal()` method so you can observe its execution line by line.

This is useful when investigating how a method works internally.

---

## Step Out

**Step Out** finishes executing the current method and returns to the method that called it.

This is useful when you accidentally entered a method or have already inspected it and want to continue with the calling code.

---

## Resume Program

After reaching a breakpoint, you can resume normal execution.

The debugger continues running until:

* Another breakpoint is reached.
* The program finishes.

---

## Understanding the Call Stack

The Call Stack shows the sequence of method calls that led to the current execution point.

Example:

```text
main()
    └── calculatePrice()
            └── applyDiscount()
```

This helps you understand:

* Which method is currently executing.
* Which method called it.
* The path taken to reach the current line.

The Call Stack is extremely useful for diagnosing complex problems.

---

## Debugger vs. Print Statements

Many beginners use `System.out.println()` to understand program behavior.

Example:

```java
System.out.println(value);
```

Although useful for quick checks, this approach has limitations.

Using a debugger allows you to:

* Inspect multiple variables at once.
* Pause execution.
* Execute one line at a time.
* Navigate through method calls.
* Analyze the complete program state.

Professional developers rely primarily on debuggers rather than print statements.

---

## Common Mistakes

* Forgetting to start the application in Debug mode.
* Placing breakpoints on the wrong lines.
* Assuming the debugger changes the program's behavior.
* Ignoring the Call Stack during debugging.
* Relying exclusively on `System.out.println()`.

---

## Best Practices

* Use breakpoints strategically.
* Inspect variables before making assumptions.
* Learn the keyboard shortcuts for debugging.
* Understand the execution flow before modifying the code.
* Remove unnecessary breakpoints after finishing.

---

## Key Concepts Summary

* Debugging allows you to inspect a running program.
* Breakpoints pause execution.
* Step Over executes the next line.
* Step Into enters a method.
* Step Out returns to the calling method.
* The Call Stack shows the execution path.
* Debugging is one of the most important professional development skills.

---

## Key Idea of this Chapter

The debugger allows you to observe exactly what your program is doing.

Instead of guessing why something is wrong, you can watch the execution happen step by step.

---

## Summary

* Debugging is essential for understanding and fixing software.
* Breakpoints allow execution to pause.
* IntelliJ IDEA provides powerful debugging tools.
* The Call Stack helps trace method execution.
* Professional developers use debuggers to analyze program behavior efficiently.

---

## Next Step

**Chapter 10 — Using the Official Java Documentation**

In the next chapter, we will learn how to navigate the official Java documentation (Javadoc), search for classes and methods, and use it as a primary learning resource throughout the rest of the Bootcamp.
