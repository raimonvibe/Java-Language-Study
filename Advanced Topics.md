# Advanced Topics

## Exceptions

### 1) Introduction

Exceptions are how Java reports problems that happen while a program is running.

Instead of crashing silently, Java gives you a clear error object you can handle.

Think of an exception like a fire alarm in a building:  
it tells you something went wrong and gives you a chance to respond safely.

Another way to think of it: exceptions are Java's "problem messages" between code parts.  
One method says, "I could not finish this safely," and another method decides what to do next.

### 2) What are Exceptions

An exception is an object that describes an error.

Example: dividing by zero.

```java
int result = 10 / 0; // ArithmeticException
```

If you do not handle it, the program stops and prints an error message.

Simple summary:

- Exception = an object that describes a failure.
- Throwing = reporting the failure.
- Catching = handling the failure.

### 3) Types of Exceptions

In simple terms, Java has:

- **Checked exceptions** - must be handled or declared (e.g., `IOException`)
- **Unchecked exceptions** - runtime errors (e.g., `NullPointerException`)
- **Errors** - serious JVM issues (usually not handled in app code)

Checked exceptions are verified by the compiler.

Beginner memory trick:

- Checked = "you must deal with me now."
- Unchecked = "you forgot a runtime safety check."
- Error = "the system itself is in serious trouble."

### 4) Exceptions Hierarchy

All exceptions come from `Throwable`.

High-level structure:

- `Throwable`
  - `Exception`
    - checked exceptions
    - `RuntimeException` (unchecked)
  - `Error`

Knowing this hierarchy helps you catch exceptions at the right level.

Why this matters:

- Catching a very broad type (like `Exception`) is easy but less precise.
- Catching a specific type (`IOException`, `ArithmeticException`) gives clearer handling.

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

Think of `try/catch` like a safety net:

- `try` = code that might fail
- `catch` = backup plan if it fails

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

Use one combined catch when the response is the same.  
Use separate catches when each type needs a different fix message or recovery action.

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

Think of `finally` like "always clean the desk before leaving," no matter what happened during work.

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

Why beginners love this:

- Less boilerplate
- Fewer forgotten `close()` calls
- Safer cleanup by default

### 9) Throwing Exceptions

Use `throw` when you want to signal an error yourself.

```java
public static void setAge(int age) {
    if (age < 0)
        throw new IllegalArgumentException("Age cannot be negative.");
}
```

This protects your methods from invalid input.

Think of `throw` as setting a boundary:

"If this input is invalid, I will stop here and report it clearly."

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

Common pattern:

1. low-level method catches and logs details
2. same exception (or wrapped one) is re-thrown
3. higher-level method decides user-facing behavior

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

Example use cases:

- `InvalidCouponCodeException`
- `InsufficientFundsException`
- `UserNotVerifiedException`

These names explain business problems better than generic exceptions.

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

Think of chaining like attaching a note to a package:

- outer exception = business context ("payment failed")
- inner exception = technical reason ("timeout in payment gateway")

### 13) Summary

Key ideas:

- Exceptions help you handle runtime problems safely
- Use `try/catch/finally` for control and cleanup
- Prefer `try-with-resources` for automatic closing
- Throw meaningful exceptions for invalid states
- Use custom and chained exceptions for clearer error handling

Good exception handling makes your code safer, cleaner, and easier to debug.

Simple summary:

- `try/catch` = handle problems
- `finally` / try-with-resources = always clean up
- `throw` = report invalid state early
- custom + chained exceptions = clearer debugging and maintenance

Quick use guide:

- use `try/catch` when you can recover locally
- re-throw when a higher layer should decide the response
- create custom exceptions for business/domain errors

How this connects:

- Exceptions are about writing safer code when things fail.
- Generics (next section) are about writing safer code when using types.
- Both reduce bugs early and make behavior more predictable.

---

## Generics

### 1) Introduction

Generics let you write classes and methods that work with different data types safely.

They help you avoid repeated code and reduce type-casting mistakes.

Think of generics like reusable containers with labels:  
the label (`<T>`) tells Java what can go inside.

### 2) The Need for Generics

Without generics, collections often store values as `Object`, and you must cast later.

That can cause runtime errors.

Generics move many of those errors to compile time, which is safer.

Real-life analogy:

- Without generics = unlabeled storage boxes, you open each box to see what is inside.
- With generics = labeled boxes, so you know what is valid before opening.

Simple summary:

- Generics catch type mistakes earlier.
- Earlier errors are easier and cheaper to fix.

### 3) A Poor Solution

A poor approach is creating separate classes for each type:

- `IntList`
- `StringList`
- `UserList`

This creates duplicated code.  
Generics solve this by making one reusable class.

Why this is poor:

- More files to maintain
- Same bug fixed in many places
- Harder to scale when new types appear

Simple summary:

- Many type-specific classes = repetition.
- One generic class = reuse.

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

You can create another box for a different type using the same class:

```java
Box<Integer> ageBox = new Box<>();
ageBox.setValue(25);
```

Simple summary:

- `T` is a placeholder for a real type.
- Java replaces `T` with the actual type you choose.

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

Why this exists:

