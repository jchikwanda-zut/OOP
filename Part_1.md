# Programming Fundamentals - Part 1: From Basics to OOP 🚀

**A Beginner's Journey into Object-Oriented Programming**

---

## Table of Contents
1. What is Programming?
2. Programming Styles
3. Introduction to Object-Oriented Programming
4. Creating Objects
5. Deep Dive: Constructors
6. Practical Task
7. What's Next?

---

## What is Programming? 💭

Programming is simply **giving instructions to a computer**. Just like you might give directions to a friend:

```
1. Walk straight for 2 blocks
2. Turn right at the coffee shop
3. The library is on your left
```

In programming, we write instructions (code) that tell the computer what to do:

```java
System.out.println("Hello, World!");  // Tell computer to display text
int age = 25;                          // Tell computer to remember a number
```

**Key Idea:** Programming is about breaking down problems into small, clear steps that a computer can follow.

---

## Programming Styles 🎨

There are different ways to organize your code. Think of them as different styles of writing a recipe!

### Style 1: Procedural Programming (The Step-by-Step Recipe)

Procedural programming is like following a recipe from top to bottom. You write a series of steps, one after another.

**Example: Making a Phone Call (Procedural Style)**

```java
public class PhoneCall {
    public static void main(String[] args) {
        // Step 1: Pick up phone
        System.out.println("Picking up phone...");
        String phoneNumber = "0977123456";
        
        // Step 2: Dial number
        System.out.println("Dialing " + phoneNumber + "...");
        
        // Step 3: Wait for connection
        System.out.println("Connecting...");
        boolean connected = true;
        
        // Step 4: Talk
        if (connected) {
            System.out.println("Call connected! You can talk now.");
        }
        
        // Step 5: End call
        System.out.println("Call ended.");
    }
}
```

**What's happening?**
- Code runs from **top to bottom**
- Each step follows the previous one
- Variables store data (`phoneNumber`, `connected`)
- It's straightforward and easy to follow!

**Good for:** Simple scripts, small programs, quick tasks

**Challenge:** As programs grow larger (thousands of lines!), this style becomes messy and hard to maintain.

---

### Style 2: Object-Oriented Programming (The Component Approach)

Object-Oriented Programming (OOP) is like having different tools, each with its own special purpose and features.

**Example: Making a Phone Call (Object-Oriented Style)**

```java
// We create a "blueprint" for a mobile phone
public class MobilePhone {
    // Properties (what it HAS)
    private String phoneNumber;
    private int batteryLevel;
    private boolean isConnected;
    
    // Constructor (how to set it up)
    public MobilePhone(String phoneNumber) {
        this.phoneNumber = phoneNumber;
        this.batteryLevel = 100;
        this.isConnected = false;
    }
    
    // Methods (what it can DO)
    public void makeCall(String number) {
        System.out.println("Calling " + number + "...");
        isConnected = true;
        batteryLevel -= 5;
    }
    
    public void endCall() {
        System.out.println("Call ended.");
        isConnected = false;
    }
    
    public void sendSMS(String number, String message) {
        System.out.println("Sending SMS to " + number + ": " + message);
        batteryLevel -= 1;
    }
    
    public void checkBattery() {
        System.out.println("Battery level: " + batteryLevel + "%");
    }
}

// Using the phone
public class PhoneUser {
    public static void main(String[] args) {
        // Create a phone object
        MobilePhone myPhone = new MobilePhone("0977123456");
        
        // Use its methods
        myPhone.makeCall("0966789012");
        myPhone.endCall();
        myPhone.sendSMS("0955555555", "Hello!");
        myPhone.checkBattery();
    }
}
```

**What's different?**
- Code is organized into **objects** (MobilePhone)
- Each object has **properties** (phoneNumber, batteryLevel, isConnected)
- Each object has **behaviors** (makeCall, endCall, sendSMS, checkBattery)
- You can create **multiple** phones easily!

