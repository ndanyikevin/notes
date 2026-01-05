Positional parameters in **Dart** are function or constructor parameters that are identified **by their position (order)** rather than by name. When you call the function, you must pass values in the exact order they are defined.

Dart has **two types** of positional parameters:

---

## ✅ 1. **Required positional parameters**

These are the simplest kind — you _must_ pass them, and in order.

### Example:

```dart
void greet(String name, int age) {
  print("Hello $name, you are $age years old");
}

greet("Kevin", 16); // correct order required
```

---

## ✅ 2. **Optional positional parameters**

These use **square brackets `[]`**.  
They are optional, and you can provide default values.

### Example:

```dart
void greet(String name, [String title = ""]) {
  print("Hello $title $name");
}

greet("Kevin");             // uses default title ""
greet("Kevin", "Mr.");      // overrides title
```

### Notes:

- Optional positional parameters must come _after_ required ones.
    
- You must respect the order: you can’t skip an optional parameter and fill the next one.
    

---

## 🤝 Positional vs Named Parameters (quick comparison)

|Type|Syntax|Call Style|
|---|---|---|
|**Positional**|`func(a, b, [c])`|`func(1, 2)`|
|**Named**|`func({a, b})`|`func(a: 1)`|
|Easier when order matters|More readable||

---

If you want, I can also explain **named parameters**, **default values**, **required keyword**, or rewrite your own Dart functions using them.