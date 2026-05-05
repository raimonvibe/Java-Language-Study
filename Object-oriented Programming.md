# Object-oriented Programming

## Getting Started

### 1) Introduction

Object-oriented Programming (OOP) is a way of writing code by organizing it around **objects**.

Think of OOP like building with Lego blocks: each object is a block with its own data and behavior.

An object is like a real-world thing in your program.  
For example, in a school app, you might have objects like:

- `Student`
- `Course`
- `Teacher`

Each object can have:

- **Data** (called fields/properties), like a student's name
- **Behavior** (called methods), like `enroll()` or `printReport()`

OOP helps you model real problems in a natural way.

Simple summary:

- Object = thing with data + behavior
- Class = blueprint to create those things
- OOP = organizing code around those things

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

Quick use guide:

- Procedural style is often fine for very small scripts.
- OOP style is usually better when your project has many related entities and rules.

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

Think of classes as templates and objects as copies made from that template.

Quick use guide:

- Use classes when you need to model real entities (user, order, product, course).
- Group related data and actions in the same class for clarity.

Simple summary:

- OOP improves structure as projects grow
- Reuse comes from creating many objects from one class
- Better structure usually means easier maintenance and scaling

How this connects:

- `Getting Started` explains the OOP mindset.
- Next, `Core OOP Concepts` shows the practical tools you use every day.

---

## Core OOP Concepts

### 1) Introduction

Now we go deeper into the building blocks of OOP in Java.

Think of this section as the practical part: how to create classes, create objects, and design cleaner code.

Simple summary:

- classes define structure
- objects hold real data
- core OOP tools help you keep code safe, reusable, and easier to change

### 2) Classes and Objects

A **class** is a blueprint.  
An **object** is a real instance created from that blueprint.

Example:

- Class: `Car`
- Object: `myCar`

```java
class Car {
    String brand;
}
```

`Car` defines what a car object can have.

Quick memory line:

- Class = plan
- Object = real thing built from the plan

### 3) Creating Classes

When creating a class, start with:

- Fields (data)
- Methods (behavior)

```java
class Employee {
    String name;
    int id;

    void work() {
        System.out.println(name + " is working.");
    }
}
```

Keep classes focused on one clear responsibility.

This idea is a foundation for clean architecture later.

### 4) Creating Objects

You create objects using `new`.

```java
Employee emp1 = new Employee();
emp1.name = "Sara";
emp1.id = 101;
emp1.work();
```

Each object gets its own field values.

So changing one object's state usually does not change another object, unless both references point to the same object.

### 5) Memory Allocation

In simple terms:

- Local primitive values are stored directly
- Objects are created in heap memory
- Variables like `emp1` store references to those objects

```java
Employee emp1 = new Employee();
Employee emp2 = emp1;
```

Now `emp1` and `emp2` point to the same object in memory.

Think of references like two remote controls connected to the same TV.

### 6) Procedural Programming

Procedural programming organizes code mainly as functions/steps.

OOP organizes code around objects.

Procedural style is fine for small scripts, but for large apps it can become messy because data and logic are separated too much.

OOP improves this by keeping related data + behavior together.

Quick use guide:

- procedural style: good for tiny scripts and linear tasks
- OOP style: better for systems with many related entities and rules

### 7) Encapsulation

Encapsulation means hiding internal details and controlling access through methods.

You often do this by making fields `private`.

```java
class Account {
    private double balance;
}
```

This prevents outside code from changing `balance` in unsafe ways.

Encapsulation is basically controlled access: protect internals, expose safe operations.

### 8) Getters and Setters

Getters read private fields.  
Setters update private fields with control/validation.

```java
class Account {
    private double balance;

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        if (balance >= 0)
            this.balance = balance;
    }
}
```

This protects your object from invalid data.

Use setters when you need validation; expose only the changes that are safe for business rules.

### 9) Abstraction

Abstraction means showing only what is needed and hiding complex details.

For example, a user can call `car.start()` without knowing all internal engine steps.

Abstraction makes code easier to use and understand.

Think of abstraction like a car dashboard: you use pedals and steering wheel, not engine internals.

### 10) Coupling

Coupling is how strongly classes depend on each other.

- High coupling = classes are tightly connected (harder to change)
- Low coupling = classes are more independent (easier to maintain)

Goal: keep coupling low when possible.

Lower coupling usually means easier testing and easier replacement of components.

### 11) Reducing Coupling

Ways to reduce coupling:

- Depend on interfaces instead of concrete classes
- Pass dependencies through constructors or methods
- Keep classes focused on one job

Bad idea:

