In Java, **classes**, **methods**, and **objects** are fundamental concepts that form the basis of object-oriented programming (OOP). Here's a detailed explanation of each:

---

### **1. Classes**
A **class** is a blueprint for creating objects. It defines the properties (attributes) and behaviors (methods) that the objects of the class will have.

#### Characteristics:
- It acts as a template or a blueprint.
- It can contain fields (variables), methods, constructors, and sometimes nested classes.
- A class must be instantiated to create objects.

#### Syntax:
```java
class ClassName {
    // fields (attributes)
    int age;
    String name;

    // methods (behaviors)
    void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}
```

---

### **2. Methods**
A **method** is a block of code within a class that performs a specific task. Methods define the behavior of the objects of a class.

#### Characteristics:
- Methods can take inputs (parameters) and may return a value.
- They enable code reuse by allowing operations to be defined once and called multiple times.
- Java has special methods like `main()`, which acts as the entry point of the program, and constructors for initializing objects.

#### Syntax:
```java
returnType methodName(parameters) {
    // method body
    return value; // optional, depending on returnType
}
```

#### Example:
```java
class MathOperations {
    int add(int a, int b) {
        return a + b;
    }
}
```

---

### **3. Objects**
An **object** is an instance of a class. It represents a specific entity with the properties and behaviors defined by its class.

#### Characteristics:
- Objects are created from classes.
- Each object can have its own unique values for the properties defined in the class.
- Objects interact with one another by calling each other's methods.

#### Creating an Object:
```java
ClassName objectName = new ClassName();
```

#### Example:
```java
class Person {
    String name;
    int age;

    void sayHello() {
        System.out.println("Hello, my name is " + name);
    }
}

// Creating and using an object
public class Main {
    public static void main(String[] args) {
        Person person1 = new Person(); // Create an object
        person1.name = "Alice"; // Set attributes
        person1.age = 25;

        person1.sayHello(); // Call method
    }
}
```

**Output:**
```
Hello, my name is Alice
```

---

### Summary
- **Class**: Defines the structure and behavior of objects.
- **Method**: A function defined inside a class that specifies actions objects can perform.
- **Object**: A specific instance of a class with its own state and behavior.

In essence:
> A class is like a blueprint, methods are the instructions, and objects are the actual items built from that blueprint.

------------------------------------------------------------------------------------------------------------------

Object-Oriented Programming (OOP) is based on four key principles: **Encapsulation**, **Inheritance**, **Polymorphism**, and **Abstraction**. Below is an explanation of each principle with examples in Java.

### 1. **Encapsulation**
Encapsulation is the bundling of data (fields) and methods that operate on the data into a single unit (class). It also involves restricting direct access to some components of an object, typically using private fields and public getter/setter methods.

**Example:**

```java
class Employee {
    private String name; // Encapsulated field
    private int age;

    // Constructor
    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getter and Setter for 'name'
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    // Getter and Setter for 'age'
    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age > 0) { // Basic validation
            this.age = age;
        } else {
            System.out.println("Age must be positive.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee("John", 30);
        System.out.println("Name: " + emp.getName());
        System.out.println("Age: " + emp.getAge());

        emp.setAge(35); // Updating age
        System.out.println("Updated Age: " + emp.getAge());
    }
}
```

---

### 2. **Inheritance**
Inheritance allows a class (child) to inherit fields and methods from another class (parent). This promotes code reuse and establishes a hierarchy.

**Example:**

```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal { // Inheriting from Animal
    void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat(); // Inherited method
        dog.bark(); // Dog's own method
    }
}
```

---

### 3. **Polymorphism**
Polymorphism allows methods to have multiple forms. This can be achieved via method overriding (runtime polymorphism) or method overloading (compile-time polymorphism).

**Example: Method Overriding (Runtime Polymorphism):**

```java
class Animal {
    void makeSound() {
        System.out.println("Some generic animal sound.");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Meow.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Cat(); // Polymorphic reference
        myAnimal.makeSound(); // Calls Cat's version of makeSound()
    }
}
```

**Example: Method Overloading (Compile-Time Polymorphism):**

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 10)); // Calls int version
        System.out.println(calc.add(5.5, 10.5)); // Calls double version
    }
}
```

---

### 4. **Abstraction**
Abstraction involves hiding implementation details and exposing only the essential features of an object. It can be achieved through abstract classes or interfaces.

**Example: Using an Abstract Class:**

```java
abstract class Shape {
    abstract void draw(); // Abstract method
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a circle.");
    }
}

class Rectangle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a rectangle.");
    }
}