- Generics rely on objects (reference types).
- Primitives are not objects, so wrappers bridge the gap.

Tip: Java autoboxing often converts automatically between primitive and wrapper types.

### 6) Constraints

You can restrict generic types using bounds.

```java
class NumberBox<T extends Number> {
    private T value;
}
```

Now `T` must be `Number` or its subclass (like `Integer`, `Double`).

Think of bounds as entry rules at a club:

- only types that match the rule can enter.

This gives you safer generic APIs because methods can rely on capabilities from the bound type.

### 7) Type Erasure

Java generics are implemented with type erasure.

At runtime, generic type details are mostly removed, and Java uses raw types internally.

That is why you cannot do some things like:

- `new T()`
- checking exact generic type at runtime in simple ways

Simple mental model:

- Compile time: Java checks generic type safety.
- Runtime: many generic details are erased.

That is why generics improve safety mostly during compilation.

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

In practice, `Comparable` defines the class's "default sort order" (like alphabetical by name).

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

Why use generic methods:

- Useful when one utility method should support many types.
- You avoid writing `printString`, `printInt`, `printUser`, etc.

### 10) Multiple Type Parameters

A class or method can use multiple type parameters.

```java
class Pair<K, V> {
    private K key;
    private V value;
}
```

Useful for key-value style data and mapping scenarios.

Simple summary:

- `<T>` = one flexible type
- `<K, V>` = two related flexible types

### 11) Generic Classes and Inheritance

Generic types work with inheritance, but be careful:

- `List<Dog>` is **not** a subtype of `List<Animal>`

Even if `Dog` extends `Animal`, generic containers are invariant by default.

This prevents unsafe assignments.

Why unsafe?

If `List<Dog>` were treated as `List<Animal>`, someone could insert a `Cat` into it, which would break type safety.

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

Beginner shortcut rule:

- `? extends T` -> good for reading from the structure
- `? super T` -> good for writing values into the structure

This is a common interview and real-world API design concept.

### 13) Summary

Key points:

- Generics give type safety and reusability
- Use generic classes and methods to remove duplicate code
- Use bounds and wildcards for flexible but safe APIs
- Remember wrappers for primitive types
- Understand type erasure limitations

Generics are a core Java skill for writing clean, scalable code.

Simple summary:

- Generics = reusable code + safer types
- Bounds/wildcards = flexible but controlled APIs
- Type erasure = why some runtime generic actions are limited

Quick use guide:

- use generics for reusable containers/utilities
- use bounds when APIs need specific capabilities
- use wildcards when accepting related type families

How this connects:

- Generics are used heavily inside collections like `List<T>` and `Map<K, V>`.
- So the next Collections section is where you see generics in everyday Java code.

---

## Collections

### 1) Introduction

Collections help you store and manage groups of objects in Java.

Instead of manually handling arrays for every case, the Collections Framework gives reusable data structures like lists, sets, queues, and maps.

Think of collections like different containers in real life:

- `List` = ordered notebook
- `Set` = unique sticker album (no duplicates)
- `Queue` = waiting line
- `Map` = dictionary (key -> meaning)

### 2) Overview of Collections Framework

Java Collections Framework is a set of interfaces + classes for working with grouped data.

Main parts:

- Interfaces (`List`, `Set`, `Queue`, `Map`)
- Implementations (`ArrayList`, `HashSet`, `PriorityQueue`, `HashMap`)
- Utility helpers (`Collections` class)

You usually code to interfaces, then choose the best implementation.

Beginner way to remember:

- Interface = the contract ("what it can do")
- Implementation = the engine ("how it does it")

So you can change the engine later without rewriting all your code.

### 3) The Need for Iterables

If you want custom objects to work in loops like `for-each`, Java needs a common way to traverse them.

That is why `Iterable` exists.

Without it, each class would need its own custom loop style.

Simple summary:

- `Iterable` gives Java a standard "walk through items" protocol.
- That is why `for-each` works across many different structures.

### 4) The Iterable Interface

`Iterable<T>` allows an object to be iterated in a `for-each` loop.

It requires one method:

- `iterator()`

```java
class Numbers implements Iterable<Integer> {
    public java.util.Iterator<Integer> iterator() {
        return java.util.List.of(1, 2, 3).iterator();
    }
}
```

Now you can do:

```java
for (int n : new Numbers())
    System.out.println(n);
```

Think of `Iterable` as saying:
"I know how to hand out my items one by one."

### 5) The Iterator Interface

`Iterator<T>` is used to move through elements one by one.

Common methods:

- `hasNext()`
- `next()`

```java
java.util.List<String> names = java.util.List.of("A", "B", "C");
java.util.Iterator<String> it = names.iterator();

while (it.hasNext())
    System.out.println(it.next());
```

Mental model:

- `hasNext()` asks: "Is there another item?"
- `next()` says: "Give me that next item."

### 6) The Collection Interface

`Collection<E>` is a root interface for many collection types (`List`, `Set`, `Queue`).

Common operations:

- `add()`
- `remove()`
- `contains()`
- `size()`
- `isEmpty()`

```java
java.util.Collection<String> items = new java.util.ArrayList<>();
items.add("Java");
items.add("Spring");
System.out.println(items.size()); // 2
```