```java
class OrderService {
    private EmailService email = new EmailService(); // tightly coupled
}
```

Better idea:

```java
class OrderService {
    private NotificationService notificationService;

    public OrderService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }
}
```

Now you can swap implementations more easily.

Simple summary:

- high coupling = hard to change
- low coupling = flexible and maintainable

### 12) Constructors

A constructor is a special method used when creating objects.

- Same name as class
- No return type

```java
class User {
    String name;

    User(String name) {
        this.name = name;
    }
}
```

When you create a `User`, constructor code runs automatically.

Constructors help guarantee objects start in a valid initial state.

### 13) Method Overloading

Method overloading means using the same method name with different parameters.

```java
class Printer {
    void print(String text) {
        System.out.println(text);
    }

    void print(int number) {
        System.out.println(number);
    }
}
```

Java picks the correct version based on arguments.

Overloading improves readability by keeping similar actions under one method name.

### 14) Constructor Overloading

You can also overload constructors.

```java
class Product {
    String name;
    double price;

    Product(String name) {
        this.name = name;
    }

    Product(String name, double price) {
        this.name = name;
        this.price = price;
    }
}
```

This gives flexible ways to create objects.

Common pattern: offer a simple constructor and a full constructor for advanced cases.

### 15) Static Members

`static` members belong to the class itself, not to each object.

Use static when data/behavior is shared by all objects.

```java
class Employee {
    static int count = 0;

    Employee() {
        count++;
    }
}

System.out.println(Employee.count);
```

You can access static members with the class name, like `Employee.count`.

Simple summary:

- instance members belong to each object
- static members belong to the class itself
- use static for shared utilities or shared counters

How this connects:

- This section teaches the core building blocks (classes, objects, encapsulation, constructors).
- Next, refactoring shows how to take messy code and apply those building blocks in a real redesign.

---

## Refactoring Towards an Object-oriented Design

### 1) Introduction

In this section, the goal is not just to make code work - it is to make code clean, reusable, and object-oriented.

You will take a working program and gradually improve its design step by step.

Think of refactoring like cleaning and reorganizing a room: same room, but easier to use and maintain.

Simple summary:

- refactoring changes structure, not behavior
- goal is readability, reuse, and maintainability
- small safe steps are better than one giant rewrite

### 2) The Problem

Many beginner programs start with everything inside one big `main` method.

That works at first, but it becomes hard to:

- read the code
- test parts separately
- reuse logic
- change one thing without breaking another

This is exactly where refactoring helps.

Quick use guide:

- if method is too long, split responsibilities
- if code repeats, extract helper methods
- if names are unclear, rename for intent

### 3) What Classes Do We Need?

A good first refactoring question is:

"What responsibilities exist in this program?"

For a mortgage app, common responsibilities are:

- Reading user input
- Calculating mortgage numbers
- Printing reports

That suggests classes like:

- `Console` (input/output)
- `MortgageCalculator` (math logic)
- `MortgageReport` (display/report formatting)

This is called separation of concerns: each class handles one main responsibility.

### 4) Extracting the Console Class

Instead of reading input directly in `main`, move that logic into a `Console` class.

```java
class Console {
    public static double readNumber(String prompt) {
        System.out.print(prompt);
        return new java.util.Scanner(System.in).nextDouble();
    }
}
```

Now `main` becomes cleaner and easier to follow.

Think of `main` as an orchestrator, not a place for all detailed logic.

### 5) Overloading Methods

Overloading is useful when you want similar behavior with different inputs.

Example in `Console`:

```java
class Console {
    public static double readNumber(String prompt) { /* ... */ return 0; }
    public static double readNumber(String prompt, double min, double max) { /* ... */ return 0; }
}
```

This helps you validate input without repeating logic.

Overloading keeps one clear method name while supporting multiple usage scenarios.

### 6) Extracting the MortgageReport Class

Printing the schedule/report is a separate responsibility from calculations.

Move report code into `MortgageReport`.

```java
class MortgageReport {
    public void printMonthlyPayment(double payment) {
        System.out.println("MONTHLY PAYMENTS");
        System.out.println("----------------");
        System.out.println(payment);
    }
}
```

This keeps presentation code in one place.

A good design habit: keep "calculation logic" and "display logic" separated.

### 7) Extracting the MortgageCalculator Class

All mortgage formulas belong in a dedicated class.

```java
class MortgageCalculator {
    private final int principal;
    private final float annualInterest;
    private final byte years;

    public MortgageCalculator(int principal, float annualInterest, byte years) {
        this.principal = principal;
        this.annualInterest = annualInterest;
        this.years = years;
    }
}
```