public class Main {
    public static void main(String[] args) {
        Shape s1 = new Circle();
        Shape s2 = new Rectangle();

        s1.draw();
        s2.draw();
    }
}
```

---


------------------------------------------------------------------------------------------------------------------

# Super Keyword In JAVA

The **`super`** keyword in Java is used to refer to the immediate parent class of a subclass. It has three main uses:

1. **Access Parent Class Methods**  
   You can call a method in the parent class that is overridden in the child class.  
   ```java
   class Parent {
       void display() {
           System.out.println("Parent method");
       }
   }
   class Child extends Parent {
       void display() {
           System.out.println("Child method");
       }
       void show() {
           super.display(); // Calls the parent class method
       }
   }
   ```

2. **Access Parent Class Variables**  
   If a parent class and a child class have variables with the same name, you can use `super` to refer to the parent class variable.  
   ```java
   class Parent {
       String name = "Parent";
   }
   class Child extends Parent {
       String name = "Child";
       void display() {
           System.out.println(super.name); // Refers to the parent class variable
       }
   }
   ```

3. **Call Parent Class Constructor**  
   You can use `super()` to call the parent class constructor, and it must be the first statement in the child class constructor.  
   ```java
   class Parent {
       Parent(String msg) {
           System.out.println("Parent Constructor: " + msg);
       }
   }
   class Child extends Parent {
       Child() {
           super("Hello from Child"); // Calls parent class constructor
       }
   }
   ```

The `super` keyword helps in managing inheritance and accessing parent class members efficiently.

------------------------------------------------------------------------------------------------------------------

# @Override is necessary or optional

Yes, the program works without `@Override`, but here's why you should still use it:

### Why Does It Work Without `@Override`?
The `@Override` annotation is optional. When you create a method in the child class with the **same signature** (name, parameters, and return type) as a method in the parent class, Java automatically treats it as an overridden method. The annotation is not required for this behavior.

### Why Use `@Override` Then?
1. **Error Checking**:  
   If you accidentally make a mistake in the method signature (e.g., typo in the method name or parameters), Java won’t treat it as overriding. Without `@Override`, this mistake won't cause a compilation error—it would create a new method instead.  
   Example:  
   ```java
   class Parent {
       void display() {
           System.out.println("Parent method");
       }
   }
   class Child extends Parent {
       // Mistyped method name
       void dispay() {
           System.out.println("Child method");
       }
   }
   ```
   Without `@Override`, this would compile without errors, but the `display()` method in the parent wouldn't be overridden. Using `@Override` would catch this mistake.

2. **Code Readability**:  
   The annotation explicitly indicates to other developers (and yourself) that the method is intentionally overriding a parent method.

3. **Consistency Across Code**:  
   Using `@Override` makes it clear that a method's behavior comes from overriding, not just a similar-looking method in the child class.

### Conclusion:
The program works because the Java compiler automatically determines overridden methods based on matching signatures. However, using `@Override` is considered a good practice for error checking and improving code clarity.

------------------------------------------------------------------------------------------------------------------

### Interface and Abstract Class Similarities:
1. **Blueprint Nature**:  
   Both **interfaces** and **abstract classes** define a structure or blueprint for other classes to follow. They cannot be instantiated directly.

2. **Enforce Contracts**:  
   They ensure that derived classes provide implementations for specific methods.  

---

### Interface:
1. **Purpose**:  
   An interface is a **pure abstraction**. It specifies what a class should do but not how it does it. Think of it as a contract that a class must adhere to.

2. **Characteristics**:
   - All methods in an interface are **implicitly abstract and public** (before Java 8).
   - A class can implement multiple interfaces (multiple inheritance of types).
   - Interfaces cannot have instance variables (but can have constants and, in modern Java, default and static methods).

3. **Use Case**:  
   Used when you want to define behavior that can be shared across **unrelated classes**.

---

### Abstract Class:
1. **Purpose**:  
   An abstract class is a **partial abstraction**. It can have some concrete methods (implemented) and some abstract methods (unimplemented).

2. **Characteristics**:
   - Can have instance variables.
   - Can have constructors.
   - A class can inherit only one abstract class (single inheritance of implementation).

3. **Use Case**:  
   Used when you have a **base class** that provides default behavior while allowing subclasses to override or extend it.

---

### Key Difference:
- **Abstract Class** is a mix of abstraction and implementation.  
- **Interface** is purely about abstraction and multiple behavior inheritance.  

---

### Example:

#### Abstract Class Example:
```java
abstract class Vehicle {
    int wheels;

    Vehicle(int wheels) {
        this.wheels = wheels;
    }

    abstract void move(); // Abstract method

    void display() { // Concrete method
        System.out.println("This vehicle has " + wheels + " wheels.");
    }
}

class Car extends Vehicle {
    Car() {
        super(4);
    }