**Good for:** Large programs, team projects, reusable code

---

### Quick Comparison 📊

| Aspect | Procedural | Object-Oriented |
|--------|-----------|-----------------|
| **Organization** | Sequential steps | Objects with properties & methods |
| **Data** | Variables scattered everywhere | Data grouped inside objects |
| **Reusability** | Copy-paste code | Create multiple objects from one blueprint |
| **Complexity** | Simple for small programs | Better for large programs |
| **Real-world modeling** | Less intuitive | Models real things naturally |

**Think of it this way:**
- **Procedural**: Like writing a long to-do list
- **Object-Oriented**: Like having different tools, each with its own purpose

---

## Introduction to Object-Oriented Programming 🎯

### The Big Idea

OOP is all about modeling real-world things in your code. Everything around you is an object with:
- **Properties** (what it HAS): color, size, name
- **Behaviors** (what it DOES): move, make sound, calculate

### Real World → Code

Let's think about a **Car**:

**Real Car:**
- Has: color, brand, speed, fuel level
- Does: start, stop, accelerate, honk

**Code Car:**
```java
public class Car {
    // Properties (what it HAS)
    String color;
    String brand;
    int speed;
    int fuelLevel;
    
    // Behaviors (what it DOES)
    public void start() {
        System.out.println("Engine started! Vroom!");
    }
    
    public void accelerate() {
        speed += 10;
        System.out.println("Speed is now: " + speed + " km/h");
    }
    
    public void honk() {
        System.out.println("Beep beep!");
    }
}
```

---

## Creating Objects 🏗️

### Understanding Classes vs Objects

**Class** = Blueprint/Recipe/Template
**Object** = The actual thing you make from the blueprint

**Analogy:**
- **Class**: Cookie cutter shape
- **Object**: The actual cookie you cut out

### Step-by-Step: Creating Your First Object

**Step 1: Define the Class (Blueprint)**

```java
public class Student {
    // Properties
    String name;
    int age;
    String major;
    
    // Methods
    public void study() {
        System.out.println(name + " is studying " + major);
    }
    
    public void introduce() {
        System.out.println("Hi! I'm " + name + ", " + age + " years old, studying " + major);
    }
}
```

**What we created:**
- A blueprint called `Student`
- Properties: `name`, `age`, `major`
- Methods: `study()`, `introduce()`

**Step 2: Create Objects (Actual Students)**

```java
public class University {
    public static void main(String[] args) {
        // Create first student object
        Student student1 = new Student();
        student1.name = "Alice";
        student1.age = 20;
        student1.major = "Computer Science";
        
        // Create second student object
        Student student2 = new Student();
        student2.name = "Bob";
        student2.age = 22;
        student2.major = "Mathematics";
        
        // Use the objects
        student1.introduce();  // Hi! I'm Alice, 20 years old...
        student2.introduce();  // Hi! I'm Bob, 22 years old...
        
        student1.study();      // Alice is studying Computer Science
        student2.study();      // Bob is studying Mathematics
    }
}
```

**Breaking it down:**

1. `Student student1 = new Student();`
   - `Student` = type (like saying "this is a car")
   - `student1` = name of our object (like naming your car "Betsy")
   - `new Student()` = actually create the object in memory

2. `student1.name = "Alice";`
   - Use the **dot (.)** to access properties
   - Set values for this specific student

3. `student1.introduce();`
   - Use the **dot (.)** to call methods
   - Run the behavior for this specific student

---

### Multiple Objects, Same Blueprint

The beauty of OOP: **one class, unlimited objects!**

```java
public class Main {
    public static void main(String[] args) {
        // Create a classroom of students
        Student s1 = new Student();
        s1.name = "Alice";
        
        Student s2 = new Student();
        s2.name = "Bob";
        
        Student s3 = new Student();
        s3.name = "Charlie";
        
        // Each object is independent!
        // Changing s1 doesn't affect s2 or s3
    }
}
```

