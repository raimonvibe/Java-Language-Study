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

---

## Collections

### 1) Introduction

Collections help you store and manage groups of objects in Java.

Instead of manually handling arrays for every case, the Collections Framework gives reusable data structures like lists, sets, queues, and maps.

### 2) Overview of Collections Framework

Java Collections Framework is a set of interfaces + classes for working with grouped data.

Main parts:

- Interfaces (`List`, `Set`, `Queue`, `Map`)
- Implementations (`ArrayList`, `HashSet`, `PriorityQueue`, `HashMap`)
- Utility helpers (`Collections` class)

You usually code to interfaces, then choose the best implementation.

### 3) The Need for Iterables

If you want custom objects to work in loops like `for-each`, Java needs a common way to traverse them.

That is why `Iterable` exists.

Without it, each class would need its own custom loop style.

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

### 9) The Comparator Interface

`Comparator<T>` defines external/custom sorting rules.

```java
java.util.Comparator<String> byLength =
        (a, b) -> Integer.compare(a.length(), b.length());
```

Use `Comparator` when you want multiple sorting strategies without changing class code.

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

### 12) Hash Tables

Hash-based collections (`HashSet`, `HashMap`) use hashing for fast lookup.

Good average performance for add/find/remove is near O(1).

For custom objects in hash collections, correctly override:

- `equals()`
- `hashCode()`

These two must be consistent.

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

### 14) Summary

Key takeaways:

- Use `List` for ordered data with duplicates
- Use `Set` for unique data
- Use `Queue` for processing flow
- Use `Map` for key-value lookups
- Use `Comparable`/`Comparator` for sorting

Choosing the right collection makes your code simpler and more efficient.

---

## Lambda Expressions and Functional Interfaces

### 1) Introduction

Lambdas let you write shorter, cleaner code for behavior you want to pass around.

They are heavily used with collections, streams, and modern Java APIs.

### 2) Functional Interfaces

A functional interface has exactly one abstract method.

```java
@FunctionalInterface
interface Printer {
    void print(String message);
}
```

This interface can be implemented with a lambda.

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

### 4) Lambda Expressions

A lambda is a shorter way to implement a functional interface.

```java
Printer p = message -> System.out.println(message);
p.print("Hello");
```

Same behavior, less boilerplate.

### 5) Variable Capture

Lambdas can use local variables from surrounding scope, but those variables must be final or effectively final.

```java
String prefix = "Log: ";
Printer p = msg -> System.out.println(prefix + msg);
```

If you reassign `prefix`, Java will reject it.

### 6) Method References

Method references are shortcuts when a lambda only calls one method.

```java
Printer p = System.out::println;
p.print("Hello");
```

They improve readability in many cases.

### 7) Built-in Functional Interfaces

Java provides common functional interfaces in `java.util.function`, such as:

- `Consumer<T>`
- `Supplier<T>`
- `Function<T, R>`
- `Predicate<T>`
- `BinaryOperator<T>`
- `UnaryOperator<T>`

Use these instead of creating new interfaces when possible.

### 8) The Consumer Interface

`Consumer<T>` takes a value and returns nothing.

```java
java.util.function.Consumer<String> print = s -> System.out.println(s);
print.accept("Java");
```

Good for side effects like logging or printing.

### 9) Chaining Consumer

You can chain consumers with `andThen`.

```java
java.util.function.Consumer<String> c1 = s -> System.out.println("First: " + s);
java.util.function.Consumer<String> c2 = s -> System.out.println("Second: " + s);

c1.andThen(c2).accept("Item");
```

Both run in order.

### 10) The Supplier Interface

`Supplier<T>` provides a value and takes no input.

```java
java.util.function.Supplier<Double> random = () -> Math.random();
System.out.println(random.get());
```

Useful for lazy value creation.

### 11) The Function Interface

`Function<T, R>` transforms one value into another.

```java
java.util.function.Function<String, Integer> length = s -> s.length();
System.out.println(length.apply("Java")); // 4
```

Great for mapping/converting data.

### 12) Composing Functions

Functions can be combined using `andThen` and `compose`.

