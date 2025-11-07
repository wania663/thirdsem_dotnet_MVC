# 💾 Entity Framework (Scratch → Pro)

---

## 💡 What is Entity Framework?

**Entity Framework (EF)** ek **Object Relational Mapper (ORM)** hai.  
Ye **C# code** ko **SQL database** ke sath connect karne ke liye use hota hai — bina manually SQL likhe.

### 🧠 Simple Words:
> Entity Framework ek “bridge” hai between your **C# classes** and **SQL tables**.

---

## 🎯 Why Use Entity Framework?

| Problem (Without EF) | Solution (With EF) |
| -------------------- | ------------------ |
| SQL manually likhna padta hai | C# code se hi CRUD ho jata hai |
| Code maintenance hard | Organized aur reusable |
| Table schema change → code change manually | EF automatically handle karta hai |

---

## 🧩 3 Main Approaches in EF

| Approach | Meaning | Use Case |
| -------- | -------- | -------- |
| **Database-First** | Pehle database banao, fir EF models generate kare | Existing database ke liye |
| **Model-First** | Pehle model banao, fir EF database banaye | Visual designer projects ke liye |
| **Code-First** | Pehle code likho (model class), fir EF database banaye | Modern ASP.NET Core apps (recommended) |

---

## ⚙️ Code-First Structure (Most Used)

### 📁 Folder: Models/

| File | Description |
| ---- | ------------ |
| **User.cs** | Model Class — defines data structure |
| **AppDbContext.cs** | Bridge — connects C# classes with database |
| **Migration Files** | Auto-generated files — convert model → SQL Table |

---

## 🧱 Model Class (Example)

```csharp
namespace MyApp.Models
{
    public class User
    {
        public int Id { get; set; }       // Primary Key
        public string Name { get; set; }  // User ka naam
        public string Email { get; set; } // User ka email
        public int Age { get; set; }      // User ki age
    }
}
````

🧩 **Explanation:**
Each property = SQL column
Class = SQL Table

---

## 🔗 DbContext Class (Bridge Between Code & Database)

```csharp
using Microsoft.EntityFrameworkCore;

namespace MyApp.Models
{
    public class AppDbContext : DbContext
    {
        public AppDbContext(DbContextOptions<AppDbContext> options)
            : base(options) { }

        public DbSet<User> Users { get; set; } // Users table banayega
    }
}
```

🧠 **Meaning:**
`DbContext` — database se connection handle karta hai
`DbSet<User>` — table represent karta hai

---

## 🏗️ Migration Files (Auto SQL Creator)

Entity Framework code ko SQL me convert karta hai using **migrations**.

### Commands:

```bash
Add-Migration InitialCreate
Update-Database
```

🧩 **Explanation:**

* `Add-Migration` → Code changes ko ek migration file me convert karta hai
* `Update-Database` → Migration ko actual SQL table me apply karta hai

📂 **Example Folder Structure:**

```
Migrations/
 ├── 20251107123456_InitialCreate.cs
 ├── AppDbContextModelSnapshot.cs