**Key Insight:** Each object has its own copy of the properties. They don't interfere with each other!

---

## Deep Dive: Constructors 🔨

### The Problem

Look at our current way of creating objects:

```java
Student student1 = new Student();
student1.name = "Alice";      // Line 1
student1.age = 20;             // Line 2
student1.major = "CS";         // Line 3
```

**Issues:**
1. Takes multiple lines
2. Easy to forget to set a property
3. Objects can exist in an incomplete state

**What if we could set everything up immediately when creating the object?** 🤔

---

### Enter: Constructors!

A **constructor** is a special method that runs automatically when you create an object. It sets up the initial state of the object.

**Think of it like:**
- Building a car at a factory: you don't get a car without an engine!
- Ordering at a restaurant: "I'll have a burger with cheese, lettuce, and tomato" (all at once!)

---

### Basic Constructor Syntax

```java
public class Student {
    // Properties
    String name;
    int age;
    String major;
    
    // Constructor - same name as the class, no return type!
    public Student(String studentName, int studentAge, String studentMajor) {
        name = studentName;
        age = studentAge;
        major = studentMajor;
    }
    
    public void introduce() {
        System.out.println("Hi! I'm " + name + ", " + age + " years old, studying " + major);
    }
}
```

**Key Points About Constructors:**
1. **Same name as the class**: `Student` class → `Student()` constructor
2. **No return type**: Not even `void`!
3. **Runs automatically**: When you use `new`
4. **Purpose**: Initialize (set up) the object

---

### Using a Constructor

**Before (without constructor):**
```java
Student student1 = new Student();
student1.name = "Alice";
student1.age = 20;
student1.major = "Computer Science";
```

**After (with constructor):**
```java
Student student1 = new Student("Alice", 20, "Computer Science");
```

**Much cleaner!** ✨ Everything is set up in one line.

---

### The `this` Keyword

Often you'll see `this` in constructors. What does it mean?

```java
public class Student {
    String name;
    int age;
    
    // Parameter names same as property names - confusing!
    public Student(String name, int age) {
        this.name = name;  // this.name = property, name = parameter
        this.age = age;    // this.age = property, age = parameter
    }
}
```

**`this` means "this object's"**
- `this.name` = "this object's name property"
- `name` = "the parameter passed in"

**Why use `this`?**
It makes your code clearer and lets you use the same names for parameters and properties!

---

### Multiple Constructors (Constructor Overloading)

You can have **multiple constructors** with different parameters. Java chooses the right one based on what you pass in!

```java
public class Student {
    String name;
    int age;
    String major;
    
    // Constructor 1: All information
    public Student(String name, int age, String major) {
        this.name = name;
        this.age = age;
        this.major = major;
    }
    
    // Constructor 2: Just name and age (major undecided)
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
        this.major = "Undecided";  // Default value
    }
    
    // Constructor 3: Just name (very new student)
    public Student(String name) {
        this.name = name;
        this.age = 18;            // Default value
        this.major = "Undecided"; // Default value
    }
    
    public void introduce() {
        System.out.println("Hi! I'm " + name + ", " + age + " years old, studying " + major);
    }
}
```

**Using different constructors:**

```java
public class Main {
    public static void main(String[] args) {
        // Use constructor 1 (all info)
        Student s1 = new Student("Alice", 20, "Computer Science");
        
        // Use constructor 2 (name and age only)
        Student s2 = new Student("Bob", 22);
        
        // Use constructor 3 (name only)
        Student s3 = new Student("Charlie");
        
        s1.introduce();  // Hi! I'm Alice, 20 years old, studying Computer Science
        s2.introduce();  // Hi! I'm Bob, 22 years old, studying Undecided
        s3.introduce();  // Hi! I'm Charlie, 18 years old, studying Undecided
    }
}
```