```java
java.util.function.Function<Integer, Integer> times2 = x -> x * 2;
java.util.function.Function<Integer, Integer> plus1 = x -> x + 1;

System.out.println(times2.andThen(plus1).apply(3)); // 7
```

Composition helps build reusable processing pipelines.

### 13) The Predicate Interface

`Predicate<T>` checks a condition and returns boolean.

```java
java.util.function.Predicate<String> isLong = s -> s.length() > 5;
System.out.println(isLong.test("Stefan")); // true
```

Useful for filtering data.

### 14) Combining Predicates

Combine predicates using `and`, `or`, and `negate`.

```java
java.util.function.Predicate<String> startsWithA = s -> s.startsWith("A");
java.util.function.Predicate<String> longName = s -> s.length() > 3;

System.out.println(startsWithA.and(longName).test("Alex")); // true
```

This keeps conditions modular and readable.

### 15) The BinaryOperator Interface

`BinaryOperator<T>` takes two values of same type and returns one value of same type.

```java
java.util.function.BinaryOperator<Integer> add = (a, b) -> a + b;
System.out.println(add.apply(2, 3)); // 5
```

Useful for combining or reducing values.

### 16) The UnaryOperator Interface

`UnaryOperator<T>` takes one value and returns same type.

```java
java.util.function.UnaryOperator<Integer> square = x -> x * x;
System.out.println(square.apply(4)); // 16
```

Useful for same-type transformations.

### 17) Summary

Key points:

- Lambdas simplify functional-style coding
- Functional interfaces define single-behavior contracts
- Built-in interfaces cover most common cases
- Composition/chaining creates reusable logic

These features help you write concise, expressive, and modern Java code.

---

## Streams

### 1) Introduction

Streams let you process collections of data in a clean, pipeline style.

You can chain operations like filter, map, sort, and collect in a readable way.

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

### 3) Creating a Stream

You can create streams from:

- collections: `list.stream()`
- arrays: `Arrays.stream(array)`
- values: `Stream.of(...)`
- ranges: `IntStream.range(...)`

```java
java.util.stream.Stream<String> stream = java.util.stream.Stream.of("A", "B", "C");
```

### 4) Mapping Elements

`map()` transforms each element into something else.

```java
java.util.List<Integer> lengths = java.util.List.of("Java", "Stream")
        .stream()
        .map(String::length)
        .toList();
```

`"Java"` becomes `4`, `"Stream"` becomes `6`.

### 5) Filtering Elements

`filter()` keeps only elements that match a condition.

```java
java.util.List<String> longNames = java.util.List.of("Al", "Alex", "Sam")
        .stream()
        .filter(name -> name.length() > 3)
        .toList();
```

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

### 10) Simple Reducers

Reducers compute a single value from stream data:

- `count()`
- `anyMatch()`, `allMatch()`, `noneMatch()`
- `findFirst()`, `findAny()`

```java
long count = java.util.List.of("A", "B", "C").stream().count();
```

### 11) Reducing a Stream

Use `reduce()` to combine elements into one result.

```java
int sum = java.util.List.of(1, 2, 3, 4)
        .stream()
        .reduce(0, Integer::sum);
```

`0` is identity, and `Integer::sum` combines values.

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

### 13) Grouping Elements

`groupingBy()` groups elements by a key.

```java
java.util.Map<Integer, java.util.List<String>> grouped = java.util.List.of("a", "bb", "cc", "ddd")
        .stream()
        .collect(java.util.stream.Collectors.groupingBy(String::length));
```

Now items are grouped by string length.

### 14) Partitioning Elements

`partitioningBy()` splits elements into two groups (`true` / `false`) based on a predicate.

```java
java.util.Map<Boolean, java.util.List<Integer>> partitioned = java.util.List.of(1, 2, 3, 4)
        .stream()
        .collect(java.util.stream.Collectors.partitioningBy(n -> n % 2 == 0));
```

### 15) Primitive Type Streams

Java has specialized streams for primitives:

- `IntStream`
- `LongStream`
- `DoubleStream`

They avoid boxing overhead and include numeric helpers.

