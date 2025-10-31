# Object-Oriented Programming - Next Steps in Java 🚀

**Building on the Fundamentals**

---

## Welcome Back! 👋

Great job learning the OOP fundamentals! Now let's take the next step and explore concepts that will make you a more confident Java programmer. We'll continue with the same friendly, step-by-step approach.

**What we'll cover:**
- Interfaces
- Static vs Instance members
- The `this` and `super` keywords
- Method Overloading
- Access Modifiers in depth
- Basic Collections (ArrayList)

Let's dive in!

---

## Lesson 1: Interfaces 🔌

An **interface** is like a contract. It says "any class that implements me MUST have these methods."

### Why do we need interfaces?

Imagine you're building a media player. You want to play music, videos, and podcasts - all different, but all need a "play" button!

```java
// Interface - defines WHAT to do, not HOW
public interface Playable {
    void play();
    void pause();
    void stop();
}

// Music player implements the interface
public class MusicPlayer implements Playable {
    private String currentSong;
    
    public MusicPlayer(String song) {
        this.currentSong = song;
    }
    
    @Override
    public void play() {
        System.out.println("Playing music: " + currentSong);
    }
    
    @Override
    public void pause() {
        System.out.println("Music paused");
    }
    
    @Override
    public void stop() {
        System.out.println("Music stopped");
    }
}

// Video player implements the same interface
public class VideoPlayer implements Playable {
    private String currentVideo;
    
    public VideoPlayer(String video) {
        this.currentVideo = video;
    }
    
    @Override
    public void play() {
        System.out.println("Playing video: " + currentVideo);
    }
    
    @Override
    public void pause() {
        System.out.println("Video paused");
    }
    
    @Override
    public void stop() {
        System.out.println("Video stopped");
    }
}
```

**Using interfaces:**

```java
public class MediaDemo {
    public static void main(String[] args) {
        Playable music = new MusicPlayer("Bohemian Rhapsody");
        Playable video = new VideoPlayer("Cat Videos");
        
        // Same interface, different implementations
        music.play();
        video.play();
        
        // We can treat them the same way!
        Playable[] media = {music, video};
        for (Playable item : media) {
            item.pause();
        }
    }
}
```

### Interface vs Abstract Class - When to use what?

```java
// Abstract Class - use when classes have a "IS-A" relationship
abstract class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    // Can have implemented methods
    public void sleep() {
        System.out.println(name + " is sleeping");
    }
    
    // Can have abstract methods
    public abstract void makeSound();
}

// Interface - use for "CAN-DO" relationships
interface Swimmable {
    void swim();
}

interface Flyable {
    void fly();
}

// A duck IS an Animal, CAN swim, and CAN fly
class Duck extends Animal implements Swimmable, Flyable {
    public Duck(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println("Quack!");
    }
    
    @Override
    public void swim() {
        System.out.println(name + " is swimming");
    }
    
    @Override
    public void fly() {
        System.out.println(name + " is flying");
    }
}
```

**Key Difference:**
- **Abstract Class:** One parent only. Use for "is-a" relationships (Dog IS an Animal)
- **Interface:** Multiple interfaces. Use for "can-do" abilities (Duck CAN swim, CAN fly)

---

## Lesson 2: Static vs Instance Members 🏷️

This is a common source of confusion, so let's clear it up!

### Instance Members (Regular)

**Instance members** belong to each individual object.

```java
public class Counter {
    private int count;  // Instance variable - each Counter has its own
    
    public Counter() {
        count = 0;
    }
    
    public void increment() {  // Instance method
        count++;
    }
    
    public int getCount() {  // Instance method
        return count;
    }
}

// Usage
public class CounterDemo {
    public static void main(String[] args) {
        Counter counter1 = new Counter();
        Counter counter2 = new Counter();
        
        counter1.increment();
        counter1.increment();
        counter2.increment();
        
        System.out.println("Counter 1: " + counter1.getCount());  // 2
        System.out.println("Counter 2: " + counter2.getCount());  // 1
        // Each object has its own count!
    }
}
```

### Static Members (Class-level)

**Static members** belong to the CLASS itself, not to any particular object. There's only ONE copy shared by all objects.

