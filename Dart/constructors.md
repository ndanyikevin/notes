A **constructor** in Dart is a special function inside a class that runs **automatically** when you create an object.  
Its job is to **initialize the object’s data** (set up the values of the class fields).

Think of a constructor as the _setup method_ for a new object.

---

# ✅ Basic example

```dart
class Person {
  String name;
  int age;

  // constructor
  Person(this.name, this.age);
}

void main() {
  var p = Person("Kevin", 16);
  print(p.name); // Kevin
}
```

Here, the constructor:

```dart
Person(this.name, this.age);
```

tells Dart to take the values you pass and assign them to the fields.

---

# ✅ What constructors do

- Run when you call `Person(...)`
    
- Initialize variables
    
- Prepare the object for use
    
- Can have parameters (or not)
    

---

# ✅ Types of constructors

### **1. Default constructor**

If you don’t write one, Dart creates it automatically.

```dart
class Car {
  Car(); // auto-created if you don’t write one
}
```

---

### **2. Parameter constructor**

```dart
class Car {
  String model;
  int year;

  Car(this.model, this.year);
}
```

---

### **3. Named constructors**

Useful when you want multiple ways to create an object.

```dart
class User {
  String name;
  int age;

  User(this.name, this.age);

  User.guest()
      : name = "Guest",
        age = 0;
}
```

---

# 🎯 Simple definition

> A **constructor** is a function that runs when you create a class object and initializes its values.

---

If you want, I can show the difference between:

- normal constructors
    
- named constructors
    
- factory constructors
    
- or help you write constructors for your own classes.