    void move() {
        System.out.println("The car drives.");
    }
}
```

#### Interface Example:
```java
interface Animal {
    void eat();
    void sleep();
}

class Dog implements Animal {
    public void eat() {
        System.out.println("Dog eats food.");
    }

    public void sleep() {
        System.out.println("Dog sleeps soundly.");
    }
}
```

In summary:
- **Abstract class**: Partial blueprint with some default behaviors.
- **Interface**: Pure blueprint for behavior definition and sharing.

------------------------------------------------------------------------------------------------------------------

Access specifiers (or access modifiers) in Java determine the **visibility** and **accessibility** of classes, methods, constructors, and variables. They control who can use or modify certain parts of your code.

### Types of Access Specifiers:
1. **`public`**  
   - Accessible **everywhere**, inside and outside the class, package, and project.
   - Example:
     ```java
     public class Example {
         public void show() {
             System.out.println("Public method");
         }
     }
     ```

2. **`protected`**  
   - Accessible within the same package and by subclasses in other packages through inheritance.
   - Example:
     ```java
     class Parent {
         protected void display() {
             System.out.println("Protected method");
         }
     }
     class Child extends Parent {
         void test() {
             display(); // Accessible here
         }
     }
     ```

3. **`default`** *(no keyword)*  
   - Accessible **only within the same package**. Also known as **package-private**.
   - Example:
     ```java
     class Example {
         void show() { // No specifier, so default
             System.out.println("Default method");
         }
     }
     ```

4. **`private`**  
   - Accessible **only within the same class**. Not visible to other classes, even in the same package.
   - Example:
     ```java
     class Example {
         private void display() {
             System.out.println("Private method");
         }
         void show() {
             display(); // Can be accessed here
         }
     }
     ```

### Access Levels Summary:
| Modifier   | Same Class | Same Package | Subclass (Different Package) | Everywhere |
|------------|------------|--------------|------------------------------|------------|
| `public`   | ✅         | ✅          | ✅                           | ✅        |
| `protected`| ✅         | ✅          | ✅                           | ❌        |
| `default`  | ✅         | ✅          | ❌                           | ❌        |
| `private`  | ✅         | ❌          | ❌                           | ❌        |

### Notes:
- **Classes**: Only `public` and `default` are allowed as access specifiers for top-level classes.
- **Best Practices**:  
  - Use `private` for encapsulation to hide implementation details.  
  - Use `protected` for members that subclasses need.  
  - Use `public` for APIs and methods intended for global use.  

------------------------------------------------------------------------------------------------------------------

### **Method Overloading** vs **Method Overriding**

| **Aspect**            | **Method Overloading**                                           | **Method Overriding**                                             |
|-----------------------|------------------------------------------------------------------|------------------------------------------------------------------|
| **Definition**         | Defining multiple methods with the **same name** but **different parameters** in the same class. | Redefining a method in a **subclass** that already exists in the **parent class**, with the **same signature**. |
| **Purpose**            | To perform similar tasks with different input parameters. | To modify or extend the behavior of a method inherited from the parent class. |
| **Method Signature**   | Method signature must differ (in **number**, **type**, or **order** of parameters). | Method signature **must be exactly the same** (same name, parameters, and return type) as the parent class method. |
| **Return Type**        | Return type can be different, but it's not used to distinguish overloaded methods. | Return type **must be the same** or a subtype (covariant return type) in the subclass. |
| **Inheritance**        | Happens within the **same class**. | Happens between a **parent class** and a **child class** (through inheritance). |
| **Compile-Time or Run-Time** | Resolved at **compile-time** (compile-time polymorphism). | Resolved at **run-time** (run-time polymorphism). |
| **Method Access**      | Methods can be called based on the argument passed (based on parameter type/number). | Overridden method is called based on the **object type** (whether it’s parent or subclass type). |
| **Example**            | ```java public int add(int a) { return a + 10; } public double add(double a) { return a + 10.5; } ``` | ```java class Parent { void display() { System.out.println("Parent"); } } class Child extends Parent { void display() { System.out.println("Child"); } } ``` |

### Key Differences:

1. **Method Signature**:
   - **Overloading**: The methods must have the **same name** but **different parameter lists** (different number, type, or order of parameters).
   - **Overriding**: The method must have the **same name** and **same parameter list** as the method in the parent class.

2. **Purpose**:
   - **Overloading** is used when you need to perform the **same action** but with **different input types or numbers** of parameters.
   - **Overriding** is used to provide a **new implementation** for an inherited method in the **subclass**, allowing you to modify or extend the behavior of the parent class method.

3. **Inheritance**:
   - **Overloading**: Does not require inheritance, and it occurs within the same class.
   - **Overriding**: Requires inheritance (a child class overrides a method from its parent class).

4. **Binding**:
   - **Overloading**: Is resolved at **compile-time** based on the method signature (known as **compile-time polymorphism**).
   - **Overriding**: Is resolved at **run-time** based on the **object type** (known as **run-time polymorphism**).

### Code Example: 

#### **Method Overloading**:
```java
class Calculator {
    // Overloaded method with one parameter
    public int add(int a) {
        return a + 10;
    }