This class becomes the single source of truth for mortgage math.

Single source of truth reduces bugs because formulas are defined in one place.

### 8) Moving Away from Static Members

At first, static methods are convenient. But too much static usage makes code rigid.

Object-oriented design prefers instance methods when logic depends on object state.

Better direction:

- create an object with constructor data
- call instance methods like `calculator.calculateMortgage()`

This improves testability and flexibility.

Instance-based design is easier to test because each object can have its own state.

### 9) Moving Static Fields

Constants that belong to a class should stay in that class.

```java
class MortgageCalculator {
    private static final byte MONTHS_IN_YEAR = 12;
    private static final byte PERCENT = 100;
}
```

This improves cohesion (related things stay together).

Cohesion means code that belongs together stays together.

### 10) Extracting Duplicate Logic

If you repeat the same formula in two methods, extract it once.

Before:

- monthly interest formula repeated
- payment count formula repeated

After:

```java
private float getMonthlyInterest() {
    return annualInterest / PERCENT / MONTHS_IN_YEAR;
}
```

This reduces mistakes and makes updates easier.

If a formula changes later, you update one method instead of many copies.

### 11) Extracting getRemainingBalances

When generating a payment schedule, you often need many balances.

Instead of mixing loops and print logic everywhere, extract a method:

```java
public double[] getRemainingBalances() {
    double[] balances = new double[years * MONTHS_IN_YEAR];
    for (short month = 1; month <= balances.length; month++)
        balances[month - 1] = calculateBalance(month);
    return balances;
}
```

Now reporting code can focus on display, not calculations.

This is a strong sign of clean design: each method/class has one clear job.

### 12) One Last Touch

After main refactoring, do a final cleanup pass:

- rename unclear variables
- improve method names
- remove dead code
- format consistently

These small touches significantly improve readability.

Final polish is where "working code" becomes "professional code."

### 13) A Quick Note

Refactoring is not a one-time action. It is a habit.

A strong workflow is:

1. Make it work
2. Refactor to improve design
3. Keep behavior the same
4. Repeat in small safe steps

That is how you move from "code that runs" to "code that is professional and maintainable."

Quick repeatable workflow:

1. make it work
2. remove duplication
3. improve naming
4. separate responsibilities
5. verify behavior is unchanged

How this connects:

- Refactoring gives you practical design habits.
- Inheritance (next) adds reuse across related classes.

---

## Inheritance

### 1) Introduction

Inheritance lets one class reuse fields and methods from another class.

It helps you avoid repetition and model "is-a" relationships, like `Dog` is an `Animal`.

Think of inheritance as a family tree: child classes inherit common traits from parent classes.

Simple summary:

- parent class = shared behavior
- child class = specialized behavior
- inheritance models "is-a" relationships

### 2) Inheritance

A child class extends a parent class using `extends`.

```java
class Animal {
    void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Barking...");
    }
}
```

`Dog` now has both `eat()` and `bark()`.

Use inheritance when child truly is a specialized type of parent, not just because code looks similar.

### 3) The Object Class

In Java, every class directly or indirectly extends `Object`.

That means every object has default methods like:

- `toString()`
- `equals()`
- `hashCode()`

So even your custom classes inherit common behavior automatically.

That is why methods like `toString()` are available on all objects.

### 4) Constructors and Inheritance

When creating a child object, parent constructor runs first.

```java
class Animal {
    Animal() {
        System.out.println("Animal constructor");
    }
}

class Dog extends Animal {
    Dog() {
        System.out.println("Dog constructor");
    }
}
```

This ensures parent state is initialized before child-specific logic.

Constructor order matters because child logic may depend on parent fields being ready first.

### 5) Access Modifiers

Access modifiers control visibility:

- `private` - only inside same class
- `protected` - same package + subclasses
- `public` - everywhere
- (no modifier) - package-private

In inheritance, `protected` is often useful when children need controlled access.

Quick use guide:

- keep fields `private` by default
- use `protected` only when subclass access is truly needed
- avoid making everything `public`

### 6) Overriding Methods

A child class can provide its own version of a parent method.

```java
class Animal {
    void speak() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    void speak() {
        System.out.println("Woof");
    }
}
```

Use `@Override` to make intention clear and catch mistakes.

Overriding is how polymorphism becomes practical in real code.

### 7) Upcasting and Downcasting

- **Upcasting**: child -> parent (safe, automatic)
- **Downcasting**: parent -> child (needs explicit cast, can fail)

```java
Animal a = new Dog(); // upcasting
Dog d = (Dog) a;      // downcasting
```

