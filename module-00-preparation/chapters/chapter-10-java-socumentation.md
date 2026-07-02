# Chapter 10 — Using the Official Java Documentation

## Overview

One of the most valuable skills a Java developer can develop is knowing how to read the official documentation.

The Java API documentation, commonly known as **Javadoc**, is the primary source of information about the Java Standard Library. It explains what every class, interface, method, and package does, as well as how they should be used.

Professional developers consult the documentation regularly—not because they don't know Java, but because it provides the most accurate and up-to-date information available.

In this chapter, we will learn how to navigate the official Java documentation and use it effectively throughout the rest of the Bootcamp.

---

## Objectives

By the end of this chapter, I will understand:

* What Javadoc is
* Why the official documentation is important
* How to navigate the Java API documentation
* How to search for classes and methods
* How to read method signatures
* How to understand parameters and return values
* How to identify deprecated APIs
* How documentation supports professional development

---

## What is Javadoc?

Javadoc is the official documentation system for Java.

It contains detailed information about:

* Packages
* Classes
* Interfaces
* Enums
* Records
* Methods
* Constructors
* Fields

Every public API in the Java Standard Library is documented using Javadoc.

---

## Why Use the Official Documentation?

The official documentation is the most reliable source of information because it is maintained alongside the Java platform itself.

Benefits include:

* Accurate information
* Up-to-date content
* Complete API reference
* Official examples
* Version-specific documentation

Instead of relying solely on tutorials, professional developers verify information using Javadoc.

---

## Understanding the Documentation Structure

Each documentation page usually contains:

* Class description
* Package information
* Constructors
* Methods
* Fields
* Inheritance hierarchy
* Implemented interfaces

This structure helps developers quickly locate the information they need.

---

## Reading a Class Page

Consider the `String` class.

A typical Javadoc page includes:

* Class description
* Constructors
* Method Summary
* Method Details

The **Method Summary** provides a quick overview of available methods.

The **Method Details** section explains how each method works.

---

## Understanding Method Signatures

A method signature describes how a method can be used.

Example:

```java
public int length()
```

Breaking it down:

* `public` → Access modifier
* `int` → Return type
* `length` → Method name
* `()` → No parameters

Another example:

```java
public String substring(int beginIndex)
```

This tells us:

* Returns a `String`
* Requires one integer parameter
* The parameter represents the starting index

Understanding method signatures is essential for reading Java APIs.

---

## Parameters

Parameters describe the information a method expects.

Example:

```java
substring(int beginIndex, int endIndex)
```

The documentation explains:

* What each parameter represents
* Valid values
* Possible exceptions

Always read the parameter descriptions before using unfamiliar methods.

---

## Return Values

The documentation specifies what a method returns.

Example:

```java
boolean isEmpty()
```

Return value:

* `true` if the string contains no characters
* `false` otherwise

Knowing the return type helps determine how the method should be used.

---

## Exceptions

Some methods may throw exceptions.

The documentation includes a **Throws** section describing:

* Which exceptions may occur
* Under what conditions they are thrown

Reading this section helps you write safer and more reliable code.

---

## Deprecated APIs

Some classes and methods are marked as **Deprecated**.

This means:

* They should no longer be used.
* A better alternative exists.
* They may be removed in a future Java version.

Always check for recommended replacements.

---

## Searching the Documentation

The documentation provides a search feature that allows you to quickly locate:

* Classes
* Interfaces
* Methods
* Packages

Examples:

* `String`
* `ArrayList`
* `Math`
* `Collections`

Learning to search efficiently saves a significant amount of development time.

---

## Documentation Inside IntelliJ IDEA

IntelliJ IDEA integrates Javadoc directly into the editor.

You can:

* View documentation by hovering over methods.
* Open complete documentation using keyboard shortcuts.
* Navigate directly to class definitions.

This integration allows you to learn without leaving the IDE.

---

## Best Practices

* Read the documentation before searching for tutorials.
* Verify method behavior using Javadoc.
* Pay attention to parameters and return types.
* Read the **Throws** section for exception details.
* Check whether an API is deprecated before using it.

---

## Common Mistakes

* Ignoring the official documentation.
* Assuming a method behaves as expected without reading its description.
* Using deprecated APIs.
* Overlooking parameter requirements.
* Ignoring exceptions documented by the API.

---

## Key Concepts Summary

* Javadoc is the official Java documentation.
* It documents every public API.
* Method signatures describe how methods are used.
* Documentation explains parameters, return values, and exceptions.
* Professional developers rely on Javadoc regularly.

---

## Key Idea of this Chapter

Knowing how to find information is more valuable than memorizing every API.

The official Java documentation is one of the most powerful learning resources available to every Java developer.

---

## Summary

* Javadoc is the official reference for the Java Standard Library.
* It provides complete documentation for classes, methods, and packages.
* Understanding method signatures is essential.
* Documentation explains parameters, return values, and exceptions.
* Learning to use Javadoc is a fundamental professional skill.

---

## Next Step

**Chapter 11 — Module Review and Final Checkpoint**

In the final chapter, we will review everything learned throughout Module 00, connect all the concepts together, and prepare for building the final project before moving on to the Java language itself.

---

🎉 **Parabéns!** Você chegou ao último capítulo de conteúdo do **Módulo 00**.

Depois do **Chapter 11 (Review & Checkpoint)**, construiremos o projeto final do módulo (estrutura profissional, pacotes, classe principal, README e primeiro programa), consolidando tudo o que foi aprendido antes de iniciar o **Module 01 — Java Language Fundamentals**.