Simple summary:

- `Collection` = base toolbox for grouped elements.
- `List`, `Set`, and `Queue` build on this toolbox.

### 7) The List Interface

`List<E>` is an ordered collection that allows duplicates.

Examples: `ArrayList`, `LinkedList`

```java
java.util.List<String> courses = new java.util.ArrayList<>();
courses.add("Java");
courses.add("Java");
courses.add("SQL");
System.out.println(courses.get(0)); // Java
```

Use `List` when order matters or duplicates are allowed.

Everyday analogy:

- A list is like a playlist.
- Order is important, and the same song can appear more than once.

### 8) The Comparable Interface

`Comparable<T>` defines natural ordering inside a class.

```java
class User implements Comparable<User> {
    String name;

    public int compareTo(User other) {
        return this.name.compareTo(other.name);
    }
}
```

Now Java knows how to sort `User` objects by default.

Use `Comparable` when your class has one natural default order (for example, by name or date).

### 9) The Comparator Interface

`Comparator<T>` defines external/custom sorting rules.

```java
java.util.Comparator<String> byLength =
        (a, b) -> Integer.compare(a.length(), b.length());
```

Use `Comparator` when you want multiple sorting strategies without changing class code.

Quick comparison:

- `Comparable` = default built-in order of class
- `Comparator` = custom order chosen from outside

### 10) The Queue Interface

`Queue<E>` is designed for processing elements in order, often FIFO (first in, first out).

Common methods:

- `offer()` add
- `poll()` remove head
- `peek()` read head

```java
java.util.Queue<String> queue = new java.util.ArrayDeque<>();
queue.offer("task1");
queue.offer("task2");
System.out.println(queue.poll()); // task1
```

Queue analogy:

- Like people standing in a checkout line.
- First person in line is first person served.

### 11) The Set Interface

`Set<E>` stores unique values (no duplicates).

Examples: `HashSet`, `LinkedHashSet`, `TreeSet`

```java
java.util.Set<String> tags = new java.util.HashSet<>();
tags.add("java");
tags.add("java");
System.out.println(tags.size()); // 1
```

Use `Set` when uniqueness matters.

Set analogy:

- Like a guest list where each name appears only once.

### 12) Hash Tables

Hash-based collections (`HashSet`, `HashMap`) use hashing for fast lookup.

Good average performance for add/find/remove is near O(1).

For custom objects in hash collections, correctly override:

- `equals()`
- `hashCode()`

These two must be consistent.

Beginner rule:

- If two objects are equal via `equals()`, they must return the same `hashCode()`.
- Breaking this rule causes strange behavior in `HashSet` and `HashMap`.

### 13) The Map Interface

`Map<K, V>` stores key-value pairs.

Keys are unique, values can repeat.

```java
java.util.Map<String, Integer> scores = new java.util.HashMap<>();
scores.put("Stefan", 95);
scores.put("Alex", 88);
System.out.println(scores.get("Stefan")); // 95
```

Useful methods:

- `put()`
- `get()`
- `containsKey()`
- `remove()`

Map analogy:

- Like a real dictionary: search by word (key) to get meaning (value).

### 14) Summary

Key takeaways:

- Use `List` for ordered data with duplicates
- Use `Set` for unique data
- Use `Queue` for processing flow
- Use `Map` for key-value lookups
- Use `Comparable`/`Comparator` for sorting

Choosing the right collection makes your code simpler and more efficient.

Simple summary:

- `List` = ordered + duplicates allowed
- `Set` = unique values only
- `Queue` = processing order
- `Map` = key -> value lookup

Quick use guide:

- choose `ArrayList` for most list use cases
- choose `HashSet` for fast uniqueness checks
- choose `HashMap` for fast key-value lookup

How this connects:

- Collections answer "where data is stored."
- Lambda and functional interfaces (next section) answer "how behavior is passed."
- Streams (later) combine both: collection data + functional operations.

---

## Lambda Expressions and Functional Interfaces

### 1) Introduction

Lambdas let you write shorter, cleaner code for behavior you want to pass around.

They are heavily used with collections, streams, and modern Java APIs.

Think of a lambda as a mini function you can pass like data.

Simple summary:

- Functional interface = shape/rule of behavior
- Lambda = quick implementation of that behavior

### 2) Functional Interfaces

A functional interface has exactly one abstract method.

```java
@FunctionalInterface
interface Printer {
    void print(String message);
}
```

This interface can be implemented with a lambda.

Think of a functional interface like a plug shape:  
any lambda with matching method signature can fit into it.

### 3) Anonymous Inner Classes

Before lambdas, Java often used anonymous classes for short behavior.

```java
Printer p = new Printer() {
    public void print(String message) {
        System.out.println(message);
    }
};
```

This works, but it is verbose.

So lambdas are mostly about readability and less boilerplate, not new capability.

### 4) Lambda Expressions

A lambda is a shorter way to implement a functional interface.

```java
Printer p = message -> System.out.println(message);
p.print("Hello");
```

Same behavior, less boilerplate.

Beginner shortcut:

