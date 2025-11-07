# 🚀 Entity Framework (EF) — Scratch to Pro Notes

---

## 🧠 What is Entity Framework?

Entity Framework (EF) ek **ORM (Object Relational Mapper)** hai jo .NET apps me database ke sath kaam karna easy banata hai.

**ORM ka matlab:**  
Database ke tables ko C# classes me convert kar deta hai —  
aur aap C# code likh kar directly data insert, update, delete, fetch kar sakte ho — SQL likhne ki zarurat nahi.

---

## ⚙️ EF ka Kaam Kya Hai?

EF database aur C# ke beech bridge ka kaam karta hai:
- Data ko fetch / insert / update / delete karna  
- SQL queries automatically generate karna  
- Database schema manage karna via **Migration**

---

## 💡 Entity Framework ke Types

1️⃣ **EF 6 (Entity Framework Classic)**  
   - Sirf .NET Framework ke liye use hota tha  
   - Thoda slow aur heavy  

2️⃣ **EF Core (Entity Framework Core)**  
   - Latest & lightweight version  
   - Work karta hai .NET Core aur .NET 6/7 dono pe  
   - Cross-platform (Windows, Linux, Mac)

✅ Modern projects me **EF Core** use hota hai.

---

## 🧩 EF Core — Important Components

| Component | Description |
|------------|-------------|
| **Model Class** | Database table ke structure ko represent karti hai |
| **DbContext Class** | Database ke sath connection aur operations handle karti hai |
| **Migration Files** | Table create/update/delete ke liye auto SQL code store karti hain |

---

## 🧱 MODEL CLASS

**Example:**
```csharp
namespace MyApp.Models
{
    public class User
    {
        public int Id { get; set; }      // Primary Key
        public string Name { get; set; } // User name
        public string Email { get; set; }// Email
        public int Age { get; set; }     // Age
    }
}
````

### 📘 Explanation:

* Ye ek **class = Table** ke barabar hai.
* Har **property = Column** hoti hai.
* `Id` automatically **Primary Key** ban jaata hai.

---

## 🧠 DBCONTEXT CLASS

**Example:**

```csharp
using Microsoft.EntityFrameworkCore;

namespace MyApp.Models
{
    public class AppDbContext : DbContext
    {
        public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }

        public DbSet<User> Users { get; set; }
    }
}
```

### 📘 Explanation:

* `AppDbContext` ka kaam hota hai database se connection handle karna.
* `DbSet<User>` ka matlab hai ek **table named “Users”** banegi in DB.

---

## ⚡ MIGRATION FILES

Migration ka use database structure ko **code ke through create/update** karne ke liye hota hai.

### 🧩 Step-by-Step Migration Setup:

1️⃣ **Add EF Core Package:**

```
Install-Package Microsoft.EntityFrameworkCore
Install-Package Microsoft.EntityFrameworkCore.SqlServer
Install-Package Microsoft.EntityFrameworkCore.Tools
```

2️⃣ **Add Migration Command:**

```
Add-Migration InitialCreate
```

➡️ Ye command ek migration file banayegi (tables create karne ke liye SQL code ke sath).

3️⃣ **Update Database:**

```
Update-Database
```

➡️ Ye command database me tables create kar degi based on model classes.

---

## 🧱 Example: End-to-End Flow

### Step 1 — Model

```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

### Step 2 — DbContext

```csharp
public class AppDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }
}
```

### Step 3 — Migration + Update

```
Add-Migration AddProductTable
Update-Database
```

🎉 Result → Database me “Products” table create ho jayegi.

---

## 🧰 Common EF Commands

| Command                | Description                                |
| ---------------------- | ------------------------------------------ |
| `Add-Migration <name>` | Nayi migration file create karta hai       |
| `Update-Database`      | DB update karta hai migrations ke basis pe |
| `Remove-Migration`     | Last migration delete karta hai            |
| `Get-Migrations`       | Saari migrations list dikhata hai          |

---

## 🧾 EF ke CRUD Operations (via LINQ)

```csharp
// Insert
var user = new User { Name="Alex", Email="alex@mail.com", Age=22 };
_context.Users.Add(user);
_context.SaveChanges();

// Read
var users = _context.Users.ToList();

// Update
var u = _context.Users.Find(1);
u.Name = "Alex Johnson";
_context.SaveChanges();

// Delete
var del = _context.Users.Find(1);
_context.Users.Remove(del);
_context.SaveChanges();
```

---

## 🧠 Why EF is Used?

✅ No need to write SQL manually
✅ Clean & readable code
✅ Faster development
✅ Works with different databases
✅ Easy to maintain and scale

---

## 🎯 Interview + Exam Short Answers

| Question                  | Short Answer                                         |
| ------------------------- | ---------------------------------------------------- |
| What is Entity Framework? | It’s an ORM that maps database tables to C# classes. |
| What is DbContext?        | A bridge between app & database for CRUD operations. |
| What is Migration?        | A way to create/update DB using C# code.             |
| What is Model class?      | A class that defines table structure.                |
| EF Core vs EF 6?          | EF Core is lightweight, cross-platform, and modern.  |
| ORM full form?            | Object Relational Mapper.                            |

---

## 🧩 Pro Tip

Entity Framework + LINQ = Full power combo 💪
You write queries in C#, EF converts them into optimized SQL automatically.

---

# ✅ Summary

EF Core =

> “Code likho → Table auto create ho → Data auto manage ho”

It’s like magic for database handling in .NET apps 💫

---


