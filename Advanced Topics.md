# Advanced Topics

## Exceptions

### 1) Introduction

Exceptions are how Java reports problems that happen while a program is running.

Instead of crashing silently, Java gives you a clear error object you can handle.

### 2) What are Exceptions

An exception is an object that describes an error.

Example: dividing by zero.

```java
int result = 10 / 0; // ArithmeticException
```

If you do not handle it, the program stops and prints an error message.

### 3) Types of Exceptions

In simple terms, Java has:

- **Checked exceptions** - must be handled or declared (e.g., `IOException`)
- **Unchecked exceptions** - runtime errors (e.g., `NullPointerException`)
- **Errors** - serious JVM issues (usually not handled in app code)

Checked exceptions are verified by the compiler.

### 4) Exceptions Hierarchy

All exceptions come from `Throwable`.

High-level structure:

- `Throwable`
  - `Exception`
    - checked exceptions
    - `RuntimeException` (unchecked)
  - `Error`

Knowing this hierarchy helps you catch exceptions at the right level.

### 5) Catching Exceptions

Use `try` and `catch` to handle errors safely.

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException ex) {
    System.out.println("Cannot divide by zero.");
}
```

Now your program can continue instead of crashing.

### 6) Catching Multiple Types of Exceptions

You can catch different exception types in separate `catch` blocks, or combine them.

```java
try {
    String text = null;
    System.out.println(text.length());
} catch (NullPointerException | ArithmeticException ex) {
    System.out.println("Invalid operation: " + ex.getMessage());
}
```

This keeps handling concise when the response is similar.

### 7) The finally Block

`finally` runs whether an exception happens or not.

Use it for cleanup work (closing files, releasing resources, etc.).

```java
try {
    System.out.println("Working...");
} catch (Exception ex) {
    System.out.println("Error.");
} finally {
    System.out.println("Always runs.");
}
```

### 8) The try-with-resources Statement

Use `try-with-resources` for resources like files/scanners.

It closes them automatically.

```java
try (java.util.Scanner scanner = new java.util.Scanner(System.in)) {
    System.out.print("Name: ");
    String name = scanner.nextLine();
    System.out.println(name);
}
```

This is cleaner and safer than manual closing.

### 9) Throwing Exceptions

Use `throw` when you want to signal an error yourself.

```java
public static void setAge(int age) {
    if (age < 0)
        throw new IllegalArgumentException("Age cannot be negative.");
}
```

This protects your methods from invalid input.

### 10) Re-throwing Exceptions

Sometimes you catch an exception to log or add context, then throw it again.

```java
try {
    // risky code
} catch (Exception ex) {
    System.out.println("Logging error: " + ex.getMessage());
    throw ex;
}
```

This lets higher layers decide how to handle it.

### 11) Custom Exceptions

You can create your own exception class for domain-specific problems.

```java
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}
```

Custom exceptions make errors clearer and more meaningful.

### 12) Chaining Exceptions

Exception chaining means wrapping one exception inside another to preserve root cause.

```java
try {
    // low-level operation
} catch (Exception ex) {
    throw new RuntimeException("Failed to process payment.", ex);
}
```

Now you keep both:

- high-level business message
- original technical cause

### 13) Summary

Key ideas:

- Exceptions help you handle runtime problems safely
- Use `try/catch/finally` for control and cleanup
- Prefer `try-with-resources` for automatic closing
- Throw meaningful exceptions for invalid states
- Use custom and chained exceptions for clearer error handling

Good exception handling makes your code safer, cleaner, and easier to debug.

---

## Generics

### 1) Introduction

Generics let you write classes and methods that work with different data types safely.

They help you avoid repeated code and reduce type-casting mistakes.

### 2) The Need for Generics

Without generics, collections often store values as `Object`, and you must cast later.

That can cause runtime errors.

Generics move many of those errors to compile time, which is safer.

### 3) A Poor Solution

A poor approach is creating separate classes for each type:

- `IntList`
- `StringList`
- `UserList`

This creates duplicated code.  
Generics solve this by making one reusable class.

### 4) Generic Classes

A generic class uses a type parameter like `<T>`.

```java
class Box<T> {
    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
```

Usage:

```java
Box<String> nameBox = new Box<>();
nameBox.setValue("Stefan");
```

### 5) Generics and Primitive Types

Generics work with reference types, not primitives.

So this is invalid:

```java
// Box<int> box = new Box<>(); // invalid
```

Use wrapper classes:

- `Integer` instead of `int`
- `Double` instead of `double`
- `Boolean` instead of `boolean`

### 6) Constraints

You can restrict generic types using bounds.

```java
class NumberBox<T extends Number> {
    private T value;
}
```

Now `T` must be `Number` or its subclass (like `Integer`, `Double`).

### 7) Type Erasure

Java generics are implemented with type erasure.

At runtime, generic type details are mostly removed, and Java uses raw types internally.

That is why you cannot do some things like:

- `new T()`
- checking exact generic type at runtime in simple ways

### 8) Comparable Interface

Generics often work with `Comparable<T>` for sorting/comparing.

```java
class User implements Comparable<User> {
    private String name;

    public int compareTo(User other) {
        return this.name.compareTo(other.name);
    }
}
```

This lets Java compare `User` objects safely and consistently.

### 9) Generic Methods

Methods can also be generic, even inside non-generic classes.

```java
public static <T> void printItem(T item) {
    System.out.println(item);
}
```

You can call it with many types:

```java
printItem("Hello");
printItem(123);
```

### 10) Multiple Type Parameters

A class or method can use multiple type parameters.

```java
class Pair<K, V> {
    private K key;
    private V value;
}
```

Useful for key-value style data and mapping scenarios.

### 11) Generic Classes and Inheritance

Generic types work with inheritance, but be careful:

- `List<Dog>` is **not** a subtype of `List<Animal>`

Even if `Dog` extends `Animal`, generic containers are invariant by default.

This prevents unsafe assignments.

### 12) Wildcards

Wildcards make generic APIs more flexible.

- `?` unknown type
- `? extends T` upper bound (read mostly)
- `? super T` lower bound (write mostly)

Example:

```java
public static void printNames(java.util.List<? extends CharSequence> items) {
    for (CharSequence item : items)
        System.out.println(item);
}
```

Now method accepts `List<String>`, `List<StringBuilder>`, etc.

### 13) Summary

Key points:

- Generics give type safety and reusability
- Use generic classes and methods to remove duplicate code
- Use bounds and wildcards for flexible but safe APIs
- Remember wrappers for primitive types
- Understand type erasure limitations

Generics are a core Java skill for writing clean, scalable code.
