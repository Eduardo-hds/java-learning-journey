# Chapter 3 — JDK, JRE and JVM

## Overview

One of the most common sources of confusion when learning Java is understanding the difference between JDK, JRE, and JVM.

Although these three components are closely related, they have very different responsibilities in the Java ecosystem.

In this chapter, we will clearly separate each one and understand how they work together to run Java applications.

---

## Objectives

By the end of this chapter, I will understand:

- What the JVM is and its role in execution
- What the JRE is and why it exists
- What the JDK is and what tools it provides
- The differences between JVM, JRE, and JDK
- How these components interact in the Java workflow
- Why developers need the JDK but users only need the JRE (historically)

---

## The Big Picture

Java is composed of three main layers:

- JDK (Java Development Kit)
- JRE (Java Runtime Environment)
- JVM (Java Virtual Machine)

They are nested in a hierarchy:

JDK → includes JRE → includes JVM

---

## What is the JVM?

The JVM (Java Virtual Machine) is the core execution engine of Java.

Its responsibilities include:

- Executing bytecode
- Managing memory (Heap, Stack, etc.)
- Running garbage collection
- Providing platform independence
- Translating bytecode into machine-level instructions

The JVM is what actually runs Java programs.

---

## What is the JRE?

The JRE (Java Runtime Environment) provides everything needed to run Java applications.

It includes:

- JVM
- Core Java libraries (java.lang, java.util, etc.)
- Runtime components required for execution

Important concept:

- JRE is for running Java programs
- JRE does NOT include development tools like compilers

---

## What is the JDK?

The JDK (Java Development Kit) is the full toolkit for Java developers.

It includes:

- JRE (so it can run programs)
- JVM
- Development tools such as:
  - javac (compiler)
  - java (runtime launcher)
  - jar (packaging tool)
  - javadoc (documentation generator)

Important concept:

- JDK is required to develop Java applications
- Without JDK, you cannot compile Java code

---

## Relationship Between Them

The relationship can be understood like this:

- JVM → executes Java bytecode
- JRE → provides environment to run Java programs (JVM + libraries)
- JDK → provides tools to develop Java programs (JRE + development tools)

---

## Java Execution Flow (with JDK, JRE, JVM)

1. You write Java code (.java)
2. JDK compiler (javac) compiles it into bytecode (.class)
3. JVM reads and executes bytecode
4. JRE provides runtime libraries needed for execution
5. Operating system provides system resources

---

## Simple Analogy

- JVM = Engine (runs the program)
- JRE = Car (engine + necessary components to drive)
- JDK = Factory (tools to build and maintain the car)

---

## Why this separation exists

This architecture was designed to:

### 1. Separate development from execution

Developers need tools, users only need runtime.

### 2. Reduce system complexity

Users don’t need compilers or development tools.

### 3. Improve portability

JVM abstracts the operating system layer.

---

## Important Modern Note

In modern Java (Java 9+), the distinction between JRE and JDK became less visible because:

- Modular system changes
- JRE is no longer distributed separately in many cases

However, the concepts are still extremely important for understanding Java architecture.

---

## Key Concepts Summary

- JVM executes bytecode
- JRE provides runtime environment
- JDK provides development tools
- JDK includes JRE, and JRE includes JVM
- Developers use JDK, users historically used JRE

---

## Key Idea of this Chapter

Java is structured in layers to separate development, runtime, and execution responsibilities.

This is what makes the ecosystem scalable and well-organized.

---

## Summary

- JVM = execution engine
- JRE = runtime environment
- JDK = development kit
- They form a layered architecture
- Each has a specific responsibility in Java execution

---

## Next Step

Next chapter: **Setting Up the Development Environment**

We will install and configure Java properly and prepare a professional development setup.
