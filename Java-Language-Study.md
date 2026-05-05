# Types

## Variables

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

---

# Control Flow

## Comparison Operators

Comparison operators compare two values. The result is always a `boolean` (`true` or `false`).

Common comparison operators:

- `==` equal to
- `!=` not equal to
- `>` greater than
- `<` less than
- `>=` greater than or equal to
- `<=` less than or equal to

```java
int age = 20;
System.out.println(age >= 18); // true
System.out.println(age == 21); // false
```

## Logical Operators

Logical operators let you combine multiple true/false checks.

- `&&` AND (both conditions must be true)
- `||` OR (at least one must be true)
- `!` NOT (flips true/false)

```java
int age = 20;
boolean hasId = true;
System.out.println(age >= 18 && hasId); // true
```

## If Statements

An `if` statement runs code only when a condition is true.

```java
int temperature = 30;

if (temperature > 25) {
    System.out.println("It's a warm day.");
}
```

You can add `else` for the other case:

```java
if (temperature > 25) {
    System.out.println("It's a warm day.");
} else {
    System.out.println("It's not warm.");
}
```

## Simplifying If Statements

Sometimes people write long `if` statements to assign a boolean. You can simplify this.

Long version:

```java
int income = 120_000;
boolean hasHighIncome;

if (income > 100_000)
    hasHighIncome = true;
else
    hasHighIncome = false;
```

Simplified version:

```java
boolean hasHighIncome = income > 100_000;
```

Cleaner code is easier to read and maintain.

## The Ternary Operator

The ternary operator is a short form of `if/else` for choosing one of two values.

Syntax:

```java
condition ? valueIfTrue : valueIfFalse
```

Example:

```java
int income = 120_000;
String className = (income > 100_000) ? "First" : "Economy";
System.out.println(className);
```

Use ternary for simple choices, not for complex logic.

## Switch Statements

`switch` is useful when you compare one value against many fixed options.

```java
String role = "admin";

switch (role) {
    case "admin":
        System.out.println("You have full access.");
        break;
    case "moderator":
        System.out.println("You can manage comments.");
        break;
    default:
        System.out.println("You are a guest.");
}
```

`default` runs if no case matches.

## Exercise - FizzBuzz

FizzBuzz is a classic control-flow exercise.

Rules:

- If number is divisible by both 3 and 5, print `FizzBuzz`
- If only divisible by 3, print `Fizz`
- If only divisible by 5, print `Buzz`
- Otherwise print the number

```java
int number = 15;

if (number % 3 == 0 && number % 5 == 0)
    System.out.println("FizzBuzz");
else if (number % 3 == 0)
    System.out.println("Fizz");
else if (number % 5 == 0)
    System.out.println("Buzz");
else
    System.out.println(number);
```

## For Loops

A `for` loop repeats code a known number of times.

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

This prints numbers 1 to 5.

## While Loops

A `while` loop repeats as long as its condition is true.

```java
int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}
```

Use `while` when you do not know in advance exactly how many times to loop.

## Do..While Loops

A `do..while` loop runs the block at least once, then checks the condition.

```java
int i = 1;
do {
    System.out.println(i);
    i++;
} while (i <= 5);
```

This is useful when the first run should always happen.

## Break and Continue Statements

`break` stops the loop immediately.  
`continue` skips the current loop step and moves to the next one.

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3)
        continue; // skip 3
    if (i == 5)
        break;    // stop at 5
    System.out.println(i);
}
```

## For-Each Loop

A for-each loop is the easiest way to loop through arrays (or collections) when you only need values.

```java
int[] numbers = {10, 20, 30};

for (int number : numbers) {
    System.out.println(number);
}
```

Use for-each when you do not need the index position.

---

# Methods & Clean Code

## Clean Coding

Clean code is code that is easy to read, understand, and change later.

Beginner rule: write code for humans first, computer second.

A few clean-code habits:

- Use clear names (`monthlyPayment` instead of `mp`)
- Keep methods short and focused
- Avoid repeating the same logic
- Keep formatting consistent

```java
double monthlyPayment = 250.75;
System.out.println(monthlyPayment);
```

Small clarity improvements save a lot of time later.

## Creating Methods

A method is a named block of code that performs one task.

Instead of writing everything inside `main`, split work into methods.

```java
public static void greetUser(String name) {
    System.out.println("Hello " + name);
}
```

Call it like this:

```java
greetUser("Stefan");
```

Methods make your code reusable and easier to test.

## Refactoring

Refactoring means improving code structure without changing what the program does.

You are not adding features - you are cleaning and organizing.

Example idea:

- Before: one long method with mixed tasks
- After: multiple small methods with clear names

Refactor in small safe steps and keep running your program.

## Extracting Methods

Extracting methods means taking a chunk of code and moving it into its own method.

Before:

```java
double principal = 100_000;
double annualInterest = 5;
int years = 30;

double monthlyInterest = annualInterest / 100 / 12;
int numberOfPayments = years * 12;
```

After:

```java
double monthlyInterest = getMonthlyInterest(annualInterest);
int numberOfPayments = getNumberOfPayments(years);
```

With helper methods:

```java
public static double getMonthlyInterest(double annualInterest) {
    return annualInterest / 100 / 12;
}

