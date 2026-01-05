A **class in Dart** is a blueprint for creating **objects**.  
It defines what an object **is** (its data) and what it **can do** (its functions/behaviors).

Think of a class like a **template**, and objects are the **actual things created from the template**.

---

# ✅ **What a class contains**

A Dart class can include:

- **Fields (variables / data)**
    
- **Methods (functions inside a class)**
    
- **Constructors (special functions used to create objects)**
    
- **Getters & setters**
    
- **Other classes (nested)**
    

---

# ✅ **Basic example of a class**

```dart
class Student {
  // fields
  String name;
  int age;

  // constructor
  Student(this.name, this.age);

  // method
  void introduce() {
    print("My name is $name and I'm $age years old.");
  }
}

void main() {
  // creating an object
  var student1 = Student("Kevin", 16);
  student1.introduce();
}
```

### Output:

```
My name is Kevin and I'm 16 years old.
```

---

# ✅ Key ideas (simple)

### 1. **A class defines structure**

```dart
class Car {
  String model;
  int year;
}
```

### 2. **You create objects from the class**

```dart
var myCar = Car();
```

### 3. **Classes group data + behavior**

```dart
class Car {
  String model;
  void drive() {
    print("Driving...");
  }
}
```

---

# 🎯 Why classes are useful?

- They help organize code.
    
- They let you create many objects with the same structure.
    
- They support OOP features like inheritance, encapsulation, etc.
    

---

If you want, I can explain **constructors**, **inheritance**, **static classes**, or help you build a real-world class (like User, Product, Invoice, etc.).