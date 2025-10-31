# Object-Oriented Programming Fundamentals in Java 🚀

**A Friendly Guide to OOP Basics**

---

## Welcome! 👋

This lesson will teach you the fundamentals of Object-Oriented Programming (OOP) using Java. We'll take it step by step, starting from the very basics. By the end, you'll understand the core concepts that every programmer should know!

---

## What is Object-Oriented Programming?

Imagine you're describing things in the real world. A **car** has properties (color, brand, speed) and can do things (start, stop, accelerate). OOP lets us model real-world things in our code the same way!

**Key idea:** Instead of writing all our code in one big pile, we organize it into "objects" that represent things.

---

## Baby Step 1: What is a Class?

A **class** is like a blueprint or template. Think of it as a cookie cutter - it defines the shape, but it's not the actual cookie!

### Simple Example: A Dog Class

```java
public class Dog {
    // Properties (what a dog HAS)
    String name;
    int age;
    String breed;
    
    // Behaviors (what a dog DOES)
    public void bark() {
        System.out.println(name + " says: Woof! Woof!");
    }
    
    public void sleep() {
        System.out.println(name + " is sleeping... Zzz");
    }
}
```

**What's happening here?**
- `String name`, `int age`, `String breed` are **attributes** (properties)
- `bark()` and `sleep()` are **methods** (actions/behaviors)

---

## Baby Step 2: Creating Objects

A **class** is the blueprint. An **object** is the actual thing you create from that blueprint!

```java
public class DogDemo {
    public static void main(String[] args) {
        // Creating objects (actual dogs!)
        Dog myDog = new Dog();
        myDog.name = "Buddy";
        myDog.age = 3;
        myDog.breed = "Golden Retriever";
        
        Dog yourDog = new Dog();
        yourDog.name = "Max";
        yourDog.age = 5;
        yourDog.breed = "Beagle";
        
        // Using the objects
        myDog.bark();    // Output: Buddy says: Woof! Woof!
        yourDog.bark();  // Output: Max says: Woof! Woof!
    }
}
```

**Key point:** One class, multiple objects! Each object has its own values.

---

## Baby Step 3: Constructors

Wouldn't it be nice to set up our dog when we create it? That's what **constructors** do!

```java
public class Dog {
    String name;
    int age;
    String breed;
    
    // Constructor - runs when you create a new Dog
    public Dog(String dogName, int dogAge, String dogBreed) {
        name = dogName;
        age = dogAge;
        breed = dogBreed;
    }
    
    public void bark() {
        System.out.println(name + " says: Woof! Woof!");
    }
    
    public void introduce() {
        System.out.println("Hi! I'm " + name + ", a " + age + 
                         " year old " + breed);
    }
}
```

**Using the constructor:**

```java
public class DogDemo {
    public static void main(String[] args) {
        // Much cleaner way to create dogs!
        Dog myDog = new Dog("Buddy", 3, "Golden Retriever");
        Dog yourDog = new Dog("Max", 5, "Beagle");
        
        myDog.introduce();  // Hi! I'm Buddy, a 3 year old Golden Retriever
        yourDog.introduce(); // Hi! I'm Max, a 5 year old Beagle
    }
}
```

---

## Baby Step 4: The Four Pillars of OOP

### 1. **Encapsulation** 🔒
*"Keeping data safe and controlled"*

Right now, anyone can change our dog's age directly:
```java
myDog.age = -5;  // Uh oh, that doesn't make sense!
```

Let's fix this by making attributes **private** and using **getters/setters**:

```java
public class Dog {
    private String name;  // Now private!
    private int age;
    private String breed;
    
    public Dog(String name, int age, String breed) {
        this.name = name;
        this.setAge(age);  // Use setter for validation
        this.breed = breed;
    }
    
    // Getter - allows reading the value
    public int getAge() {
        return age;
    }
    
    // Setter - allows changing the value (with validation!)
    public void setAge(int age) {
        if (age > 0 && age < 30) {  // Dogs don't live to 100!
            this.age = age;
        } else {
            System.out.println("Invalid age!");
        }
    }
    
    public String getName() {
        return name;
    }
}
```

**Why is this good?**
- We control how data is accessed and changed
- We can validate input (no negative ages!)
- We can change internal implementation without breaking other code

---

### 2. **Inheritance** 👨‍👦
*"One class can inherit from another"*

Imagine we want different types of animals. Instead of repeating code, we can use inheritance!

```java
// Parent class (superclass)
public class Animal {
    protected String name;
    protected int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void eat() {
        System.out.println(name + " is eating");
    }
    
    public void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Child class (subclass)
public class Dog extends Animal {
    private String breed;
    
    public Dog(String name, int age, String breed) {
        super(name, age);  // Call parent constructor
        this.breed = breed;
    }
    
    public void bark() {  // Dog-specific method
        System.out.println(name + " says: Woof!");
    }
}

// Another child class
public class Cat extends Animal {
    private boolean isIndoor;
    
    public Cat(String name, int age, boolean isIndoor) {
        super(name, age);
        this.isIndoor = isIndoor;
    }
    
    public void meow() {  // Cat-specific method
        System.out.println(name + " says: Meow!");
    }
}
```

**Using inheritance:**

