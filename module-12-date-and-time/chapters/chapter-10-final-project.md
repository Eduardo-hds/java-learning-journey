# Chapter 10 — Final Project: Event Management System

Congratulations!

You have completed the theoretical part of **Module 12**.

Now it's time to combine everything you've learned into a realistic application.

Unlike the previous exercises, this project will be developed as if it were a small production application.

The goal is **not** to write all the code at once.

Instead, we'll build it step by step, continuously improving the design.

---

# Project Objectives

Build a console application capable of:

* Registering events
* Storing dates and times
* Calculating remaining time
* Formatting dates
* Supporting multiple time zones
* Separating business logic from presentation
* Applying object-oriented design

---

# Concepts Used

During this project you will apply:

* `LocalDate`
* `LocalTime`
* `LocalDateTime`
* `Instant`
* `Duration`
* `Period`
* `DateTimeFormatter`
* `ZoneId`
* `ZonedDateTime`
* `ChronoUnit`
* Classes
* Objects
* Collections
* Services
* Packages

---

# Final Project Structure

```text
src/
│
├── Main.java
│
├── model/
│     ├── Event.java
│     ├── Appointment.java
│     └── Reminder.java
│
├── service/
│     ├── EventScheduler.java
│     ├── FormatterService.java
│     └── DateCalculator.java
│
└── util/
```

Notice how all business logic stays outside `Main.java`.

`Main` should only coordinate the application.

---

# Project Architecture

```text
               Main
                 │
      ┌──────────┴──────────┐
      │                     │
      ▼                     ▼

EventScheduler      FormatterService
      │
      ▼

Event Objects
```

Responsibilities are clearly separated.

---

# Step 1 — Create the Event Model

Create the class:

```text
model/Event.java
```

Suggested attributes:

```java
private String title;

private LocalDateTime dateTime;

private ZoneId zoneId;
```

Why these fields?

* Event name
* When it occurs
* Where it occurs

A global application should know the event's time zone.

---

# Step 2 — Constructor

Create a constructor that initializes all fields.

Example usage:

```java
Event meeting =
        new Event(
                "Team Meeting",
                LocalDateTime.of(
                        2026,
                        8,
                        10,
                        14,
                        30
                ),
                ZoneId.of("America/Sao_Paulo")
        );
```

---

# Step 3 — Getters

Implement getters for every field.

Do **not** expose mutable state through setters unless your design truly requires it.

Remember that:

* `LocalDateTime`
* `ZoneId`

are immutable.

---

# Step 4 — Create FormatterService

Package:

```text
service/
```

Create:

```text
FormatterService.java
```

Create a reusable formatter.

Example:

```java
dd/MM/yyyy HH:mm
```

Add a method:

```java
String format(Event event)
```

Example output:

```text
Team Meeting

10/08/2026 14:30

America/Sao_Paulo
```

Avoid duplicating formatting logic across the application.

---

# Step 5 — Create DateCalculator

Package:

```text
service/
```

Create methods like:

```java
daysUntil(Event event)

hoursUntil(Event event)

isUpcoming(Event event)
```

Use:

* `ChronoUnit`
* `Duration`
* `LocalDateTime.now()`

This class centralizes date-related calculations.

---

# Step 6 — Create EventScheduler

Package:

```text
service/
```

Internally store:

```java
List<Event>
```

Operations:

```text
addEvent()

removeEvent()

listEvents()

findNextEvent()
```

Keep all event management inside this service instead of `Main`.

---

# Step 7 — Display Events

In `Main.java`:

* Create several sample events.
* Add them to the scheduler.
* Display them using `FormatterService`.

The output should resemble:

```text
Upcoming Events

-------------------------

Java Bootcamp

20/08/2026 19:00

America/Sao_Paulo

Remaining:

36 days

-------------------------

Dentist

25/07/2026 09:30

America/Sao_Paulo

Remaining:

10 days
```

---

# Step 8 — Remaining Time

Use:

```java
ChronoUnit.DAYS.between(...)
```