```java
public class BankAccount {
    private String accountNumber;
    private double balance;
    
    // Static variable - ONE copy for ALL accounts
    private static int totalAccounts = 0;
    private static double totalBankBalance = 0;
    
    public BankAccount(String accountNumber, double initialBalance) {
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
        
        totalAccounts++;  // Shared counter
        totalBankBalance += initialBalance;
    }
    
    // Static method - can be called without creating an object
    public static int getTotalAccounts() {
        return totalAccounts;
    }
    
    public static double getTotalBankBalance() {
        return totalBankBalance;
    }
    
    // Instance method
    public double getBalance() {
        return balance;
    }
}

// Usage
public class BankDemo {
    public static void main(String[] args) {
        // Static method - called on the CLASS
        System.out.println("Accounts: " + BankAccount.getTotalAccounts());  // 0
        
        BankAccount acc1 = new BankAccount("001", 1000);
        BankAccount acc2 = new BankAccount("002", 2000);
        BankAccount acc3 = new BankAccount("003", 1500);
        
        // Static method - same value for all
        System.out.println("Total Accounts: " + BankAccount.getTotalAccounts());  // 3
        System.out.println("Total Money: $" + BankAccount.getTotalBankBalance());  // 4500
        
        // Instance method - specific to each object
        System.out.println("Account 1 balance: $" + acc1.getBalance());  // 1000
    }
}
```

### When to use Static?

✅ **Use static for:**
- Constants: `public static final double PI = 3.14159;`
- Utility methods: `Math.sqrt()`, `Math.pow()`
- Counters shared across all instances
- Factory methods

❌ **Don't use static for:**
- Object-specific data
- Methods that need to access instance variables

**Memory tip:** 
- **Instance** = "This specific dog's name"
- **Static** = "Total number of dogs created"

---

## Lesson 3: The `this` and `super` Keywords 🔑

### The `this` Keyword

`this` refers to the **current object**. It's useful when you need to be clear about what you're referring to.

```java
public class Person {
    private String name;
    private int age;
    
    // Using 'this' to distinguish between parameters and instance variables
    public Person(String name, int age) {
        this.name = name;  // this.name = instance variable
        this.age = age;    // name/age on the right = parameters
    }
    
    // Using 'this' to call another constructor
    public Person(String name) {
        this(name, 0);  // Calls the other constructor
    }
    
    // Using 'this' to return the current object
    public Person setName(String name) {
        this.name = name;
        return this;  // Enables method chaining!
    }
    
    public Person setAge(int age) {
        this.age = age;
        return this;
    }
    
    public void introduce() {
        System.out.println("I'm " + this.name + ", age " + this.age);
    }
}

// Method chaining example
public class PersonDemo {
    public static void main(String[] args) {
        Person person = new Person("Alice")
            .setAge(25)
            .setName("Alice Smith");
        
        person.introduce();  // I'm Alice Smith, age 25
    }
}
```

### The `super` Keyword

`super` refers to the **parent class**. Use it to access parent class methods and constructors.

```java
public class Vehicle {
    protected String brand;
    protected int year;
    
    public Vehicle(String brand, int year) {
        this.brand = brand;
        this.year = year;
    }
    
    public void displayInfo() {
        System.out.println("Brand: " + brand + ", Year: " + year);
    }
}

public class Car extends Vehicle {
    private int numberOfDoors;
    
    public Car(String brand, int year, int doors) {
        super(brand, year);  // Call parent constructor
        this.numberOfDoors = doors;
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();  // Call parent's method
        System.out.println("Doors: " + numberOfDoors);
    }
}

// Usage
public class VehicleDemo {
    public static void main(String[] args) {
        Car myCar = new Car("Toyota", 2024, 4);
        myCar.displayInfo();
        // Output:
        // Brand: Toyota, Year: 2024
        // Doors: 4
    }
}
```

---

## Lesson 4: Method Overloading 🎯

**Method overloading** means having multiple methods with the SAME NAME but DIFFERENT PARAMETERS.

```java
public class Calculator {
    
    // Add two integers
    public int add(int a, int b) {
        return a + b;
    }
    
    // Add three integers
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Add two doubles
    public double add(double a, double b) {
        return a + b;
    }
    
    // Add an array of integers
    public int add(int[] numbers) {
        int sum = 0;
        for (int num : numbers) {
            sum += num;
        }
        return sum;
    }
}

// Usage
public class CalculatorDemo {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        System.out.println(calc.add(5, 3));           // 8
        System.out.println(calc.add(5, 3, 2));        // 10
        System.out.println(calc.add(5.5, 3.2));       // 8.7
        System.out.println(calc.add(new int[]{1, 2, 3, 4}));  // 10
    }
}
```

### Real-world example: Constructor Overloading

```java
public class Book {
    private String title;
    private String author;
    private int pages;
    private double price;
    
    // Constructor 1: All parameters
    public Book(String title, String author, int pages, double price) {
        this.title = title;
        this.author = author;
        this.pages = pages;
        this.price = price;
    }
    
    // Constructor 2: Without price (default to 0)
    public Book(String title, String author, int pages) {
        this(title, author, pages, 0.0);  // Call the first constructor
    }
    
    // Constructor 3: Just title and author
    public Book(String title, String author) {
        this(title, author, 0, 0.0);
    }
    
    public void display() {
        System.out.println(title + " by " + author);
        if (pages > 0) System.out.println("Pages: " + pages);
        if (price > 0) System.out.println("Price: $" + price);
    }
}
```