Downcast only when you are sure the object is that child type.

Safe pattern:

```java
if (a instanceof Dog) {
    Dog d = (Dog) a;
}
```

### 8) Comparing Objects

`==` compares references (same object in memory).  
`equals()` compares content/meaning (if properly overridden).

```java
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1 == s2);      // false
System.out.println(s1.equals(s2)); // true
```

For custom classes, override `equals()` (and usually `hashCode()`) for value-based comparison.

If two objects represent the same logical value, `equals()` should reflect that.

### 9) Polymorphism

Polymorphism means one parent reference can point to many child types.

```java
Animal[] animals = { new Dog(), new Cat() };
for (Animal animal : animals)
    animal.speak();
```

Each child runs its own `speak()` version.  
This is powerful for flexible and extensible design.

Polymorphism lets you write one loop/algorithm that works with many child behaviors.

### 10) Abstract Classes and Methods

An abstract class cannot be instantiated directly.  
It is a template for child classes.

```java
abstract class Shape {
    abstract double area();
}
```

Child classes must implement abstract methods.

Abstract classes are useful when you want shared base code plus required child-specific behavior.

### 11) Final Classes and Methods

- `final class` cannot be extended
- `final method` cannot be overridden

```java
final class SecurityManager {
}
```

Use `final` when behavior should stay fixed.

`final` is a protection tool: it prevents accidental or unsafe extension/overriding.

### 12) Deep Inheritance Hierarchies

Too many inheritance levels make code hard to understand and maintain.

Try to keep hierarchies shallow and clear.  
If inheritance gets complex, consider composition (using objects inside objects).

### 13) Multiple Inheritance

Java does not allow multiple inheritance of classes.

This is not allowed:

```java
// class C extends A, B { } // invalid in Java
```

But Java supports implementing multiple interfaces.

This gives multiple-behavior contracts without ambiguous multiple parent class state.

### 14) Inheritance Quiz

Quick self-check:

1. What is inherited from `Object`?
2. Difference between overriding and overloading?
3. Why is downcasting risky?
4. When should you use `final`?
5. Why can deep hierarchies become a problem?

If you can answer these clearly, your inheritance basics are strong.

### 15) Summary

Inheritance helps you:

- reuse code
- model real relationships
- support polymorphism

Use it carefully:

- prefer clear shallow hierarchies
- override thoughtfully
- combine with encapsulation and abstraction

Done well, inheritance makes object-oriented code cleaner and more maintainable.

Quick use guide:

- use inheritance for true "is-a" modeling
- keep hierarchies shallow
- prefer composition when inheritance starts feeling forced

Simple summary:

- inheritance shares code across related types
- overriding customizes behavior
- polymorphism enables flexible parent-based coding

How this connects:

- Inheritance shares behavior across related classes.
- Interfaces (next) share contracts across possibly unrelated classes.
- Together they form the backbone of flexible OOP design.

---

## Interfaces

### 1) Introduction

Interfaces are one of the most important tools in object-oriented Java design.

They help classes work together through contracts, not hard-coded implementations.

Think of an interface like a power socket standard: many devices can plug in as long as they follow the same shape.

Simple summary:

- interface defines required behavior
- classes provide concrete implementation
- this enables loose coupling and easier replacement

### 2) What are Interfaces

An interface is a contract that defines what a class must do, without saying how.

```java
interface TaxCalculator {
    double calculateTax();
}
```

Any class that implements `TaxCalculator` must provide `calculateTax()`.

So the rest of your app can depend on the contract, not on one specific calculator class.

### 3) Tightly-coupled Code

Tightly-coupled code happens when a class directly depends on a specific concrete class.

```java
class Store {
    private TaxCalculator2024 calculator = new TaxCalculator2024();
}
```

This is hard to change and hard to test.  
Interfaces help remove that tight dependency.

Tight coupling usually means:

- more code breaks when one class changes
- harder unit testing
- less flexibility in future design changes

### 4) Creating an Interface

Create an interface with `interface`, then implement it in classes.

```java
interface NotificationService {
    void send(String message);
}

class EmailService implements NotificationService {
    public void send(String message) {
        System.out.println("Email: " + message);
    }
}
```

Now your code can work with `NotificationService` instead of one specific class.

This is the core OOP design idea: depend on abstractions, not concrete details.

### 5) Dependency Injection

Dependency Injection means passing required objects from outside instead of creating them inside a class.

This reduces coupling and makes code easier to test.

Dependency injection is how interfaces become practical in real applications.

### 6) Constructor Injection