```

---

## ⚡ CRUD Operations Example

### 🟢 Create

```csharp
var user = new User { Name = "Wania", Email = "wania@mail.com", Age = 17 };
_context.Users.Add(user);
_context.SaveChanges();
```

### 🔵 Read

```csharp
var users = _context.Users.ToList();
```

### 🟠 Update

```csharp
var user = _context.Users.Find(1);
user.Name = "Updated Wania";
_context.SaveChanges();
```

### 🔴 Delete

```csharp
var user = _context.Users.Find(1);
_context.Users.Remove(user);
_context.SaveChanges();
```

---

## 🔍 LINQ (Language Integrated Query)

EF ke sath LINQ use hota hai taaki SQL likhne ki zarurat na pade.

```csharp
var adults = _context.Users.Where(u => u.Age > 18).ToList();
```

🧠 LINQ automatically SQL me convert ho jaata hai → execute hota hai database me.

---

## 🔄 Lifecycle of Entity Framework (Code-First)

1. Create Model classes
2. Create DbContext
3. Configure connection string
4. Run migrations
5. Database auto-generate
6. Perform CRUD using EF

---

## 🧠 Internal Working

| Step | What Happens                 |
| ---- | ---------------------------- |
| 1    | EF reads your model classes  |
| 2    | DbContext maps them to SQL   |
| 3    | Migration generates SQL code |
| 4    | Database updates accordingly |

---

## 🧩 Interview / Viva Questions

| Question                     | Short Answer                                      |
| ---------------------------- | ------------------------------------------------- |
| What is Entity Framework?    | ORM tool that maps C# classes to database tables  |
| What are Migrations?         | Auto-generated files that sync code with database |
| What is DbContext?           | Class that manages database connection            |
| What is DbSet?               | Represents a database table                       |
| Code-First approach kya hai? | Database generate hota hai model se               |
| LINQ kya karta hai?          | C# queries ko SQL me convert karta hai            |

---

## 🚀 Summary (One Table Recap)

| Concept          | Meaning                      |
| ---------------- | ---------------------------- |
| Entity Framework | ORM for connecting C# & SQL  |
| Model Class      | Blueprint for table          |
| DbContext        | Bridge between app & DB      |
| Migration        | Converts model to SQL        |
| LINQ             | C# based query language      |
| CRUD             | Create, Read, Update, Delete |

---

## 💬 Short Viva Answer

> “Entity Framework ek ORM tool hai jo C# classes ko database tables me map karta hai.
> Code-First approach me hum model class likhte hain, DbContext se connect karte hain,
> aur migrations run karke automatic database create karte hain.”

---

## 🌟 Bonus Tip (Pro Level)

Use this command to drop & recreate DB cleanly:

```bash
Drop-Database
Add-Migration Recreate
Update-Database
```

---

🧩 **Now you officially understand Entity Framework — Scratch → Pro.**

# 🔗 Entity Framework Relationships (Scratch → Pro)

---

## 💡 What Are Relationships?

Entity Framework me **relationships** ka matlab hota hai —  
**2 ya zyada tables ke beech connection** banana.

Example:
- Ek user ke multiple posts ho sakte hain
- Ek student ka ek hi address ho sakta hai

EF in relationships ko **navigation properties** ke through handle karta hai.

---

## 🧩 3 Types of Relationships

| Type | Name | Meaning |
|------|------|----------|
| 1️⃣ | One-to-One (1:1) | Ek record sirf ek se linked |
| 2️⃣ | One-to-Many (1:N) | Ek record multiple records se linked |
| 3️⃣ | Many-to-Many (M:N) | Multiple records multiple se linked |

---

## 🧠 1️⃣ One-to-One Relationship

### 💬 Example:
Ek **User** ka ek **Profile** hai.

### 🏗️ Model Classes

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }

    public Profile Profile { get; set; } // Navigation property
}

public class Profile
{
    public int Id { get; set; }
    public string Bio { get; set; }

    public int UserId { get; set; }      // Foreign Key
    public User User { get; set; }       // Navigation property
}
````

---

### 🧩 Explanation:

| Property            | Meaning                 |
| ------------------- | ----------------------- |
| `Profile` in User   | One profile per user    |
| `UserId` in Profile | Foreign Key for linking |
| `User` in Profile   | Reverse navigation      |

---

### ⚙️ Configuration (Optional Fluent API)

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<User>()
        .HasOne(u => u.Profile)
        .WithOne(p => p.User)
        .HasForeignKey<Profile>(p => p.UserId);
}
```

🧠 **Result:**
EF SQL me 2 tables banayega → `Users` & `Profiles`
`Profiles` table me `UserId` as foreign key hoga.

---

## 🧠 2️⃣ One-to-Many Relationship

### 💬 Example:

Ek **Category** ke multiple **Products** ho sakte hain.

---

### 🏗️ Model Classes

```csharp
public class Category
{
    public int Id { get; set; }
    public string Name { get; set; }

    public List<Product> Products { get; set; } // One-to-Many
}

public class Product
{
    public int Id { get; set; }
    public string ProductName { get; set; }

    public int CategoryId { get; set; }  // Foreign Key
    public Category Category { get; set; } // Navigation property
}
```

---

### 🧩 Explanation:

| Concept              | Description                      |
| -------------------- | -------------------------------- |
| `Category.Products`  | One category → multiple products |
| `Product.CategoryId` | Foreign key                      |
| `Product.Category`   | Reverse navigation               |

---

### ⚙️ SQL Side:

EF automatically `CategoryId` foreign key column create karega in Products table.

---

### 🔥 Example Query:

```csharp
// Add category with products
var category = new Category
{
    Name = "Toys",
    Products = new List<Product>
    {
        new Product { ProductName = "Teddy Bear" },
        new Product { ProductName = "Toy Car" }
    }
};
_context.Categories.Add(category);
_context.SaveChanges();
```

---

## 🧠 3️⃣ Many-to-Many Relationship

