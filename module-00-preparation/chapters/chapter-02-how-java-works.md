# Chapter 2 — How Java Works Internally

## Overview

In the previous chapter, we understood what Java is, why it was created, and the idea behind its platform independence.

Now we go one level deeper.

This chapter explains how Java actually works under the hood: how code is executed, what happens after you write a `.java` file, and how the JVM makes Java platform-independent.

The goal is to understand the full execution pipeline of a Java program.

---

## Objectives

By the end of this chapter, I will understand:

- How Java code is compiled and executed
- What bytecode is
- What the JVM does internally
- What a class loader is
- How Java achieves platform independence
- The basic structure of Java memory (Stack, Heap, Metaspace)
- The lifecycle of a Java program from code to execution

---

## The Java Execution Flow

When you write Java code, it does not run directly on the operating system.

Instead, it goes through a transformation process:

Java Source Code → Bytecode → JVM → Operating System

Each step has a specific responsibility:

- Source Code: what you write (`.java`)
- Bytecode: intermediate compiled format (`.class`)
- JVM: executes the bytecode
- Operating System: provides resources (CPU, memory, etc.)

---

## What is Bytecode?

Bytecode is an intermediate representation of Java code.

When you compile a Java file using `javac`, it does not become machine code. Instead, it becomes bytecode.

Characteristics of bytecode:

- Platform-independent
- Not readable like source code
- Executed by the JVM
- Stored in `.class` files

This is one of the key reasons Java is portable.

---

## What is the JVM?

The JVM (Java Virtual Machine) is the core of Java’s platform independence.

It is responsible for:

- Loading bytecode
- Verifying code safety
- Executing instructions
- Managing memory
- Running the program on a specific operating system

Each operating system has its own JVM implementation, but all follow the same specification.

---

## Class Loader System

Before code is executed, the JVM loads classes into memory using the Class Loader.

The process happens in three steps:

1. Loading
2. Linking
3. Initialization

### Loading

The class bytecode is read and loaded into memory.

### Linking

The class is verified and prepared for execution.

### Initialization

Static variables are initialized and ready to use.

---

## JVM Memory Structure (Basic View)

The JVM uses different memory areas to execute programs:

### Stack

- Stores method calls
- Stores local variables
- Works in LIFO (Last In, First Out)
- Each thread has its own stack

---

### Heap

- Stores objects
- Shared across all threads
- Managed by Garbage Collector

---

### Metaspace

- Stores class metadata
- Information about classes, methods, and structure

---

## How a Java Program Runs (Step-by-Step)

1. You write a `.java` file
2. The compiler (`javac`) converts it into bytecode
3. Bytecode is stored in `.class` files
4. JVM loads the class using Class Loader
5. JVM verifies the bytecode
6. JVM executes the program
7. Garbage Collector manages memory automatically

---

## Why this architecture exists

This design solves three major problems:

### 1. Portability

Bytecode can run on any system with a JVM.

### 2. Security

JVM verifies code before execution.

### 3. Memory management

Garbage Collector handles memory automatically.

---

## Real-world analogy

- Java code = recipe written in human language
- Bytecode = standardized cooking instructions
- JVM = chef that adapts the recipe to any kitchen
- Operating system = kitchen environment

---

## Key Concepts Summary

- Java does not run directly on the OS
- It runs inside the JVM
- Source code is compiled into bytecode
- Bytecode is platform-independent
- JVM handles execution and memory management
- Class Loader prepares classes before execution

---

## Key Idea of this Chapter

Java is not just compiled code.

It is a runtime system built around the JVM that makes execution portable, safe, and automated.

---

## Summary

- Java compilation produces bytecode
- JVM executes bytecode, not the OS directly
- Class Loader loads and prepares classes
- Memory is divided into Stack, Heap, and Metaspace
- This architecture enables portability and security

---

## Next Step

Next chapter: **JDK, JRE and JVM**

We will break down these three concepts clearly and remove one of the biggest confusions in Java.