- If interface has one abstract method, lambda is usually the cleanest implementation style.

### 5) Variable Capture

Lambdas can use local variables from surrounding scope, but those variables must be final or effectively final.

```java
String prefix = "Log: ";
Printer p = msg -> System.out.println(prefix + msg);
```

If you reassign `prefix`, Java will reject it.

Why this rule exists:

- It prevents confusing behavior when lambdas run later.
- Java keeps captured local values stable and predictable.

### 6) Method References

Method references are shortcuts when a lambda only calls one method.

```java
Printer p = System.out::println;
p.print("Hello");
```

They improve readability in many cases.

Rule of thumb:

- If method reference is clearer than lambda, use it.
- If lambda explains intent better, keep lambda.

### 7) Built-in Functional Interfaces

Java provides common functional interfaces in `java.util.function`, such as:

- `Consumer<T>`
- `Supplier<T>`
- `Function<T, R>`
- `Predicate<T>`
- `BinaryOperator<T>`
- `UnaryOperator<T>`

Use these instead of creating new interfaces when possible.

Simple cheat sheet:

- `Consumer<T>` -> takes input, returns nothing
- `Supplier<T>` -> takes nothing, returns value
- `Function<T, R>` -> converts T to R
- `Predicate<T>` -> returns true/false

### 8) The Consumer Interface

`Consumer<T>` takes a value and returns nothing.

```java
java.util.function.Consumer<String> print = s -> System.out.println(s);
print.accept("Java");
```

Good for side effects like logging or printing.

Consumer analogy:

- Like a machine that consumes an item and performs an action, but does not give a new item back.

### 9) Chaining Consumer

You can chain consumers with `andThen`.

```java
java.util.function.Consumer<String> c1 = s -> System.out.println("First: " + s);
java.util.function.Consumer<String> c2 = s -> System.out.println("Second: " + s);

c1.andThen(c2).accept("Item");
```

Both run in order.

Great for building step-by-step processing flows (for example, validate then log).

### 10) The Supplier Interface

`Supplier<T>` provides a value and takes no input.

```java
java.util.function.Supplier<Double> random = () -> Math.random();
System.out.println(random.get());
```

Useful for lazy value creation.

Supplier analogy:

- Like a vending machine: you ask, it gives you one value.

### 11) The Function Interface

`Function<T, R>` transforms one value into another.

```java
java.util.function.Function<String, Integer> length = s -> s.length();
System.out.println(length.apply("Java")); // 4
```

Great for mapping/converting data.

Function analogy:

- Input goes in, transformed output comes out.

### 12) Composing Functions

Functions can be combined using `andThen` and `compose`.

```java
java.util.function.Function<Integer, Integer> times2 = x -> x * 2;
java.util.function.Function<Integer, Integer> plus1 = x -> x + 1;

System.out.println(times2.andThen(plus1).apply(3)); // 7
```

Composition helps build reusable processing pipelines.

Think of composition like snapping Lego pieces together to create bigger behavior from small reusable parts.

### 13) The Predicate Interface

`Predicate<T>` checks a condition and returns boolean.

```java
java.util.function.Predicate<String> isLong = s -> s.length() > 5;
System.out.println(isLong.test("Stefan")); // true
```

Useful for filtering data.

Predicate analogy:

- Like a yes/no gate that decides whether an item passes.

### 14) Combining Predicates

Combine predicates using `and`, `or`, and `negate`.

```java
java.util.function.Predicate<String> startsWithA = s -> s.startsWith("A");
java.util.function.Predicate<String> longName = s -> s.length() > 3;

System.out.println(startsWithA.and(longName).test("Alex")); // true
```

This keeps conditions modular and readable.

This is especially helpful when business rules grow and you want to combine small rules cleanly.

### 15) The BinaryOperator Interface

`BinaryOperator<T>` takes two values of same type and returns one value of same type.

```java
java.util.function.BinaryOperator<Integer> add = (a, b) -> a + b;
System.out.println(add.apply(2, 3)); // 5
```

Useful for combining or reducing values.

Common use case: totals, sums, minimum/maximum comparisons.

### 16) The UnaryOperator Interface

`UnaryOperator<T>` takes one value and returns same type.

```java
java.util.function.UnaryOperator<Integer> square = x -> x * x;
System.out.println(square.apply(4)); // 16
```

Useful for same-type transformations.

Example use case: clean text, normalize values, or apply repeated transformations.

### 17) Summary

Key points:

- Lambdas simplify functional-style coding
- Functional interfaces define single-behavior contracts
- Built-in interfaces cover most common cases
- Composition/chaining creates reusable logic

These features help you write concise, expressive, and modern Java code.

Simple summary:

- Lambdas make behavior easier to pass
- Functional interfaces standardize common behavior patterns
- Chaining/composition helps build reusable logic blocks

Quick use guide:

- use lambdas for short one-method behaviors
- use built-in functional interfaces before creating custom ones
- compose small functions/predicates instead of one large expression

How this connects:

- Functional interfaces define behavior contracts.
- Lambdas provide quick implementations of those contracts.
- Streams (next section) use this style everywhere (`map`, `filter`, `reduce`).

---

## Streams

### 1) Introduction

