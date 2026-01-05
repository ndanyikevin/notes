An **exception** in Dart is an error that happens **while your program is running**.  
When something goes wrong—like dividing by zero, missing a file, or invalid input—Dart “throws” an **exception** to signal the problem.

Instead of crashing the whole app, you can **catch** the exception and handle it.

---

# ✅ Simple definition

> An **exception** is a runtime error that stops normal program execution unless it is handled.

---

# ✅ Example of an exception

```dart
void main() {
  int a = 10;
  int b = 0;

  int result = a ~/ b; // this throws an exception
  print(result);
}
```

This will throw:

```
IntegerDivisionByZeroException
```

---

# ✅ Handling exceptions (try–catch)

```dart
void main() {
  try {
    int x = 10 ~/ 0;
  } catch (e) {
    print("An error occurred: $e");
  }
}
```

Output:

```
An error occurred: IntegerDivisionByZeroException
```

---

# ❗ Why exceptions are useful?

- Prevent apps from crashing
    
- Allow you to handle errors safely
    
- Make debugging easier
    

---

# 🔧 Try–Catch–Finally structure

```dart
try {
  // code that may fail
} on FormatException {
  // handle specific exception
} catch (e, stackTrace) {
  // handle any exception
} finally {
  // always runs (optional)
}
```

---

# 🎯 Summary

|Term|Meaning|
|---|---|
|**throw**|Create an exception|
|**try**|Code that might fail|
|**catch**|Handle the error|
|**finally**|Always runs|

---

If you want, I can explain:

- custom exceptions
    
- `throw` keyword
    
- specific exception types
    
- or real examples for apps (API errors, null errors, etc.).