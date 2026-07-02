# Chapter 4 — Setting Up the Development Environment

## Overview

Before writing Java code professionally, it is essential to set up a proper development environment.

This includes installing the Java Development Kit (JDK), configuring system variables, and verifying that the tools are working correctly.

A correct setup ensures that you can compile, run, and manage Java applications without issues.

---

## Objectives

By the end of this chapter, I will understand:

- What a JDK distribution is
- How to install Java (JDK) correctly
- What JAVA_HOME is and why it is important
- How the PATH environment variable works
- How to verify a Java installation
- How to ensure the system is ready for development

---

## Choosing a JDK Distribution

There are multiple JDK distributions available:

- Oracle JDK
- OpenJDK
- Eclipse Temurin (recommended for most developers)
- Microsoft Build of OpenJDK

All of them implement the same Java specification.

Recommended choice for beginners and professionals:

- Eclipse Temurin (stable, free, widely used)

---

## Installing the JDK

After choosing a distribution:

1. Download the installer for your operating system
2. Run the installation
3. Install the JDK in the default location (recommended)

After installation, Java tools will be available on your system.

---

## Understanding JAVA_HOME

JAVA_HOME is an environment variable that points to the JDK installation directory.

It is used by:

- Build tools (Maven, Gradle)
- IDEs (IntelliJ IDEA)
- System scripts

Example:

JAVA_HOME = C:\Program Files\Java\jdk-21

---

## Configuring PATH

The PATH variable allows you to run Java commands from any terminal location.

You should include:

- JAVA_HOME/bin

This enables commands like:

- java
- javac
- jar

to be accessible globally.

---

## Verifying Installation

After setup, open a terminal and run:

- java -version
- javac -version

If correctly installed, both commands will display version information.

This confirms that:

- JDK is installed
- System variables are configured correctly
- Java is ready to use

---

## How Java Tools Work Together

Once installed:

- javac compiles Java code into bytecode
- java runs the compiled bytecode using the JVM
- JDK provides both tools
- JVM executes the program

This completes the development loop.

---

## Common Issues

### 1. "java is not recognized"

Cause:

- PATH not configured correctly

Solution:

- Add JAVA_HOME/bin to PATH

---

### 2. Wrong Java version

Cause:

- Multiple Java versions installed

Solution:

- Check JAVA_HOME and PATH order

---

### 3. JAVA_HOME not set

Cause:

- Missing environment variable

Solution:

- Manually set JAVA_HOME to JDK folder

---

## Best Practices

- Always use a stable LTS version (e.g., Java 17 or 21)
- Prefer Eclipse Temurin for consistency
- Always verify installation before starting development
- Keep environment variables clean and organized

---

## Key Concepts Summary

- JDK is required to develop Java applications
- JAVA_HOME points to the JDK installation
- PATH allows global access to Java commands
- javac compiles code, java executes it
- Proper setup avoids development issues

---

## Key Idea of this Chapter

A correct environment setup is the foundation of professional Java development.

Without it, even simple programs cannot be compiled or executed.

---

## Summary

- Install a JDK distribution (recommended: Temurin)
- Configure JAVA_HOME
- Add Java to PATH
- Verify installation using terminal commands
- Ensure system is ready for development

---

## Next Step

Next chapter: **Getting to Know IntelliJ IDEA**

We will learn how to use a professional IDE to write, run, and debug Java applications efficiently.