```java
public class AnimalDemo {
    public static void main(String[] args) {
        Dog myDog = new Dog("Buddy", 3, "Golden Retriever");
        Cat myCat = new Cat("Whiskers", 2, true);
        
        myDog.eat();   // Inherited from Animal
        myDog.bark();  // Dog's own method
        
        myCat.eat();   // Inherited from Animal
        myCat.meow();  // Cat's own method
    }
}
```

**Key point:** Dog and Cat both have `eat()` and `sleep()` methods without repeating code!

---

### 3. **Polymorphism** 🎭
*"Many forms - one interface, different implementations"*

This means the same method name can behave differently for different classes:

```java
public class Animal {
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }
}

public class Dog extends Animal {
    @Override  // We're replacing the parent's method
    public void makeSound() {
        System.out.println("Woof! Woof!");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}

public class Cow extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Moo!");
    }
}
```

**The magic of polymorphism:**

```java
public class PolymorphismDemo {
    public static void main(String[] args) {
        Animal[] animals = new Animal[3];
        animals[0] = new Dog("Buddy", 3, "Retriever");
        animals[1] = new Cat("Whiskers", 2, true);
        animals[2] = new Cow("Bessie", 4);
        
        // Same method call, different behaviors!
        for (Animal animal : animals) {
            animal.makeSound();
        }
        // Output:
        // Woof! Woof!
        // Meow!
        // Moo!
    }
}
```

---

### 4. **Abstraction** 🎨
*"Hiding complex details, showing only what's necessary"*

Sometimes we want to define WHAT something should do, but not HOW it does it:

```java
// Abstract class - cannot create objects directly from it
public abstract class Shape {
    protected String color;
    
    public Shape(String color) {
        this.color = color;
    }
    
    // Abstract method - subclasses MUST implement this
    public abstract double calculateArea();
    
    // Regular method - all shapes can use this
    public void displayColor() {
        System.out.println("This shape is " + color);
    }
}

public class Circle extends Shape {
    private double radius;
    
    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

public class Rectangle extends Shape {
    private double width;
    private double height;
    
    public Rectangle(String color, double width, double height) {
        super(color);
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
}
```

**Using abstraction:**

```java
public class ShapeDemo {
    public static void main(String[] args) {
        Shape circle = new Circle("Red", 5);
        Shape rectangle = new Rectangle("Blue", 4, 6);
        
        circle.displayColor();
        System.out.println("Area: " + circle.calculateArea());
        
        rectangle.displayColor();
        System.out.println("Area: " + rectangle.calculateArea());
    }
}
```

---

## Complete Practice Example 🎯

Let's put it all together with a simple bank account system:

```java
// Encapsulation example
public class BankAccount {
    private String accountNumber;
    private String ownerName;
    private double balance;
    
    // Constructor
    public BankAccount(String accountNumber, String ownerName) {
        this.accountNumber = accountNumber;
        this.ownerName = ownerName;
        this.balance = 0.0;
    }
    
    // Getters
    public String getAccountNumber() {
        return accountNumber;
    }
    
    public String getOwnerName() {
        return ownerName;
    }
    
    public double getBalance() {
        return balance;
    }
    
    // Methods with validation
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount);
        } else {
            System.out.println("Invalid deposit amount");
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
        } else {
            System.out.println("Invalid withdrawal amount or insufficient funds");
        }
    }
    
    public void displayAccountInfo() {
        System.out.println("Account: " + accountNumber);
        System.out.println("Owner: " + ownerName);
        System.out.println("Balance: $" + balance);
    }
}

// Test the class
public class BankDemo {
    public static void main(String[] args) {
        BankAccount myAccount = new BankAccount("12345", "John Doe");
        
        myAccount.deposit(1000);
        myAccount.withdraw(250);
        myAccount.displayAccountInfo();
        
        // This won't work - balance is private!
        // myAccount.balance = 1000000;  // Compilation error
    }
}
```

---

## Quick Reference Card 📝

| Concept | What It Means | Example |
|---------|---------------|---------|
| **Class** | Blueprint for objects | `public class Dog { }` |
| **Object** | Instance of a class | `Dog myDog = new Dog();` |
| **Constructor** | Special method to initialize objects | `public Dog(String name) { }` |
| **Encapsulation** | Hide data, use getters/setters | `private int age;` |
| **Inheritance** | One class extends another | `class Dog extends Animal` |
| **Polymorphism** | Same method, different behavior | `@Override makeSound()` |
| **Abstraction** | Hide complexity, show essentials | `abstract class Shape` |

---

## Key Takeaways 🎓

1. **Classes are blueprints**, objects are the actual things
2. **Encapsulation** keeps your data safe with private variables
3. **Inheritance** lets you reuse code (child classes inherit from parent)
4. **Polymorphism** allows different classes to respond to the same method differently
5. **Abstraction** hides unnecessary details

---

## Practice Exercises 💪

Try creating these on your own:

1. **Student Class**: Create a Student class with name, ID, and GPA. Add methods to update GPA and display student info.

2. **Vehicle Hierarchy**: Create a Vehicle parent class and Car, Motorcycle child classes with inheritance.

3. **Library System**: Create Book and Library classes where Library manages multiple Books.

---

## What's Next?

You now know the fundamentals! When you're ready, explore:
- Interfaces
- Static vs Instance members
- Collections (ArrayList, HashMap)
- Exception handling

---

**Happy Coding! 🚀**

Remember: OOP is about organizing code to mirror real-world concepts. Start simple, practice often, and build up gradually!