**Why is this useful?**
- Flexibility! Sometimes you have all info, sometimes you don't
- Default values for missing information
- Different ways to create objects based on what data you have

---

### Default Constructor

If you **don't write any constructor**, Java gives you a free one (the **default constructor**):

```java
public class Book {
    String title;
    String author;
    // No constructor written!
}

// Java automatically provides:
// public Book() { }

// So this works:
Book myBook = new Book();
```

**BUT!** If you write **any** constructor, the default one disappears:

```java
public class Book {
    String title;
    String author;
    
    // We wrote a constructor
    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }
}

// This now gives an ERROR:
Book myBook = new Book();  // ❌ No constructor without parameters!

// This works:
Book myBook = new Book("1984", "George Orwell");  // ✅
```

---

### Constructor Best Practices 🌟

1. **Initialize all properties**: Make sure your object is fully set up
   ```java
   public Student(String name, int age, String major) {
       this.name = name;
       this.age = age;
       this.major = major;  // Don't forget any!
   }
   ```

2. **Validate input**: Check if values make sense
   ```java
   public Student(String name, int age, String major) {
       this.name = name;
       
       // Age should be positive and reasonable
       if (age > 0 && age < 120) {
           this.age = age;
       } else {
           this.age = 18;  // Default if invalid
           System.out.println("Invalid age! Setting to 18");
       }
       
       this.major = major;
   }
   ```

3. **Use `this` for clarity**: Even if not required, it makes code clearer
   ```java
   public Student(String name, int age) {
       this.name = name;  // Clear: property vs parameter
       this.age = age;
   }
   ```

4. **Provide multiple constructors**: For flexibility
   ```java
   // Full info constructor
   public Student(String name, int age, String major) { ... }
   
   // Partial info constructor
   public Student(String name) { ... }
   ```

---

### Complete Constructor Example

Let's create a realistic example that uses everything we've learned:

```java
public class BankAccount {
    // Properties
    private String accountNumber;
    private String ownerName;
    private double balance;
    private String accountType;
    
    // Constructor 1: Full details
    public BankAccount(String accountNumber, String ownerName, double initialBalance, String accountType) {
        this.accountNumber = accountNumber;
        this.ownerName = ownerName;
        
        // Validate balance
        if (initialBalance >= 0) {
            this.balance = initialBalance;
        } else {
            this.balance = 0;
            System.out.println("Invalid balance! Starting with $0");
        }
        
        this.accountType = accountType;
        
        System.out.println("Account created for " + ownerName);
    }
    
    // Constructor 2: New account with zero balance
    public BankAccount(String accountNumber, String ownerName, String accountType) {
        this.accountNumber = accountNumber;
        this.ownerName = ownerName;
        this.balance = 0;  // Start with zero
        this.accountType = accountType;
        
        System.out.println("New account created for " + ownerName + " with $0 balance");
    }
    
    // Constructor 3: Simple savings account
    public BankAccount(String ownerName) {
        this.accountNumber = "AUTO-" + System.currentTimeMillis();  // Generate ID
        this.ownerName = ownerName;
        this.balance = 0;
        this.accountType = "Savings";  // Default type
        
        System.out.println("Simple savings account created for " + ownerName);
    }
    
    // Methods
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited $" + amount + ". New balance: $" + balance);
        }
    }
    
    public void displayInfo() {
        System.out.println("=== Account Info ===");
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Owner: " + ownerName);
        System.out.println("Type: " + accountType);
        System.out.println("Balance: $" + balance);
    }
}
```

**Using the BankAccount class:**

```java
public class BankApp {
    public static void main(String[] args) {
        // Using constructor 1 (full details)
        BankAccount account1 = new BankAccount("ACC001", "Alice Johnson", 5000, "Checking");
        account1.displayInfo();
        
        System.out.println();
        
        // Using constructor 2 (zero balance)
        BankAccount account2 = new BankAccount("ACC002", "Bob Smith", "Savings");
        account2.deposit(1000);
        account2.displayInfo();
        
        System.out.println();
        
        // Using constructor 3 (simple account)
        BankAccount account3 = new BankAccount("Charlie Brown");
        account3.deposit(500);
        account3.displayInfo();
    }
}
```