### 💬 Example:

Ek **Student** ke multiple **Courses**, aur ek **Course** me multiple **Students** ho sakte hain.

---

### 🏗️ Model Classes (EF Core 5+)

```csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }

    public List<Course> Courses { get; set; }
}

public class Course
{
    public int Id { get; set; }
    public string Title { get; set; }

    public List<Student> Students { get; set; }
}
```

---

### ⚙️ EF Automatically Creates a Join Table:

```
StudentCourses
---------------
StudentId (FK)
CourseId  (FK)
```

Tumhe manually join table banane ki zarurat nahi hai
(ye EF Core 5+ ka best feature hai).

---

### 🔥 Example Query:

```csharp
var student = new Student { Name = "Wania" };
var course = new Course { Title = "Web Development" };

student.Courses = new List<Course> { course };
_context.Students.Add(student);
_context.SaveChanges();
```

🧠 EF automatically StudentCourses join table me entry karega.

---

## ⚡ Summary Table

| Type         | Example             | SQL Result                 |
| ------------ | ------------------- | -------------------------- |
| One-to-One   | User ↔ Profile      | 2 Tables, 1 FK             |
| One-to-Many  | Category → Products | 2 Tables, FK in Many side  |
| Many-to-Many | Students ↔ Courses  | 3 Tables (auto join table) |

---

## 🧠 Interview / Viva Q&A

| Question                     | Short Answer                                                 |
| ---------------------------- | ------------------------------------------------------------ |
| What are EF relationships?   | Links between two or more tables using navigation properties |
| How is 1:1 implemented?      | `HasOne().WithOne()` + FK                                    |
| How is 1:N implemented?      | `HasMany().WithOne()`                                        |
| How is M:N implemented?      | Lists on both sides; EF auto creates join table              |
| What is navigation property? | Property that defines relation between entities              |
| What is foreign key?         | Column that links one table to another                       |

---

## 🧩 Pro Level: Fluent API Cheat Sheet

```csharp
// One-to-One
modelBuilder.Entity<User>()
    .HasOne(u => u.Profile)
    .WithOne(p => p.User)
    .HasForeignKey<Profile>(p => p.UserId);

// One-to-Many
modelBuilder.Entity<Category>()
    .HasMany(c => c.Products)
    .WithOne(p => p.Category)
    .HasForeignKey(p => p.CategoryId);

// Many-to-Many
modelBuilder.Entity<Student>()
    .HasMany(s => s.Courses)
    .WithMany(c => c.Students);
```

---

## 💬 Short Viva Answer

> “Relationships in Entity Framework define how tables connect.
>
> One-to-One links one record to one,
> One-to-Many links one record to many,
> and Many-to-Many connects multiple records on both sides.”

---

## 🏁 Quick Recap

| Concept             | Definition               |
| ------------------- | ------------------------ |
| Relationship        | Link between tables      |
| Navigation Property | Used to define relation  |
| Foreign Key         | Column that links tables |
| One-to-One          | User ↔ Profile           |
| One-to-Many         | Category → Products      |
| Many-to-Many        | Students ↔ Courses       |

---

✅ **You’ve officially mastered Entity Framework Relationships — Scratch → Pro!**

# ⚙️ Entity Framework Migrations — Scratch → Pro

---

## 💡 What Are Migrations?

Migrations ka matlab hota hai  
**C# code se SQL database update karna automatically** —  
matlab manually table banana, alter karna, ya update karna ki zarurat nahi.

Entity Framework khud ye sab handle karta hai.

---

## 🧩 Simple Line Me

> “Migration is a feature of Entity Framework that **syncs your model classes with the database schema**.”

Jab tum apne model me koi nayi property add karti ho (like `PhoneNumber`),  
to migration run karke EF database me wo column automatically add kar deta hai.

---

## 🧱 How Migration Works (Step-by-Step)

```

Model Class (C#)
↓
Migration Command
↓
Migration Files Generated
↓
Database Updated (SQL)

````

---

## 🧩 Required Packages

Ensure these are installed:
```bash
Microsoft.EntityFrameworkCore
Microsoft.EntityFrameworkCore.SqlServer
Microsoft.EntityFrameworkCore.Tools
````

---

## ⚙️ Step-by-Step Migration Commands