or

```java
Duration.between(...)
```

depending on the level of precision you want.

Display:

```text
Starts in:

5 days
```

or

```text
Starts in:

4 hours
```

---

# Step 9 — Multiple Time Zones

Create one event in:

```text
America/Sao_Paulo
```

Another in:

```text
Europe/London
```

Another in:

```text
Asia/Tokyo
```

Display each event with its own time zone.

As an optional enhancement, also display the event converted to the user's system time zone using:

```java
eventInstant.atZone(ZoneId.systemDefault())
```

---

# Step 10 — Sorting

Sort events by date.

Hint:

`LocalDateTime` implements `Comparable`.

Example:

```java
events.sort(
        Comparator.comparing(
                Event::getDateTime
        )
);
```

Now the scheduler always lists events chronologically.

---

# Step 11 — Find the Next Event

Create:

```java
findNextEvent()
```

The method should:

* Ignore past events.
* Return the closest future event.
* Return `null` or `Optional<Event>` if none exist.

This is a great opportunity to practice filtering and comparisons.

---

# Step 12 — Reminder Class

Create:

```text
model/Reminder.java
```

Suggested fields:

```java
message

LocalDateTime reminderTime
```

Possible method:

```java
shouldNotify()
```

Return:

```java
true
```

when:

```text
Current time >= reminder time
```

---

# Step 13 — Appointment Class

Create:

```text
model/Appointment.java
```

Suggested attributes:

```java
doctorName

patientName

LocalDateTime appointmentTime
```

Useful methods:

```text
isPast()

isToday()

isFuture()
```

Reuse the comparison methods you've learned instead of duplicating logic.

---

# Example Execution

```text
==================================

EVENT MANAGEMENT SYSTEM

==================================

1 - List Events

2 - Next Event

3 - Days Until Event

4 - Exit

==================================
```

Selecting:

```text
1
```

Could display:

```text
Java Bootcamp

20/08/2026 19:00

America/Sao_Paulo

Remaining:

36 days
```

---

# Recommended Improvements

After the basic version works, try adding:

* Event categories
* Event descriptions
* Multiple reminders
* Event duration
* Search by title
* Events happening today
* Monthly calendar view
* Save and load events from a file (after learning file I/O)
* User-selected display time zone

These are excellent opportunities to extend the project as you progress through later modules.

---

# What This Project Reinforces

By completing this project, you will have practiced:

* Object-oriented design
* Separation of responsibilities
* Immutability
* Date calculations
* Formatting and parsing
* Time zones
* Collections
* Service classes
* Package organization
* Clean architecture principles

This project is intentionally structured to resemble the architecture of larger Java applications, making it a strong foundation for upcoming modules such as File I/O, JDBC, and Spring Boot.

---

# Module 12 Review

You learned:

* Why the legacy `Date` and `Calendar` APIs were replaced.
* How to work with `LocalDate`, `LocalTime`, and `LocalDateTime`.
* How `Instant` represents a universal point in time.
* The difference between `Duration` and `Period`.
* How to format and parse dates with `DateTimeFormatter`.
* How to work with `ZoneId` and `ZonedDateTime`.
* How to perform advanced operations using `ChronoUnit`.
* How to apply all these concepts in a practical event management application.

---

# Common Mistakes to Remember

* ❌ Using `LocalDateTime` for globally shared timestamps.
* ❌ Confusing `Duration` (time-based) with `Period` (date-based).
* ❌ Forgetting that all `java.time` classes are immutable.
* ❌ Using fixed UTC offsets instead of `ZoneId`.
* ❌ Parsing dates with the wrong formatting pattern.
* ❌ Ignoring invalid user input when parsing.

---

# 🎉 Module 12 Complete

Excellent work. At this point in the bootcamp, you're comfortable with one of the most important APIs in modern Java. The `java.time` package is used extensively in enterprise applications, REST APIs, databases, scheduling systems, financial software, and backend services.

You're now ready to move on to the next module of the bootcamp.