Streams let you process collections of data in a clean, pipeline style.

You can chain operations like filter, map, sort, and collect in a readable way.

Think of a stream pipeline like a factory line:

- `filter` removes unwanted items
- `map` transforms items
- `collect` packs the final result

Simple summary:

- Stream = data flow
- Intermediate operations (`map`, `filter`, `sorted`) = steps in pipeline
- Terminal operation (`toList`, `count`, `collect`) = final result

### 2) Imperative vs Functional Programming

Imperative style says **how** to do steps (loops, temp variables).  
Functional style says **what** result you want.

Imperative:

```java
java.util.List<String> result = new java.util.ArrayList<>();
for (String name : java.util.List.of("alex", "bob"))
    result.add(name.toUpperCase());
```

Functional (stream):

```java
java.util.List<String> result = java.util.List.of("alex", "bob")
        .stream()
        .map(String::toUpperCase)
        .toList();
```

Both work, but functional style is often shorter and clearer for data transformation.

When to choose streams:

- You are transforming/filtering data
- You want clear "pipeline" logic

When a loop is still fine:

- Very simple one-step logic
- You need detailed index-based control

### 3) Creating a Stream

You can create streams from:

- collections: `list.stream()`
- arrays: `Arrays.stream(array)`
- values: `Stream.of(...)`
- ranges: `IntStream.range(...)`

```java
java.util.stream.Stream<String> stream = java.util.stream.Stream.of("A", "B", "C");
```

Tip:

- Streams are single-use.  
  After a terminal operation, create a new stream if you need to process data again.

### 4) Mapping Elements

`map()` transforms each element into something else.

```java
java.util.List<Integer> lengths = java.util.List.of("Java", "Stream")
        .stream()
        .map(String::length)
        .toList();
```

`"Java"` becomes `4`, `"Stream"` becomes `6`.

Think of `map` as "convert each item into a new shape."

### 5) Filtering Elements

`filter()` keeps only elements that match a condition.

```java
java.util.List<String> longNames = java.util.List.of("Al", "Alex", "Sam")
        .stream()
        .filter(name -> name.length() > 3)
        .toList();
```

Think of `filter` as a sieve: only matching items pass through.

### 6) Slicing Streams

Use:

- `limit(n)` to keep first `n` items
- `skip(n)` to skip first `n` items
- `takeWhile(...)` / `dropWhile(...)` (ordered streams)

```java
java.util.List<Integer> sliced = java.util.List.of(1, 2, 3, 4, 5)
        .stream()
        .skip(1)
        .limit(3)
        .toList(); // [2, 3, 4]
```

Slicing is useful for pagination-style logic (skip page start, limit page size).

### 7) Sorting Streams

Use `sorted()` for natural ordering, or pass a comparator for custom order.

```java
java.util.List<String> sorted = java.util.List.of("Bob", "Alex", "Chris")
        .stream()
        .sorted()
        .toList();
```

Custom sort:

```java
java.util.List<String> byLength = java.util.List.of("Bob", "Alexander", "Chris")
        .stream()
        .sorted(java.util.Comparator.comparingInt(String::length))
        .toList();
```

### 8) Getting Unique Elements

Use `distinct()` to remove duplicates.

```java
java.util.List<Integer> unique = java.util.List.of(1, 2, 2, 3, 3, 3)
        .stream()
        .distinct()
        .toList(); // [1, 2, 3]
```

`distinct()` uses equality rules, so for custom objects you may need proper `equals()` and `hashCode()`.

### 9) Peeking Elements

`peek()` is useful for debugging stream pipelines.

```java
java.util.List.of("a", "b", "c")
        .stream()
        .peek(x -> System.out.println("Before: " + x))
        .map(String::toUpperCase)
        .peek(x -> System.out.println("After: " + x))
        .toList();
```

Avoid using `peek()` for important business side effects.

Use `peek()` mainly as a debug checkpoint while learning or troubleshooting pipelines.

### 10) Simple Reducers

Reducers compute a single value from stream data:

- `count()`
- `anyMatch()`, `allMatch()`, `noneMatch()`
- `findFirst()`, `findAny()`

```java
long count = java.util.List.of("A", "B", "C").stream().count();
```

These reducers are great when you only need one answer, not a whole new list.

### 11) Reducing a Stream

Use `reduce()` to combine elements into one result.

```java
int sum = java.util.List.of(1, 2, 3, 4)
        .stream()
        .reduce(0, Integer::sum);
```

`0` is identity, and `Integer::sum` combines values.

Think of `reduce` as folding many values into one final value.

### 12) Collectors

Collectors convert stream results into containers or summaries.

```java
java.util.List<String> list = java.util.List.of("a", "b")
        .stream()
        .map(String::toUpperCase)
        .collect(java.util.stream.Collectors.toList());
```

Common collectors:

- `toList()`
- `toSet()`
- `toMap()`
- `joining()`
- `counting()`

Collector analogy:

- Stream pipeline builds items.
- Collector decides what container/final format they should end up in.

### 13) Grouping Elements

`groupingBy()` groups elements by a key.