    // Overloaded method with two parameters
    public int add(int a, int b) {
        return a + b;
    }
}

public class TestOverloading {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5));      // Calls add(int)
        System.out.println(calc.add(5, 10));  // Calls add(int, int)
    }
}
```

#### **Method Overriding**:
```java
class Animal {
    // Parent method
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    // Overriding method in subclass
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

public class TestOverriding {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();
        Animal myDog = new Dog();  // Polymorphism in action

        myAnimal.sound();  // Animal makes a sound
        myDog.sound();     // Dog barks (overridden method)
    }
}
```

### Key Takeaways:
- **Overloading** allows you to have multiple methods with the same name but different parameters in the **same class**.
- **Overriding** allows a **subclass** to provide a specific implementation for a method already defined in the **parent class**.


    Yes, the program works without `@Override`, but here's why you should still use it:

    ### Why Does It Work Without `@Override`?
    The `@Override` annotation is optional. When you create a method in the child class with the **same signature** (name, parameters, and return type) as a method in the parent class, Java automatically treats it as an overridden method. The annotation is not required for this behavior.

    ### Why Use `@Override` Then?
    1. **Error Checking**:  
    If you accidentally make a mistake in the method signature (e.g., typo in the method name or parameters), Java won’t treat it as overriding. Without `@Override`, this mistake won't cause a compilation error—it would create a new method instead.  
    Example:  
    ```java
    class Parent {
        void display() {
            System.out.println("Parent method");
        }
    }
    class Child extends Parent { 
        // Mistyped method name
        void dispay() {
            System.out.println("Child method");
        }
    }
    ```
    Without `@Override`, this would compile without errors, but the `display()` method in the parent wouldn't be overridden. Using `@Override` would catch this mistake.

    2. **Code Readability**:  
    The annotation explicitly indicates to other developers (and yourself) that the method is intentionally overriding a parent method.

    3. **Consistency Across Code**:  
    Using `@Override` makes it clear that a method's behavior comes from overriding, not just a similar-looking method in the child class.

    ### Conclusion:
    The program works because the Java compiler automatically determines overridden methods based on matching signatures. However, using `@Override` is considered a good practice for error checking and improving code clarity.

------------------------------------------------------------------------------------------------------------------


### **Final Keyword in Java (OOPs)**

The `final` keyword in Java is a modifier that can be applied to variables, methods, and classes. It provides **restrictions** in the following ways:

1. **Final Variables**: 
   - When a variable is declared as `final`, its value cannot be changed after it is initialized. It becomes a constant.
   - Example: `final int x = 10;`

2. **Final Methods**: 
   - A `final` method cannot be overridden by a subclass. This is useful when you want to enforce a specific behavior in a method.
   - Example: `final void display() { ... }`

3. **Final Classes**: 
   - A class declared as `final` cannot be extended by other classes. This is useful for creating immutable classes or preventing inheritance.
   - Example: `final class A { ... }`

### Code Examples

#### **Final Variable**
```java
class FinalVariableExample {
    public static void main(String[] args) {
        final int x = 100;  // Final variable
        System.out.println("The value of x is: " + x);

        // Uncommenting the following line will cause a compile-time error
        // x = 200;  // Error: cannot assign a value to final variable 'x'
    }
}
```

#### **Final Method**
```java
class Parent {
    final void display() {
        System.out.println("This is a final method and cannot be overridden.");
    }
}

class Child extends Parent {
    // Uncommenting the following code will cause a compile-time error
    // void display() {
    //     System.out.println("Trying to override a final method."); // Error
    // }
}

public class FinalMethodExample {
    public static void main(String[] args) {
        Child obj = new Child();
        obj.display();
    }
}
```

#### **Final Class**
```java
final class FinalClass {
    void show() {
        System.out.println("This is a final class and cannot be extended.");
    }
}

// Uncommenting the following code will cause a compile-time error
// class SubClass extends FinalClass { }  // Error: Cannot inherit from final class

public class FinalClassExample {
    public static void main(String[] args) {
        FinalClass obj = new FinalClass();
        obj.show();
    }
}
```

### Use Cases of `final` Keyword
- **Final Variables**: To define constants whose values should not change.
- **Final Methods**: To prevent method overriding when you want a fixed implementation.
- **Final Classes**: To prevent inheritance, which can help in creating immutable classes (e.g., `String` in Java is a `final` class).