**Output:**
```
Account created for Alice Johnson
=== Account Info ===
Account Number: ACC001
Owner: Alice Johnson
Type: Checking
Balance: $5000.0

New account created for Bob Smith with $0 balance
Deposited $1000.0. New balance: $1000.0
=== Account Info ===
Account Number: ACC002
Owner: Bob Smith
Type: Savings
Balance: $1000.0

Simple savings account created for Charlie Brown
Deposited $500.0. New balance: $500.0
=== Account Info ===
Account Number: AUTO-1234567890123
Owner: Charlie Brown
Type: Savings
Balance: $500.0
```

---

## Practical Task 🎯

Now it's your turn! Create a simple **Library Management System**.

### Task Requirements

Create a `Book` class with the following:

**Properties:**
- `title` (String)
- `author` (String)
- `isbn` (String)
- `numberOfPages` (int)
- `isAvailable` (boolean) - whether the book can be borrowed

**Constructors:**
1. A constructor that takes all properties
2. A constructor that takes only title and author (set default values for the rest)

**Methods:**
1. `displayInfo()` - prints all book information
2. `borrowBook()` - marks the book as unavailable if it's currently available
3. `returnBook()` - marks the book as available

### Step-by-Step Guide

**Step 1: Create the Book class**
```java
public class Book {
    // TODO: Add properties here
    
    // TODO: Add constructors here
    
    // TODO: Add methods here
}
```

**Step 2: Test your class**
```java
public class LibraryTest {
    public static void main(String[] args) {
        // Create a book using the full constructor
        Book book1 = new Book("1984", "George Orwell", "978-0451524935", 328, true);
        
        // Create a book using the simple constructor
        Book book2 = new Book("To Kill a Mockingbird", "Harper Lee");
        
        // Display book information
        book1.displayInfo();
        
        // Try borrowing the book
        book1.borrowBook();
        book1.borrowBook();  // Try again - should say it's already borrowed
        
        // Return the book
        book1.returnBook();
    }
}
```

### Expected Output
```
=== Book Information ===
Title: 1984
Author: George Orwell
ISBN: 978-0451524935
Pages: 328
Status: Available

1984 has been borrowed successfully!
Sorry, 1984 is already borrowed.
1984 has been returned successfully!
```

### Solution Template

<details>
<summary>Click here if you need help getting started</summary>

```java
public class Book {
    // Properties
    private String title;
    private String author;
    private String isbn;
    private int numberOfPages;
    private boolean isAvailable;
    
    // Constructor 1: Full details
    public Book(String title, String author, String isbn, int numberOfPages, boolean isAvailable) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.numberOfPages = numberOfPages;
        this.isAvailable = isAvailable;
    }
    
    // Constructor 2: Simple (only title and author)
    public Book(String title, String author) {
        this.title = title;
        this.author = author;
        this.isbn = "Unknown";
        this.numberOfPages = 0;
        this.isAvailable = true;  // New books are available
    }
    
    // Method: Display information
    public void displayInfo() {
        System.out.println("=== Book Information ===");
        System.out.println("Title: " + title);
        System.out.println("Author: " + author);
        System.out.println("ISBN: " + isbn);
        System.out.println("Pages: " + numberOfPages);
        System.out.println("Status: " + (isAvailable ? "Available" : "Borrowed"));
        System.out.println();
    }
    
    // Method: Borrow book
    public void borrowBook() {
        if (isAvailable) {
            isAvailable = false;
            System.out.println(title + " has been borrowed successfully!");
        } else {
            System.out.println("Sorry, " + title + " is already borrowed.");
        }
    }
    
    // Method: Return book
    public void returnBook() {
        if (!isAvailable) {
            isAvailable = true;
            System.out.println(title + " has been returned successfully!");
        } else {
            System.out.println(title + " was not borrowed.");
        }
    }
}
```

