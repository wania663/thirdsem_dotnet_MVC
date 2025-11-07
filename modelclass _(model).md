# 🧩 User Model — Complete Explanation  

---

## 💡 Simple Meaning  

`User.cs` ek **Model Class** hai —  
jiska kaam hota hai **data ka structure define karna** (like ek blueprint).  

Jese SQL me hum **table banate hain columns ke sath**,  
waise hi yahan C# me **class ke properties** hoti hain jo **columns** ban jaati hain database me.  

---

## 🧠 Breakdown  

```csharp
public class User
{
    public int Id { get; set; }       // Primary Key (auto increment)
    public string Name { get; set; }  // User ka naam
    public string Email { get; set; } // User ka email
    public int Age { get; set; }      // User ki age
}
````

### 🧩 Explanation Line by Line

| Code                                | Meaning                                                                              |
| ----------------------------------- | ------------------------------------------------------------------------------------ |
| `public class User`                 | Ye ek **Model Class** hai (like ek design ya template for data).                     |
| `public int Id { get; set; }`       | Ye primary key column banega (Entity Framework automatically auto-increment karega). |
| `public string Name { get; set; }`  | Ye **Name** column banega SQL me (user ka naam store karega).                        |
| `public string Email { get; set; }` | Ye **Email** column banega.                                                          |
| `public int Age { get; set; }`      | Ye **Age** column banega.                                                            |

---

## ⚙️ Entity Framework Magic

Entity Framework kya karta hai 👇

> Tumhara `User` class uthata hai →
> `AppDbContext` me `DbSet<User>` dekhta hai →
> Automatically SQL me ek **Users** table create kar deta hai jisme columns hote hain:
> **Id, Name, Email, Age**

---

## 📘 Exam / Interview Line

> “A Model class in ASP.NET Core represents the **structure of data**.
> Each property of the class becomes a **column in the database table** when using Entity Framework.”

---

## 💬 Easy Example in Real Life

Socho tum ek **form banate ho user ke data ke liye**.
Us form me fields hoti hain: Name, Email, Age.
C# me ye sab ek **Model Class** me likhte ho —
Entity Framework unhe **table ke columns** me convert kar deta hai.

---

## ✅ Summary

| Concept          | Meaning                                        |
| ---------------- | ---------------------------------------------- |
| Model Class      | Data ka blueprint (structure define karta hai) |
| Property         | Table ka column                                |
| Entity Framework | Class ko Table me convert karta hai            |
| `Id`             | Primary Key (auto increment)                   |

---

## 🔥 Short Viva Answer

> “Model class ek blueprint hoti hai jo data ka structure define karti hai.
> Entity Framework ise database table me convert karta hai — har property ek column ban jaati hai.”

---

```

---

chaho mai next **`AppDbContext.md`** bhi isi pro format me ready kar du (upload-style)?
```