**Rules for Overloading:**
1. Same method name
2. Different parameter list (number, type, or order)
3. Return type doesn't matter

---

## Lesson 5: Access Modifiers Explained 🔐

Java has four access levels. Let's understand them clearly:

```java
public class AccessExample {
    
    // PUBLIC - accessible from ANYWHERE
    public String publicVar = "Everyone can see me!";
    
    // PROTECTED - accessible in same package + subclasses
    protected String protectedVar = "Subclasses and package can see me";
    
    // DEFAULT (no modifier) - accessible only in same package
    String defaultVar = "Only my package can see me";
    
    // PRIVATE - accessible only within this class
    private String privateVar = "Only this class can see me";
    
    public void demonstrateAccess() {
        // All accessible here since we're inside the class
        System.out.println(publicVar);
        System.out.println(protectedVar);
        System.out.println(defaultVar);
        System.out.println(privateVar);
    }
}
```

### Visual Guide:

| Modifier | Same Class | Same Package | Subclass | Everywhere |
|----------|-----------|--------------|----------|------------|
| `public` | ✅ | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| default (none) | ✅ | ✅ | ❌ | ❌ |
| `private` | ✅ | ❌ | ❌ | ❌ |

### Best Practices:

```java
public class BestPractice {
    // ✅ GOOD: Private variables, public getters/setters
    private String name;
    private int age;
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    // ✅ GOOD: Private helper methods
    private void validateAge(int age) {
        if (age < 0 || age > 150) {
            throw new IllegalArgumentException("Invalid age");
        }
    }
    
    // ✅ GOOD: Public interface methods
    public void setAge(int age) {
        validateAge(age);
        this.age = age;
    }
}
```

**Rule of thumb:** Start with `private`, make it less restrictive only if needed!

---

## Lesson 6: ArrayList - Your First Collection 📦

An **ArrayList** is like an array, but it can grow and shrink automatically!

```java
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        // Creating an ArrayList of Strings
        ArrayList<String> fruits = new ArrayList<>();
        
        // Adding elements
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        
        System.out.println(fruits);  // [Apple, Banana, Orange]
        
        // Accessing elements
        System.out.println(fruits.get(0));  // Apple (index 0)
        
        // Size of ArrayList
        System.out.println("Size: " + fruits.size());  // 3
        
        // Removing elements
        fruits.remove("Banana");
        fruits.remove(0);  // Remove by index
        
        System.out.println(fruits);  // [Orange]
        
        // Checking if element exists
        if (fruits.contains("Orange")) {
            System.out.println("We have oranges!");
        }
        
        // Looping through ArrayList
        fruits.add("Grape");
        fruits.add("Mango");
        
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
    }
}
```

### ArrayList with Custom Objects

```java
import java.util.ArrayList;

public class Student {
    private String name;
    private int id;
    private double gpa;
    
    public Student(String name, int id, double gpa) {
        this.name = name;
        this.id = id;
        this.gpa = gpa;
    }
    
    public String getName() {
        return name;
    }
    
    public double getGpa() {
        return gpa;
    }
    
    @Override
    public String toString() {
        return name + " (ID: " + id + ", GPA: " + gpa + ")";
    }
}

public class StudentManager {
    private ArrayList<Student> students;
    
    public StudentManager() {
        students = new ArrayList<>();
    }
    
    public void addStudent(Student student) {
        students.add(student);
    }
    
    public void displayAllStudents() {
        for (Student student : students) {
            System.out.println(student);
        }
    }
    
    public Student findTopStudent() {
        if (students.isEmpty()) return null;
        
        Student topStudent = students.get(0);
        for (Student student : students) {
            if (student.getGpa() > topStudent.getGpa()) {
                topStudent = student;
            }
        }
        return topStudent;
    }
    
    public static void main(String[] args) {
        StudentManager manager = new StudentManager();
        
        manager.addStudent(new Student("Alice", 101, 3.8));
        manager.addStudent(new Student("Bob", 102, 3.5));
        manager.addStudent(new Student("Charlie", 103, 3.9));
        
        System.out.println("All Students:");
        manager.displayAllStudents();
        
        System.out.println("\nTop Student:");
        System.out.println(manager.findTopStudent());
    }
}
```

---

## Putting It All Together: E-Commerce System 🛒

Let's build a simple shopping system using everything we've learned!

