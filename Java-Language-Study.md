# Variables

Variables are like labeled boxes in your program where you can store data. Think of them as little sticky notes with a name on them - you write a value on the note, and later you can look at that name to get the value back.

In Java, before you can use a variable, you have to tell Java two things: what kind of data it will hold and what name you're giving it. That's called declaring the variable.

For example, if you want to store someone's age, you could say:

```java
int age = 25;
```

Here, `int` means integer, `age` is the name of your box, and `25` is the value you're putting inside it.

The name you choose should describe what the data is for - that makes your code much easier to read later. So instead of calling it `x`, calling it `age` or `price` is way better.

# Primitive Types

Primitive types are Java's most basic data types. They store simple values directly, like numbers or true/false.

Think of primitive types as the "built-in tiny containers" Java gives you for common data.

Some important primitive types:

- `byte` - very small whole numbers
- `short` - small whole numbers
- `int` - normal whole numbers
- `long` - very large whole numbers
- `float` - decimal numbers (less precise)
- `double` - decimal numbers (more precise, most common for decimals)
- `char` - a single character
- `boolean` - `true` or `false`

Example:

```java
int age = 25;
double price = 19.99;
boolean isStudent = true;
char grade = 'A';
```

Use primitive types when you only need a simple value and no extra behavior.

# Reference Types

Reference types are different from primitive types. Instead of storing the real data directly, they store a reference (an address) to where the data lives in memory.

You can think of a reference type variable like a note that says, "the real object is over there."

Common reference types include:

- `String`
- Arrays (like `int[]`)
- Classes you create (like `Person`, `Car`, etc.)

Example:

```java
String name = "Stefan";
int[] scores = {90, 85, 100};
```

Both `name` and `scores` hold references to objects, not the raw object data itself.

# Primitive vs Reference Types

The biggest difference is how values are stored and copied.

- Primitive variable: stores the actual value.
- Reference variable: stores the address to an object.

Example with primitives:

```java
int a = 10;
int b = a;
b = 20;
System.out.println(a); // 10
```

`a` stays `10` because `b` got its own copy of the value.

Example with references:

```java
int[] numbers1 = {1, 2, 3};
int[] numbers2 = numbers1;
numbers2[0] = 99;
System.out.println(numbers1[0]); // 99
```

`numbers1` also changes because both variables point to the same array object.

# Strings

A `String` is text in Java. Anything inside double quotes is a string.

Examples:

```java
String firstName = "Stefan";
String message = "Hello, Java!";
```

Strings are reference types, but Java makes them very easy to use.

Useful string operations:

```java
String name = "stefan";
System.out.println(name.length());      // 6
System.out.println(name.toUpperCase()); // STEFAN
System.out.println(name.startsWith("st")); // true
```

Strings are immutable, which means when you "change" a string, Java actually creates a new one.

# Escape Sequences

Escape sequences let you put special characters inside strings.

They start with a backslash `\`.

Common ones:

- `\"` - double quote
- `\\` - backslash
- `\n` - new line
- `\t` - tab

Example:

```java
String text = "He said, \"Java is fun!\"\nNew line here.";
System.out.println(text);
```

Without escape sequences, some characters would break your string syntax.

# Arrays

An array stores multiple values of the same type in one variable.

Instead of making many variables like `score1`, `score2`, `score3`, you can use one array.

Example:

```java
int[] scores = {90, 85, 100};
System.out.println(scores[0]); // 90
```

Array positions are called indexes, and indexing starts at `0`, not `1`.

You can also create an empty array with a fixed size:

```java
int[] numbers = new int[5]; // 5 slots, default value 0
```

# Multi-dimensional Arrays

A multi-dimensional array is an array of arrays.

The most common is a 2D array, like a table with rows and columns.

Example:

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

System.out.println(matrix[1][2]); // 6
```

`matrix[1][2]` means: row `1`, column `2`.

# Constants

A constant is a value that should not change after it is set.

In Java, use the `final` keyword for constants.

Example:

```java
final double PI = 3.14159;
final int DAYS_IN_WEEK = 7;
```

By convention, constants are usually written in uppercase with underscores.

Constants make your code safer and easier to understand.

# Arithmetic Expressions

Arithmetic expressions are math operations in code.

Java supports:

- `+` addition
- `-` subtraction
- `*` multiplication
- `/` division
- `%` remainder (what is left after division)

Example:

```java
int a = 10;
int b = 3;

System.out.println(a + b); // 13
System.out.println(a / b); // 3
System.out.println(a % b); // 1
```

Notice `10 / 3` gives `3` because both values are integers.

# Order of Operations

Java follows math priority rules when evaluating expressions:

1. Parentheses `()`
2. Multiplication/division `* / %`
3. Addition/subtraction `+ -`

Example:

```java
int result1 = 10 + 2 * 3;      // 16
int result2 = (10 + 2) * 3;    // 36
```

Use parentheses when you want to make your intention clear.

# Casting

Casting means converting a value from one type to another.

There are two common types:

- Implicit casting (automatic, safe)
- Explicit casting (manual)

Example:

```java
int x = 10;
double y = x; // implicit casting: int -> double
```

Explicit casting:

```java
double price = 19.99;
int whole = (int) price; // 19
```

When casting from a larger or more precise type to a smaller one, you can lose data.

# The Math Class

Java has a built-in `Math` class with helpful math methods.

Examples:

```java
System.out.println(Math.round(1.6));  // 2
System.out.println(Math.ceil(1.2));   // 2.0
System.out.println(Math.floor(1.8));  // 1.0
System.out.println(Math.max(10, 20)); // 20
System.out.println(Math.random());    // random number 0.0 to <1.0
```

To get a random integer range, you often combine `Math.random()` with casting.

# Formatting Numbers

Sometimes you want numbers to look nice for users, like money or percentages.

Java provides formatter classes such as `NumberFormat`.

Example:

```java
import java.text.NumberFormat;

double amount = 1234.5;
String money = NumberFormat.getCurrencyInstance().format(amount);
System.out.println(money); // e.g. €1,234.50 (depends on locale)
```

You can also format as a percent:

```java
double ratio = 0.82;
String percent = NumberFormat.getPercentInstance().format(ratio);
System.out.println(percent); // 82%
```

Formatting makes output cleaner and more professional.

# Reading Input

To read input from the user in the console, Java commonly uses the `Scanner` class.

Example:

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
System.out.print("What is your name? ");
String name = scanner.nextLine();

System.out.print("How old are you? ");
int age = scanner.nextInt();

System.out.println("Hello " + name + ", age " + age);
```

This lets your program interact with users instead of always using fixed values in code.

Tip: if you are done with input, you can close the scanner with `scanner.close();`.
