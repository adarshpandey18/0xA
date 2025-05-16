_Architectural blueprints for building adaptable, scalable, and durable software._

---

## **S - Single Responsibility Princi[]()ple (SRP)**

> A class should have only one reason to change.

**Example – Violating SRP:**

```dart
class UserManager {
  bool authenticatedUser(String username, String password) {
    return true;
  }

  void updateProfile(String username, Map<String, dynamic> profile) {
    print("Profile Updated: $username");
  }
}
```

This class handles **both authentication and profile updating**, violating SRP. If either authentication or profile logic changes, the class must be modified, making it harder to maintain.

**Benefits of SRP:**
- Easier to understand
- Easier to name and organize
- Improved readability
- Better maintainability

---

## **O - Open/Closed Principle (OCP)**

> Software entities (classes, modules, functions, etc.) should be **open for extension but closed for modification**.

**Violation Example:**

```dart
class Shape {
  String type;
  Shape(this.type);
}

class AreaCalculator {
  double calculateArea(Shape shape) {
    if (shape.type == 'circle') {
      return 3.14 * 3.14;
    } else if (shape.type == 'rectangle') {
      return 4 * 5;
    }
    return 0;
  }
}
```

This design requires modifying existing code to add new shapes, which violates OCP.

**Improved (OCP Compliant):**

```dart
abstract interface class Shape {
  double calculateArea();
}

class Circle implements Shape {
  double radius;
  Circle(this.radius);

  @override
  double calculateArea() {
    return 3.14 * radius * radius;
  }
}

class Rectangle implements Shape {
  double length;
  double breadth;
  Rectangle(this.length, this.breadth);

  @override
  double calculateArea() {
    return length * breadth;
  }
}

class AreaCalculator {
  double calculateArea(Shape shape) {
    return shape.calculateArea();
  }
}
```

**Benefits of OCP:**
- Promotes extensibility
- Reduces bugs from modifying existing code    
- Encourages use of abstraction and polymorphism

---

## **L - Liskov Substitution Principle (LSP)**

> Subtypes must be substitutable for their base types without altering the correctness of the program.

**Correct Example:**

```dart
abstract class Animal {
  void makeSound();
}

class Lion implements Animal {
  @override
  void makeSound() {
    print("Roar");
  }
}

void main() {
  Animal lion = Lion(); // Substituting parent with child
  lion.makeSound();
}
```

**Violation Example:**

```dart
class Animal {
  void makeSound() {
    print("The animal is making sound");
  }
}

class Lion extends Animal {
  @override
  void makeSound() {
    super.makeSound();
    print("Lion is roaring");
  }
}
```

This introduces unexpected behavior—**inconsistent behavior from subclasses** can violate LSP.

**Benefits of LSP:**
- Encourages consistency
- Reduces unexpected behavior
- Improves modularity and reliability    

---

## **I - Interface Segregation Principle (ISP)**

> Clients should not be forced to depend on interfaces they do not use.

**Violation Example:**

```dart
abstract interface class Worker {
  void eat();
  void work();
}

class Developer implements Worker {
  @override
  void eat() {
    print("Developer eating");
  }

  @override
  void work() {
    print("Developer working");
  }
}
```

Developers may not need the `eat()` method; it forces them to implement irrelevant behavior.

**ISP Compliant:**

```dart
abstract interface class Worker {
  void work();
}

abstract interface class Eater {
  void eat();
}

class Developer implements Worker {
  @override
  void work() {
    print("Developer working");
  }
}

class Waiter implements Worker, Eater {
  @override
  void work() {
    print("Waiter working");
  }

  @override
  void eat() {
    print("Waiter eating");
  }
}
```

**Benefits of ISP:**
- Cleaner and more focused interfaces
- Avoids unnecessary implementation
- Encourages better software design

---

## **D - Dependency Inversion Principle (DIP)**

> High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Violation Example:**

```dart
class IncandescentBulb {
  void turnOn() {
    print("Turn on");
  }

  void turnOff() {
    print("Turn off");
  }
}

class Room {
  IncandescentBulb bulb;
  Room(this.bulb);

  void turnOnBulb() {
    bulb.turnOn();
  }

  void turnOffBulb() {
    bulb.turnOff();
  }
}
```

Room is tightly coupled to `IncandescentBulb`.

**DIP Compliant:**

```dart
abstract interface class Bulb {
  void turnOn();
  void turnOff();
}

class IncandescentBulb implements Bulb {
  @override
  void turnOn() {
    print("Turn on");
  }

  @override
  void turnOff() {
    print("Turn off");
  }
}

class Room {
  Bulb bulb;
  Room(this.bulb);

  void turnOnBulb() {
    bulb.turnOn();
  }

  void turnOffBulb() {
    bulb.turnOff();
  }
}
```

**Benefits of DIP:**
- Decouples high-level and low-level components
- Easier to test and extend
- Encourages abstraction and loose coupling

---

| Principle | Core Idea                                            |
| --------- | ---------------------------------------------------- |
| SRP       | One class = One responsibility                       |
| OCP       | Open for extension, closed for modification          |
| LSP       | Subtypes must behave like their base types           |
| ISP       | Don’t force classes to implement unused interfaces   |
| DIP       | Depend on abstractions, not concrete implementations |
