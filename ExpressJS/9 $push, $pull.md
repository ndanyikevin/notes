`push` and `pull` are **update operators** in MongoDB that let you **add or remove elements from array fields** inside a document.

They’re used with commands like `updateOne()`, `updateMany()`, or `findByIdAndUpdate()` in Mongoose or the MongoDB shell.

Let’s break them down 👇

---

## 🧱 Example Schema

Say you have a **User** collection:

```js
{
  _id: 1,
  name: "Kevin",
  hobbies: ["coding", "football"]
}
```

---

## 🟢 `$push` — Add to an Array

The `$push` operator **adds an element to an array**.

```js
db.users.updateOne(
  { name: "Kevin" },
  { $push: { hobbies: "music" } }
)
```

✅ Result:

```js
{
  _id: 1,
  name: "Kevin",
  hobbies: ["coding", "football", "music"]
}
```

---

### 💡 `$push` with Multiple Values (`$each`)

If you want to add **multiple items**:

```js
db.users.updateOne(
  { name: "Kevin" },
  { $push: { hobbies: { $each: ["traveling", "reading"] } } }
)
```

✅ Result:

```js
{
  _id: 1,
  name: "Kevin",
  hobbies: ["coding", "football", "music", "traveling", "reading"]
}
```

---

### ⚙️ `$push` with Sorting or Limiting

You can even sort or limit the array after pushing:

```js
db.users.updateOne(
  { name: "Kevin" },
  { $push: { scores: { $each: [95, 87], $sort: -1, $slice: 3 } } }
)
```

This:

- Adds new scores,
    
- Sorts descending,
    
- Keeps only top 3.
    

---

## 🔴 `$pull` — Remove from an Array

The `$pull` operator **removes elements that match a condition**.

```js
db.users.updateOne(
  { name: "Kevin" },
  { $pull: { hobbies: "football" } }
)
```

✅ Result:

```js
{
  _id: 1,
  name: "Kevin",
  hobbies: ["coding", "music", "traveling", "reading"]
}
```

---

### 💡 `$pull` with a Condition

You can remove objects from an array based on a condition.

Example — suppose each user has posts:

```js
{
  name: "Kevin",
  posts: [
    { title: "First Post", likes: 10 },
    { title: "Second Post", likes: 0 }
  ]
}
```

Remove posts with 0 likes:

```js
db.users.updateOne(
  { name: "Kevin" },
  { $pull: { posts: { likes: 0 } } }
)
```

✅ Result:

```js
{
  name: "Kevin",
  posts: [
    { title: "First Post", likes: 10 }
  ]
}
```

---

## 🧾 Summary

|Operator|Purpose|Example|
|---|---|---|
|`$push`|Add elements to an array|`{ $push: { hobbies: "music" } }`|
|`$push + $each`|Add multiple elements|`{ $push: { hobbies: { $each: ["x","y"] } } }`|
|`$pull`|Remove elements from an array|`{ $pull: { hobbies: "football" } }`|
|`$pull` (with condition)|Remove elements matching filter|`{ $pull: { posts: { likes: 0 } } }`|

---

### 🧠 Quick Analogy

- **`$push`** → “append” or “add to a list”
    
- **`$pull`** → “filter out” or “remove from a list”
    

---

Would you like me to show how to use `$push` and `$pull` with **Mongoose models** (e.g., adding/removing comments from a post)?