```java
java.util.Map<Integer, java.util.List<String>> grouped = java.util.List.of("a", "bb", "cc", "ddd")
        .stream()
        .collect(java.util.stream.Collectors.groupingBy(String::length));
```

Now items are grouped by string length.

Grouping is like creating labeled buckets, then dropping each item into its matching bucket.

### 14) Partitioning Elements

`partitioningBy()` splits elements into two groups (`true` / `false`) based on a predicate.

```java
java.util.Map<Boolean, java.util.List<Integer>> partitioned = java.util.List.of(1, 2, 3, 4)
        .stream()
        .collect(java.util.stream.Collectors.partitioningBy(n -> n % 2 == 0));
```

Partitioning is a special case of grouping with only two buckets: true and false.

### 15) Primitive Type Streams

Java has specialized streams for primitives:

- `IntStream`
- `LongStream`
- `DoubleStream`

They avoid boxing overhead and include numeric helpers.

```java
int total = java.util.stream.IntStream.rangeClosed(1, 5).sum(); // 15
```

Use primitive streams in number-heavy code for better performance and less boxing overhead.

### 16) Summary

Streams help you process data with readable, chainable operations.

Key ideas:

- Create pipelines with map/filter/sort
- Use reducers and collectors for final results
- Use grouping/partitioning for structured outputs
- Prefer primitive streams for number-heavy operations

Once mastered, streams make data-processing code cleaner and more expressive.

Simple summary:

- `map` transforms
- `filter` selects
- `reduce` combines
- `collect` packages results

How this connects:

- Streams build directly on collections + lambdas.
- Concurrency (next section) focuses on running tasks safely in parallel.
- Later, Executor Framework combines concurrency with practical APIs.

---

## Concurrency and Multi-threading

### 1) Introduction

Concurrency means handling multiple tasks at the same time.

In Java, this is often done with threads so programs can be more responsive and make better use of CPU resources.

Think of threads like multiple workers in one kitchen preparing parts of a meal.

Simple summary:

- Concurrency = dealing with multiple tasks at once
- Thread = one worker doing one path of execution
- Main challenge = workers sharing the same data safely

### 2) Processes and Threads

- A **process** is a running program with its own memory space.
- A **thread** is a smaller execution unit inside a process.

One process can have many threads sharing the same memory.

That shared memory is powerful but also the main source of concurrency bugs.

### 3) Starting a Thread

You can start a new thread by passing code (a `Runnable`) to `Thread`.

```java
Thread thread = new Thread(() -> System.out.println("Running in thread"));
thread.start();
```

Use `start()`, not `run()`, to actually create a separate thread.

Common beginner mistake:

- calling `run()` executes on current thread
- calling `start()` asks JVM to run on a new thread

### 4) Pausing a Thread

Use `Thread.sleep(milliseconds)` to pause current thread.

```java
try {
    Thread.sleep(1000);
} catch (InterruptedException e) {
    Thread.currentThread().interrupt();
}
```

Sleeping is useful for delays, retries, or simulation.

### 5) Joining a Thread

`join()` makes one thread wait until another finishes.

```java
Thread worker = new Thread(() -> System.out.println("Work done"));
worker.start();
worker.join(); // wait for worker
```

This helps coordinate task order.

Use `join()` when a result depends on another thread finishing first.

### 6) Interrupting a Thread

Interrupting asks a thread to stop what it is doing.

```java
thread.interrupt();
```

In long-running code, check interrupt status and exit gracefully.

Think of interruption as a polite stop request, not a force-kill.

### 7) Concurrency Issues

Multiple threads sharing mutable data can cause bugs like:

- lost updates
- inconsistent reads
- unexpected ordering

These bugs are often hard to reproduce.

Because timing changes from run to run, concurrency bugs may appear "random."

### 8) Race Conditions

A race condition happens when result depends on thread timing.

Example: two threads increment same counter at once and one update is lost.

```java
counter++; // not atomic
```

`counter++` is multiple steps, not one safe operation.

Simple summary:

- Race condition = outcome depends on who runs first
- Same code can give different results on different runs

### 9) Strategies for Thread Safety

Common strategies:

- Avoid shared mutable state
- Use immutable objects
- Use synchronization/locks
- Use thread-safe collections/atomic classes

Pick the simplest strategy that solves the problem.

Beginner order of preference:

1. avoid sharing mutable state
2. use immutable data where possible
3. then add synchronization tools only where needed

### 10) Confinement

Confinement means limiting data to one thread only.

If only one thread can access data, no synchronization is needed for that data.

Example: local variables inside a method are thread-confined.

Confinement is often the easiest and safest thread-safety strategy.

### 11) Locks

Locks ensure only one thread accesses critical code at a time.

```java
java.util.concurrent.locks.Lock lock = new java.util.concurrent.locks.ReentrantLock();
lock.lock();
try {
    // critical section
} finally {
    lock.unlock();
}
```

Always unlock in `finally`.

If you forget to unlock, other threads can get stuck waiting forever.

### 12) The synchronized Keyword

`synchronized` is built-in Java locking.

```java
public synchronized void increment() {
    count++;
}
```

Only one thread can run this synchronized method on same object at once.

Think of `synchronized` as putting a "one person at a time" sign on critical code.