Pass dependency through constructor.

```java
class OrderService {
    private final NotificationService notificationService;

    public OrderService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }
}
```

This is the most common and preferred injection style.

Constructor injection is preferred because required dependencies are provided up front.

### 7) Setter Injection

Pass dependency through a setter method.

```java
class OrderService {
    private NotificationService notificationService;

    public void setNotificationService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }
}
```

Useful when dependency is optional or can change later.

Use setter injection carefully; too many optional dependencies can make object state unclear.

### 8) Method Injection

Pass dependency directly to the method that needs it.

```java
class OrderService {
    public void placeOrder(NotificationService notificationService) {
        notificationService.send("Order placed.");
    }
}
```

Good when dependency is used only in one operation.

Method injection keeps dependency scope very local to where it is used.

### 9) Interface Segregation Principle

This principle says: do not force classes to implement methods they do not need.

Bad design:

```java
interface Worker {
    void work();
    void eat();
}
```

Better design: split into smaller interfaces.

```java
interface Workable { void work(); }
interface Eatable { void eat(); }
```

Small focused interfaces keep code cleaner.

Simple rule: many small focused interfaces are usually better than one large "do-everything" interface.

### 10) Project - MyTube Video Platform

Imagine building a simple YouTube-like app.

Main flow:

1. Encode video
2. Store video metadata
3. Notify user

Great place to use interfaces:

- `VideoEncoder`
- `VideoDatabase`
- `NotificationService`

### 11) Solution

A service class can depend on interfaces:

```java
class VideoProcessor {
    private final VideoEncoder encoder;
    private final VideoDatabase database;
    private final NotificationService notifier;

    public VideoProcessor(VideoEncoder encoder, VideoDatabase database, NotificationService notifier) {
        this.encoder = encoder;
        this.database = database;
        this.notifier = notifier;
    }
}
```

You can swap implementations without changing `VideoProcessor`.

That is a major maintenance win as systems grow.

### 12) Fields

Interface fields are always:

- `public`
- `static`
- `final`

So they are constants.

Interfaces are not used for instance state; they are primarily behavior contracts.

```java
interface Tax {
    double MIN_TAX = 1000;
}
```

### 13) Static Methods

Interfaces can have static methods (Java 8+).

```java
interface Logger {
    static void log(String message) {
        System.out.println("[LOG] " + message);
    }
}
```

Call using interface name: `Logger.log("Started");`

Static interface methods are utility-style helpers tied to the interface concept.

### 14) Private Methods

Interfaces can also have private helper methods (Java 9+), used internally by default/static methods.

```java
interface Greeting {
    default void sayHi() {
        print("Hi");
    }

    private void print(String text) {
        System.out.println(text);
    }
}
```

This avoids repeating helper logic inside the interface.

Private interface methods help keep default/static methods DRY.

### 15) Interfaces and Abstract Classes

Use interfaces for contracts.  
Use abstract classes for shared base code/state.

Quick rule:

- Need multiple contracts? -> interfaces
- Need shared fields + partial implementation? -> abstract class

Both can work together in one design.

Think:

- interface = "what must be done"
- abstract class = "shared partial way to do it"

### 16) When to Use Interfaces

Use interfaces when:

- You want loose coupling
- You want to swap implementations easily
- You want easier unit testing (mocking dependencies)
- Multiple classes should follow the same contract

Avoid adding interfaces "just because."  
Use them when they improve flexibility and clarity.

Quick use guide:

- start with simple concrete classes
- introduce interfaces when multiple implementations or testing flexibility is needed

### 17) Common Beginner Mistakes

Watch out for these:

- Creating interfaces too early with only one tiny class and no flexibility need
- Putting too many unrelated methods in one interface
- Depending on concrete classes in service layers

Start simple, then introduce interfaces where they solve a real design problem.

Avoid turning interfaces into "extra ceremony" when no flexibility benefit exists.

### 18) Practice Check

Try this quick exercise:

1. Create an interface `PaymentGateway` with `processPayment(double amount)`
2. Implement `StripeGateway` and `PayPalGateway`
3. Inject one of them into `CheckoutService`
4. Switch implementation without changing `CheckoutService`

If this feels clear, your interface foundations are strong.

### 19) Summary

Interfaces help you design flexible and maintainable OOP systems.

Key ideas to remember:

- Program to interfaces, not implementations
- Use dependency injection to reduce coupling
- Keep interfaces small and focused
- Combine interfaces with OOP principles for cleaner design

Simple summary:

- interfaces define contracts
- dependency injection wires contracts to implementations
- small focused interfaces improve maintainability
