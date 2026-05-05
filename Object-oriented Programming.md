# Object-oriented Programming

## Getting Started

### 1) Introduction

Object-oriented Programming (OOP) is a way of writing code by organizing it around **objects**.

An object is like a real-world thing in your program.  
For example, in a school app, you might have objects like:

- `Student`
- `Course`
- `Teacher`

Each object can have:

- **Data** (called fields/properties), like a student's name
- **Behavior** (called methods), like `enroll()` or `printReport()`

OOP helps you model real problems in a natural way.

### 2) Programming Paradigms

A programming paradigm is a style or approach to writing code.

Common paradigms:

- **Procedural programming** - code is organized as steps and functions
- **Object-oriented programming** - code is organized as objects and classes
- **Functional programming** - code is organized around pure functions and immutability

Java supports multiple styles, but OOP is one of its main strengths.

Simple comparison:

Procedural style often asks:  
"What steps should happen?"

OOP style often asks:  
"What objects do I have, and what should each object do?"

Both can solve problems, but OOP is very useful for larger applications.

### 3) Benefits of Object-oriented Programming

OOP gives you structure, especially when projects grow bigger.

Main beginner-friendly benefits:

- **Better organization** - related data and behavior stay together in one class
- **Reusability** - you can reuse classes in different parts of your app
- **Easier maintenance** - cleaner structure makes bugs easier to find
- **Scalability** - easier to add new features without breaking old code

Quick example idea:

If you have a `Car` class once, you can create many car objects from it:

```java
Car car1 = new Car();
Car car2 = new Car();
```

You write the class once, then reuse it many times.