| Step | Command                       | Description                                         |
| ---- | ----------------------------- | --------------------------------------------------- |
| 1️⃣  | `Add-Migration InitialCreate` | Creates a migration file based on your model        |
| 2️⃣  | `Update-Database`             | Applies migration to your database (creates tables) |
| 3️⃣  | `Add-Migration AddAgeColumn`  | Creates migration for new model changes             |
| 4️⃣  | `Update-Database`             | Applies those new changes to database               |
| 5️⃣  | `Remove-Migration`            | Deletes last migration (if not applied yet)         |
| 6️⃣  | `Drop-Database`               | Deletes full database                               |

---

## 🧠 Example Walkthrough

### Step 1️⃣ — Create Model

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

### Step 2️⃣ — Add Migration

```bash
Add-Migration InitialCreate
```

📁 EF automatically creates a folder `/Migrations` with:

* `20251107_InitialCreate.cs`
* `AppDbContextModelSnapshot.cs`

---

### Step 3️⃣ — Apply to Database

```bash
Update-Database
```

💾 Result: SQL Database me `Users` table ban jayegi.

---

## 🧩 Example: Add New Property

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; } // new property
}
```

### Run Commands Again:

```bash
Add-Migration AddEmailColumn
Update-Database
```

🧠 EF automatically `ALTER TABLE` run karega aur `Email` column add karega.

---

## 📂 Migration Files Explained

Migration file ke andar 2 main methods hote hain:

```csharp
protected override void Up(MigrationBuilder migrationBuilder)
{
    // Changes to apply (create table, add column)
}

protected override void Down(MigrationBuilder migrationBuilder)
{
    // Rollback changes (drop table, remove column)
}
```

---

## 🧱 Folder Structure Example

```
📁 MyApp
 ┣ 📂 Models
 ┃ ┣ User.cs
 ┃ ┗ AppDbContext.cs
 ┣ 📂 Migrations
 ┃ ┣ 20251107_InitialCreate.cs
 ┃ ┗ AppDbContextModelSnapshot.cs
 ┣ appsettings.json
 ┗ Program.cs
```

---

## ⚡ Common Migration Errors + Fixes

| Error                        | Cause                                      | Fix                                                                      |
| ---------------------------- | ------------------------------------------ | ------------------------------------------------------------------------ |
| ❌ “No DbContext found”       | DbContext class not registered properly    | Ensure in `Program.cs` → `builder.Services.AddDbContext<AppDbContext>()` |
| ❌ “Cannot create database”   | Wrong connection string                    | Check `appsettings.json` for valid SQL Server name                       |
| ❌ “Pending changes detected” | You changed model but didn’t run migration | Run `Add-Migration` + `Update-Database`                                  |
| ❌ “Model snapshot conflicts” | Deleted migration manually                 | Delete `Migrations` folder and start fresh                               |
| ❌ “Timeout expired”          | SQL Server not running                     | Restart SQL Server service                                               |

---

## ⚙️ Connection Example (appsettings.json)

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=DESKTOP-1234\\SQLEXPRESS;Database=MyAppDB;Trusted_Connection=True;"
  }
}
```

and in `Program.cs` 👇

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

---

## 🧠 Entity Framework Code-First Lifecycle

| Step | Description        |
| ---- | ------------------ |
| 1️⃣  | Create Model Class |
| 2️⃣  | Add DbContext      |
| 3️⃣  | Add Migration      |
| 4️⃣  | Update Database    |
| 5️⃣  | CRUD Operations    |

---

## 💬 Example Viva / Interview Line

> “Entity Framework Migration helps keep the database and code in sync.
> Whenever the model changes, we create a new migration and update the database using `Add-Migration` and `Update-Database` commands.”

---

## 🧩 Shortcut Recap (Pro View)

```
# First Migration
Add-Migration InitialCreate
Update-Database

# Update Model
Add-Migration AddedEmailColumn
Update-Database

# Rollback
Remove-Migration
```

---

## 🧠 Pro Tip

If something breaks badly 👇

```
Drop-Database
Remove-Migration
Add-Migration RebuildAll
Update-Database
```

It resets everything cleanly.

---

## ✅ Summary

| Concept         | Definition                                 |
| --------------- | ------------------------------------------ |
| Migration       | Syncs model → database                     |
| Add-Migration   | Generates SQL changes                      |
| Update-Database | Applies changes                            |
| Up()            | Apply changes                              |
| Down()          | Revert changes                             |
| Folder          | `/Migrations` stores all migration history |

---

## 🎯 Final Short Answer (Exam/Interview)

> “Migration in Entity Framework is the process of **creating and updating database schema** based on model changes, without writing SQL manually.”

---

## 🏁 You’re now Entity Framework Migrations PRO 💥

```

---