</details>

### Extension Challenges 🌟

Once you've completed the basic task, try these:

1. **Add a `publishedYear` property** and modify constructors
2. **Create a `Library` class** that can store multiple books
3. **Add validation** in constructors (e.g., pages can't be negative)
4. **Create a method** to check how many days a book has been borrowed

---

## What's Next? 📚

Congratulations! You've learned the fundamentals of OOP and mastered constructors. This is just the beginning!

### Topics for Part 2
- **Encapsulation**: Using getters and setters properly
- **Inheritance**: Creating class hierarchies
- **Polymorphism**: Same method, different behaviors
- **Access Modifiers**: public, private, protected

### Recommended Resources

**Official Documentation:**
- [Oracle Java Tutorials - Classes and Objects](https://docs.oracle.com/javase/tutorial/java/javaOO/index.html)
- [Oracle Java Tutorials - Constructors](https://docs.oracle.com/javase/tutorial/java/javaOO/constructors.html)

**Interactive Learning:**
- [Codecademy - Learn Java](https://www.codecademy.com/learn/learn-java)
- [JetBrains Academy - Java Developer Track](https://www.jetbrains.com/academy/)

**Video Tutorials:**
- [Programming with Mosh - Java Tutorial for Beginners](https://www.youtube.com/watch?v=eIrMbAQSU34)
- [freeCodeCamp - Java Programming](https://www.youtube.com/watch?v=grEKMHGYyns)

**Practice Platforms:**
- [HackerRank - Java Domain](https://www.hackerrank.com/domains/java)
- [LeetCode - Java Problems](https://leetcode.com/problemset/all/)
- [CodingBat - Java Practice](https://codingbat.com/java)

**Books:**
- "Head First Java" by Kathy Sierra (Great for beginners!)
- "Effective Java" by Joshua Bloch (For when you're ready to level up)

---

## Quick Reference Card 🎴

| Concept | What It Is | Example |
|---------|-----------|---------|
| **Class** | Blueprint for objects | `public class Student { }` |
| **Object** | Instance of a class | `Student s = new Student();` |
| **Properties** | Data the object stores | `String name; int age;` |
| **Methods** | Actions the object can do | `public void study() { }` |
| **Constructor** | Special method to initialize objects | `public Student(String name) { }` |
| **this** | Refers to current object | `this.name = name;` |
| **Overloading** | Multiple methods/constructors with same name | Multiple constructors |

---

## Key Takeaways 🔑

1. **Procedural vs OOP**: Procedural is step-by-step, OOP organizes code into objects
2. **Classes are blueprints**, objects are the actual instances
3. **Constructors** initialize objects and run automatically with `new`
4. **`this`** refers to the current object's properties/methods
5. **Constructor overloading** provides flexibility in object creation
6. **Always validate input** in constructors to ensure objects start in valid states

---

## Final Thoughts 💡

Object-Oriented Programming might seem complex at first, but remember:
- **Start small**: Create simple classes with a few properties  
- **Practice regularly**: The more objects you create, the more natural it becomes  
- **Think real-world**: Model things you see around you  
- **Be patient**: OOP is a skill that develops over time  

You now have the foundation to build amazing applications. Keep coding, keep learning, and most importantly, **have fun with it**! 🚀  

---

**Ready for Part 2?** Stay tuned for our next lesson on Encapsulation and Access Modifiers!  

**Questions or feedback?** Practice makes perfect — try building small projects using what you've learned today!  
If you have any questions, feel free to reach out at [jchikwanda@zut.edu.zm](mailto:jchikwanda@zut.edu.zm). 📧  

---

*Happy Coding! 💻✨*