public static int getNumberOfPayments(int years) {
    return years * 12;
}
```

This makes the main flow easier to read.

## Refactoring Repetitive Patterns

If you copy/paste logic, that is usually a sign to create a method.

Before (repetitive):

```java
System.out.print("Principal: ");
double principal = scanner.nextDouble();

System.out.print("Interest: ");
double interest = scanner.nextDouble();
```

After (reusable input method):

```java
public static double readNumber(Scanner scanner, String prompt) {
    System.out.print(prompt);
    return scanner.nextDouble();
}
```

Then:

```java
double principal = readNumber(scanner, "Principal: ");
double interest = readNumber(scanner, "Interest: ");
```

Less repetition means fewer bugs and easier updates.

## Project - Payment Schedule

Goal: build a small program that prints a loan payment schedule month by month.

High-level steps:

1. Read loan details (principal, annual interest, years)
2. Calculate fixed monthly payment
3. Loop through each month
4. Show remaining balance after each payment

This is a great beginner project because it uses:

- variables and types
- math expressions
- methods
- loops

## Solution

A simple structure could look like this:

```java
public static void main(String[] args) {
    double principal = 100_000;
    double annualInterest = 5;
    int years = 30;

    double payment = calculateMonthlyPayment(principal, annualInterest, years);
    printPaymentSchedule(principal, annualInterest, years, payment);
}
```

Monthly payment formula method:

```java
public static double calculateMonthlyPayment(double principal, double annualInterest, int years) {
    double monthlyInterest = annualInterest / 100 / 12;
    int numberOfPayments = years * 12;
    return principal
            * (monthlyInterest * Math.pow(1 + monthlyInterest, numberOfPayments))
            / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);
}
```

Schedule printing method:

```java
public static void printPaymentSchedule(double principal, double annualInterest, int years, double payment) {
    int months = years * 12;
    for (int month = 1; month <= months; month++) {
        double balance = calculateBalance(principal, annualInterest, years, month, payment);
        System.out.println("Month " + month + ": " + balance);
    }
}
```

## Refactoring the Code

After making the program work, clean it up:

- Move repeated math into helper methods
- Use constants for fixed numbers (`MONTHS_IN_YEAR`, `PERCENT`)
- Improve method names
- Keep `main` short and readable

Example constants:

```java
final byte MONTHS_IN_YEAR = 12;
final byte PERCENT = 100;
```

Final mindset:

1. Make it work
2. Make it clear
3. Make it clean

---

# Debugging and Deploying Applications

## Introduction

Writing code is only one part of programming. You also need to fix problems and share your app so others can run it.

That is where debugging and deploying come in:

- **Debugging** = finding and fixing problems
- **Deploying/Packaging** = preparing your app to run outside your IDE

## Types of Errors

In Java, beginners usually meet three main error types:

1. **Syntax errors** - code rules are broken (compiler catches these)
2. **Runtime errors** - program crashes while running
3. **Logical errors** - program runs, but gives wrong result

Example:

```java
int result = 10 / 0; // runtime error: ArithmeticException
```

Understanding the error type helps you fix it faster.

## Common Syntax Errors

Syntax errors happen when Java grammar is wrong.

Common examples:

- Missing semicolon `;`
- Misspelled keywords (`publc` instead of `public`)
- Missing braces `{ }`
- Wrong quotes (`'Hello'` instead of `"Hello"` for strings)

Example with errors:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello")
    }
}
```

This fails because of the missing semicolon after `println`.

Fix:

```java
System.out.println("Hello");
```

## Debugging Java Applications

Debugging means inspecting your program step by step to find where things go wrong.

Useful debugging tools:

- Breakpoints
- Step Over / Step Into
- Variable inspection
- Call stack view

Simple method to debug:

1. Reproduce the bug
2. Read the error message carefully
3. Check the line mentioned in the stack trace
4. Use breakpoints before the problem line
5. Watch variable values change step by step
6. Fix one thing at a time

You can also use quick print debugging:

```java
System.out.println("monthlyInterest = " + monthlyInterest);
System.out.println("numberOfPayments = " + numberOfPayments);
```

This helps you verify whether values are what you expect.

### Mini Debug Checklist

- Did the program crash? Read the exception type first.
- Did it run but give wrong output? Re-check your formulas and conditions.
- Are your inputs valid and in the expected range?
- Did you change one thing, then test again?

Debugging is a skill that gets better with practice.

## Packaging Java Applications

Packaging means bundling compiled code so it can run from the command line or be shared.

A common package format is a **JAR** file.

Basic flow:

1. Compile `.java` files to `.class` files
2. Package them into a `.jar`
3. Run the jar with Java

Typical commands:

```bash
javac Main.java
jar cfe app.jar Main Main.class
java -jar app.jar
```

What this does:

- `javac` compiles source code
- `jar cfe` creates an executable JAR and sets the main class
- `java -jar` runs your packaged app

For bigger projects, build tools like Maven or Gradle automate this process.