```java
import java.util.ArrayList;

// Interface for things that can be sold
interface Sellable {
    double getPrice();
    String getName();
}

// Abstract product class
abstract class Product implements Sellable {
    protected String name;
    protected double price;
    protected static int totalProducts = 0;  // Static counter
    
    public Product(String name, double price) {
        this.name = name;
        this.price = price;
        totalProducts++;
    }
    
    @Override
    public String getName() {
        return name;
    }
    
    @Override
    public double getPrice() {
        return price;
    }
    
    public static int getTotalProducts() {
        return totalProducts;
    }
    
    public abstract void displayDetails();
}

// Concrete product: Book
class Book extends Product {
    private String author;
    private int pages;
    
    public Book(String name, double price, String author, int pages) {
        super(name, price);
        this.author = author;
        this.pages = pages;
    }
    
    @Override
    public void displayDetails() {
        System.out.println("Book: " + name);
        System.out.println("Author: " + author);
        System.out.println("Pages: " + pages);
        System.out.println("Price: $" + price);
    }
}

// Concrete product: Electronics
class Electronics extends Product {
    private String brand;
    private int warrantyMonths;
    
    public Electronics(String name, double price, String brand, int warranty) {
        super(name, price);
        this.brand = brand;
        this.warrantyMonths = warranty;
    }
    
    @Override
    public void displayDetails() {
        System.out.println("Electronic: " + name);
        System.out.println("Brand: " + brand);
        System.out.println("Warranty: " + warrantyMonths + " months");
        System.out.println("Price: $" + price);
    }
}

// Shopping Cart
class ShoppingCart {
    private ArrayList<Product> items;
    
    public ShoppingCart() {
        this.items = new ArrayList<>();
    }
    
    public void addItem(Product product) {
        items.add(product);
        System.out.println(product.getName() + " added to cart!");
    }
    
    public void removeItem(Product product) {
        items.remove(product);
        System.out.println(product.getName() + " removed from cart!");
    }
    
    public double calculateTotal() {
        double total = 0;
        for (Product item : items) {
            total += item.getPrice();
        }
        return total;
    }
    
    public void displayCart() {
        if (items.isEmpty()) {
            System.out.println("Your cart is empty!");
            return;
        }
        
        System.out.println("\n--- Your Shopping Cart ---");
        for (Product item : items) {
            System.out.println(item.getName() + " - $" + item.getPrice());
        }
        System.out.println("Total: $" + calculateTotal());
        System.out.println("-------------------------\n");
    }
}

// Main demo
public class ECommerceDemo {
    public static void main(String[] args) {
        // Create products
        Book book1 = new Book("Java Programming", 45.99, "John Doe", 500);
        Book book2 = new Book("Clean Code", 39.99, "Robert Martin", 464);
        Electronics laptop = new Electronics("Laptop", 899.99, "Dell", 24);
        Electronics phone = new Electronics("Smartphone", 699.99, "Samsung", 12);
        
        // Create shopping cart
        ShoppingCart cart = new ShoppingCart();
        
        // Add items
        cart.addItem(book1);
        cart.addItem(laptop);
        cart.addItem(phone);
        
        // Display cart
        cart.displayCart();
        
        // Remove an item
        cart.removeItem(phone);
        
        // Display updated cart
        cart.displayCart();
        
        // Show total products created (static method)
        System.out.println("Total products created: " + Product.getTotalProducts());
    }
}
```

---

## Quick Reference Card 📋

| Concept | Key Point | Example |
|---------|-----------|---------|
| **Interface** | Contract for what methods a class must have | `interface Playable { void play(); }` |
| **Static** | Belongs to class, not object | `static int count = 0;` |
| **Instance** | Belongs to each object | `private String name;` |
| **this** | Refers to current object | `this.name = name;` |
| **super** | Refers to parent class | `super(name, age);` |
| **Overloading** | Same name, different parameters | `add(int a, int b)` & `add(int a, int b, int c)` |
| **ArrayList** | Dynamic array | `ArrayList<String> list = new ArrayList<>();` |

---

## Practice Challenges 💪

1. **Music Library System:**
   - Create an interface `Playable` with methods `play()`, `pause()`, `stop()`
   - Create classes `Song` and `Podcast` that implement it
   - Use an ArrayList to store a playlist
   - Add methods to shuffle and display the playlist

2. **Bank System Enhancement:**
   - Create a `BankAccount` class with static variable for total bank money
   - Create `SavingsAccount` and `CheckingAccount` subclasses
   - Implement method overloading for deposit (single amount vs multiple amounts)
   - Use ArrayList to manage multiple accounts

3. **School Management:**
   - Create `Person` class with common attributes
   - Create `Student` and `Teacher` classes that extend `Person`
   - Use interfaces for `Gradable` and `Teachable`
   - Implement a `Classroom` class with ArrayList of students

---

## Key Takeaways 🎓

1. **Interfaces** define contracts - classes must implement all methods
2. **Static** members are shared across all instances
3. **this** refers to current object, **super** refers to parent
4. **Method overloading** = same name, different parameters
5. **Access modifiers** control visibility (use `private` by default!)
6. **ArrayList** is a flexible, resizable array
**Keep Coding! 🚀**

Remember: Practice is key. Try to build small projects using these concepts. The more you code, the more natural it becomes!
