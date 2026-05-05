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