```java
int total = java.util.stream.IntStream.rangeClosed(1, 5).sum(); // 15
```

### 16) Summary

Streams help you process data with readable, chainable operations.

Key ideas:

- Create pipelines with map/filter/sort
- Use reducers and collectors for final results
- Use grouping/partitioning for structured outputs
- Prefer primitive streams for number-heavy operations

Once mastered, streams make data-processing code cleaner and more expressive.

---

## Concurrency and Multi-threading

### 1) Introduction

Concurrency means handling multiple tasks at the same time.

In Java, this is often done with threads so programs can be more responsive and make better use of CPU resources.

### 2) Processes and Threads

- A **process** is a running program with its own memory space.
- A **thread** is a smaller execution unit inside a process.

One process can have many threads sharing the same memory.

### 3) Starting a Thread

You can start a new thread by passing code (a `Runnable`) to `Thread`.

```java
Thread thread = new Thread(() -> System.out.println("Running in thread"));
thread.start();
```

Use `start()`, not `run()`, to actually create a separate thread.

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

### 6) Interrupting a Thread

Interrupting asks a thread to stop what it is doing.

```java
thread.interrupt();
```

In long-running code, check interrupt status and exit gracefully.

### 7) Concurrency Issues

Multiple threads sharing mutable data can cause bugs like:

- lost updates
- inconsistent reads
- unexpected ordering

These bugs are often hard to reproduce.

### 8) Race Conditions

A race condition happens when result depends on thread timing.

Example: two threads increment same counter at once and one update is lost.

```java
counter++; // not atomic
```

`counter++` is multiple steps, not one safe operation.

### 9) Strategies for Thread Safety

Common strategies:

- Avoid shared mutable state
- Use immutable objects
- Use synchronization/locks
- Use thread-safe collections/atomic classes

Pick the simplest strategy that solves the problem.

### 10) Confinement

Confinement means limiting data to one thread only.

If only one thread can access data, no synchronization is needed for that data.

Example: local variables inside a method are thread-confined.

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

### 12) The synchronized Keyword

`synchronized` is built-in Java locking.

```java
public synchronized void increment() {
    count++;
}
```

Only one thread can run this synchronized method on same object at once.

### 13) The volatile Keyword

`volatile` ensures changes to a variable are visible across threads quickly.

```java
private volatile boolean running = true;
```

Use it for visibility, not for compound atomic operations (like `count++`).

### 14) Thread Signalling with wait() and notify()

Threads can coordinate by waiting and notifying on same monitor object.

```java
synchronized (lock) {
    lock.wait();   // releases lock and waits
    lock.notify(); // wakes one waiting thread
}
```

Usually used in producer-consumer style coordination.

### 15) Atomic Objects

Atomic classes perform thread-safe operations without manual locks.

```java
java.util.concurrent.atomic.AtomicInteger counter = new java.util.concurrent.atomic.AtomicInteger();
counter.incrementAndGet();
```

Great for counters and simple shared numeric state.

### 16) Adders

`LongAdder` / `DoubleAdder` are optimized for high-contention counters.

```java
java.util.concurrent.atomic.LongAdder adder = new java.util.concurrent.atomic.LongAdder();
adder.increment();
long total = adder.sum();
```

Often faster than `AtomicLong` under heavy parallel updates.

### 17) Synchronized Collections

Java provides synchronized wrappers:

```java
java.util.List<String> list = java.util.Collections.synchronizedList(new java.util.ArrayList<>());
```

They are thread-safe but can become bottlenecks under heavy concurrency.

### 18) Concurrent Collections

`java.util.concurrent` has collections built for concurrency, like:

- `ConcurrentHashMap`
- `CopyOnWriteArrayList`
- `ConcurrentLinkedQueue`

They usually scale better than synchronized wrappers.

### 19) Summary

Key ideas:

- Threads improve responsiveness and throughput
- Shared mutable state causes most concurrency bugs
- Use synchronization, locks, atomic classes, and concurrent collections carefully
- Prefer simple, clear thread-safe design first

Concurrency is powerful, but correctness comes before speed.