### 13) The volatile Keyword

`volatile` ensures changes to a variable are visible across threads quickly.

```java
private volatile boolean running = true;
```

Use it for visibility, not for compound atomic operations (like `count++`).

Quick rule:

- `volatile` solves visibility
- `synchronized`/atomic classes solve atomicity

### 14) Thread Signalling with wait() and notify()

Threads can coordinate by waiting and notifying on same monitor object.

```java
synchronized (lock) {
    lock.wait();   // releases lock and waits
    lock.notify(); // wakes one waiting thread
}
```

Usually used in producer-consumer style coordination.

Important:

- `wait()` and `notify()` must be called inside synchronized context on the same monitor object.

### 15) Atomic Objects

Atomic classes perform thread-safe operations without manual locks.

```java
java.util.concurrent.atomic.AtomicInteger counter = new java.util.concurrent.atomic.AtomicInteger();
counter.incrementAndGet();
```

Great for counters and simple shared numeric state.

Atomic classes are often easier than manual locking for simple shared values.

### 16) Adders

`LongAdder` / `DoubleAdder` are optimized for high-contention counters.

```java
java.util.concurrent.atomic.LongAdder adder = new java.util.concurrent.atomic.LongAdder();
adder.increment();
long total = adder.sum();
```

Often faster than `AtomicLong` under heavy parallel updates.

Use adders mainly in high-write, high-contention counter scenarios.

### 17) Synchronized Collections

Java provides synchronized wrappers:

```java
java.util.List<String> list = java.util.Collections.synchronizedList(new java.util.ArrayList<>());
```

They are thread-safe but can become bottlenecks under heavy concurrency.

Good for simple cases, but not always best for highly parallel workloads.

### 18) Concurrent Collections

`java.util.concurrent` has collections built for concurrency, like:

- `ConcurrentHashMap`
- `CopyOnWriteArrayList`
- `ConcurrentLinkedQueue`

They usually scale better than synchronized wrappers.

Simple summary:

- synchronized wrappers = easy, coarse locking
- concurrent collections = designed for better parallel throughput

### 19) Summary

Key ideas:

- Threads improve responsiveness and throughput
- Shared mutable state causes most concurrency bugs
- Use synchronization, locks, atomic classes, and concurrent collections carefully
- Prefer simple, clear thread-safe design first

Concurrency is powerful, but correctness comes before speed.

Simple summary:

- First make shared-state code correct
- Then optimize performance if needed
- Debugging wrong concurrent logic is much harder than writing safe logic first

Quick use guide:

- start with confinement/immutability when possible
- use atomics for simple shared counters/flags
- use locks/synchronized only for true critical sections

How this connects:

- This section explains thread-safety foundations.
- The Executor Framework (next section) gives higher-level tools so you do not manage every thread manually.

---

## The Executor Framework

### 1) Introduction

The Executor Framework helps you manage threads in a cleaner and safer way than creating threads manually.

It is a core part of modern concurrent programming in Java.

Think of it as a task manager:  
you submit jobs, and the framework decides which worker thread runs them.

Simple summary:

- You focus on tasks.
- Framework focuses on thread management.

### 2) Thread Pools

A thread pool is a group of reusable worker threads.

Instead of creating a new thread for each task, tasks are submitted to the pool.

Benefits:

- better performance
- less thread-creation overhead
- controlled resource usage

Thread pool analogy:

- Like a team of workers already in office.
- New task arrives -> assign to available worker.
- No need to hire a brand-new worker every time.

### 3) Executors

The `Executors` utility class creates common executor types.

```java
java.util.concurrent.ExecutorService executor =
        java.util.concurrent.Executors.newFixedThreadPool(4);

executor.submit(() -> System.out.println("Task running"));
executor.shutdown();
```

Common factories:

- `newFixedThreadPool(n)`
- `newCachedThreadPool()`
- `newSingleThreadExecutor()`

Quick choosing guide:

- fixed pool -> stable, predictable concurrency
- cached pool -> short-lived bursty tasks
- single-thread executor -> tasks must run one-by-one in order

### 4) Callables and Futures

`Runnable` does not return a value.  
`Callable<T>` can return a value (and throw exceptions).

```java
java.util.concurrent.Future<Integer> future = executor.submit(() -> 1 + 2);
int result = future.get(); // blocks until done
```

`Future` represents a result that will be available later.

Analogy: ordering takeout food

- `Callable` = the chef who cooks and returns your meal
- `Future` = your receipt/ticket

You get the receipt immediately, but the food may still be cooking.

You can check or wait for the result later.

```java
java.util.concurrent.Callable<Integer> task = () -> {
    // do some work...
    return 42;
};

java.util.concurrent.Future<Integer> future = executor.submit(task);

// later...
Integer result = future.get(); // waits until ready
```

Simple summary:

- `Callable` = task that returns something
- `Future` = placeholder for result that arrives later

### 5) Asynchronous Programming

Asynchronous programming means starting tasks without blocking current thread immediately.

This improves responsiveness, especially for I/O or remote calls.

Simple idea:

- synchronous: do task A, wait, then do task B
- asynchronous: start task A, continue with task B, collect A later

