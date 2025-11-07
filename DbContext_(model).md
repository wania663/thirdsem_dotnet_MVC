# ⚙️ AppDbContext — Bridge Between Code & Database  

> **DbContext** is the *heart* of Entity Framework — it connects your **C# models** with your **SQL database**.  

---

## 💡 What is DbContext?

**DbContext** ek special class hoti hai jo **Entity Framework** me use hoti hai  
aur iska main kaam hota hai tumhare **C# code aur SQL database** ke beech bridge ka kaam karna.  

🧠 In easy words:
> “DbContext = Database ka Gatekeeper”  
Ye hi handle karta hai sab CRUD (Create, Read, Update, Delete) operations.

---

## 🔧 Example Code

```csharp
using Microsoft.EntityFrameworkCore;

namespace MyApp.Models
{
    public class AppDbContext : DbContext
    {
        public AppDbContext(DbContextOptions<AppDbContext> options)
            : base(options) { }

        public DbSet<User> Users { get; set; } // SQL me "Users" table banayega
    }
}
````

---

## 🧩 Code Explanation

| Code                       | Description                                                                                                          |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `AppDbContext : DbContext` | Tumhari class Entity Framework ke DbContext se inherit kar rahi hai → iska matlab ye database se baat kar sakti hai. |
| `DbSet<User> Users`        | Ye line “User” model ke liye ek SQL table create karti hai.                                                          |
| `base(options)`            | Ye constructor me connection string use karta hai jo `appsettings.json` se aati hai.                                 |

---

## 🧠 Role of DbContext

1️⃣ **Database Connection Handle** karta hai
2️⃣ **Models ko Tables** ke saath map karta hai
3️⃣ **Data Changes Track** karta hai (insert/update/delete)
4️⃣ **CRUD Operations** perform karta hai

---

## 🔄 Entity Framework Flow

```
Model Class → DbSet<Model> → DbContext → Database Table
```

### Example:

* `User.cs` → Model
* `AppDbContext.cs` → Database Manager
* SQL → “Users” Table

---

## 💬 Exam / Interview Answer

> **“DbContext is a class in Entity Framework that acts as a bridge between C# code and the database.
> It manages database connections, maps model classes to SQL tables, and performs CRUD operations.”**

---

## ⚡ Key Points for Viva

* DbContext → Base class of Entity Framework
* Connects code with database
* Handles CRUD operations
* Maps C# classes → SQL tables
* Used inside `AppDbContext.cs`

---

## 🧠 Pro Tip

Every model you want in the database must be listed as a **DbSet** inside your **DbContext** class —
varna Entity Framework us model ke liye table create nahi karega.

---

✅ **Summary:**

> `AppDbContext` = Database Manager
> `DbSet<Model>` = Table
> `Model Class` = Table Columns

---

```