### 6) Completable Futures

`CompletableFuture` is a powerful API for async workflows.

It supports:

- callbacks on completion
- transformations
- composition/combination
- exception handling

`CompletableFuture` is like a programmable future: you can attach next steps instead of only waiting with `get()`.

### 7) Creating a Completable Future

You can create one with `supplyAsync` or `runAsync`.

```java
java.util.concurrent.CompletableFuture<Integer> future =
        java.util.concurrent.CompletableFuture.supplyAsync(() -> 42);
```

Use `runAsync` for no return value, and `supplyAsync` when you want a returned result.

### 8) Implementing an Asynchronous API

Instead of returning a direct value, return `CompletableFuture<T>`.

```java
public java.util.concurrent.CompletableFuture<String> getUserNameAsync() {
    return java.util.concurrent.CompletableFuture.supplyAsync(() -> "Stefan");
}
```

This allows caller to continue doing other work.

This is how you design non-blocking service methods in modern Java applications.

### 9) Running Code on Completion

Use completion methods:

- `thenRun()`
- `thenAccept()`
- `thenApply()`

```java
future.thenAccept(value -> System.out.println("Done: " + value));
```

Think of this as: "When task finishes, run this callback."

### 10) Handling Exceptions

Use `exceptionally`, `handle`, or `whenComplete`.

```java
future.exceptionally(ex -> {
    System.out.println("Error: " + ex.getMessage());
    return -1;
});
```

This prevents async failures from being ignored.

Without explicit handling, async exceptions are easy to miss.

### 11) Transforming a Completable Future

Use `thenApply` to transform result value.

```java
java.util.concurrent.CompletableFuture<String> nameFuture =
        java.util.concurrent.CompletableFuture.supplyAsync(() -> "stefan")
                .thenApply(String::toUpperCase);
```

`thenApply` = transform result value (T -> R) when it arrives.

### 12) Composing Completable Futures

Use `thenCompose` when second async task depends on first result.

```java
java.util.concurrent.CompletableFuture<String> composed =
        getUserNameAsync().thenCompose(name -> getGreetingAsync(name));
```

This avoids nested futures.

Rule of thumb:

- `thenApply` for normal transformation
- `thenCompose` when next step returns another future

### 13) Combining Completable Futures

Use `thenCombine` when two independent futures both produce needed values.

```java
futureA.thenCombine(futureB, (a, b) -> a + " " + b);
```

Use this when two tasks are independent and you need both outputs.

### 14) Waiting for Many Tasks to Complete

Use `CompletableFuture.allOf(...)`.

```java
java.util.concurrent.CompletableFuture<Void> all =
        java.util.concurrent.CompletableFuture.allOf(future1, future2, future3);
all.join();
```

Useful when all tasks must finish first.

`allOf` is like "wait until every team member reports done."

### 15) Waiting for the First Task

Use `CompletableFuture.anyOf(...)` to continue with first completed task.

```java
java.util.concurrent.CompletableFuture<Object> first =
        java.util.concurrent.CompletableFuture.anyOf(future1, future2);
```

Great for race/fastest-response scenarios.

`anyOf` is like "use whichever response arrives first."

### 16) Handling Timeouts

You can limit waiting time for futures.

```java
future.orTimeout(2, java.util.concurrent.TimeUnit.SECONDS);
```

Or provide fallback:

```java
future.completeOnTimeout("default", 2, java.util.concurrent.TimeUnit.SECONDS);
```

Timeouts protect your app from waiting forever on slow external systems.

### 17) Project - Best Price Finder

Project idea: fetch product quotes from multiple online stores and show best price.

Why this project is great:

- multiple independent tasks
- async calls
- combining results
- timeout/error handling

This project combines nearly every core async concept in one realistic scenario.

### 18) Solution - Getting a Quote

Each store API call can return a `CompletableFuture<Quote>`.

```java
public java.util.concurrent.CompletableFuture<Double> getQuoteAsync(String store) {
    return java.util.concurrent.CompletableFuture.supplyAsync(() -> fetchPrice(store));
}
```

### 19) Solution - Getting Many Quotes

Call many stores concurrently, then wait for all.

```java
java.util.List<java.util.concurrent.CompletableFuture<Double>> futures = stores.stream()
        .map(this::getQuoteAsync)
        .toList();

java.util.concurrent.CompletableFuture.allOf(futures.toArray(new java.util.concurrent.CompletableFuture[0])).join();
```

Then collect results and choose minimum.

This pattern is common in travel search, shopping comparison, and price aggregator systems.

### 20) Solution - Random Delays

Real APIs have different response speeds. Simulating random delays helps test timeout handling and UI behavior.

Example idea:

- add random sleep inside mock `fetchPrice`
- test which store returns first
- verify fallback if a store is too slow

This prepares your async code for real-world network behavior.

Simple summary:

- Use executors for controlled threading
- Use futures for delayed results
- Use `CompletableFuture` for chaining async workflows
- Use timeouts and fallbacks for reliability

Quick use guide:

- use `ExecutorService` for task execution control
- use `Future` when you only need a later result
- use `CompletableFuture` for multi-step async pipelines
