
# 💎 .NET MVC — Model Full Guide

## 💎 LESSON 1 — Model Kya Hota Hai (.NET MVC Me)

### 🧠 Simple Meaning:
Model basically **data ka brain** hai.  
App me jitna bhi data aata ya jata hai — sabka center **Model** hota hai.

### 🧩 Model Ka Role:

| Kaam | Explanation |
|------|--------------|
| 1️⃣ Data Store | App ka data represent karta hai (e.g., Users, Products, Orders) |
| 2️⃣ Database Link | SQL Server ya kisi DB ke sath link hota hai |
| 3️⃣ Business Logic | Data ke rules aur calculations rakhta hai (like price * quantity) |

### 🏗️ MVC Me Model Ka Place:
```
User ↔ Controller ↔ Model ↔ Database
```

**Flow:**
- User → request bhejta hai  
- Controller → request handle karta hai  
- Model → data handle karta hai (DB se fetch ya save karta hai)  
- Database → actual data store karta hai

---

## 💎 LESSON 2 — Model Me Kya Files Hoti Hain?

Model folder me tum yeh 3 type ki files bana sakti ho 👇

| File Type | Example | Kaam |
|------------|----------|------|
| 1️⃣ Model Class | User.cs | data define karta (Name, Age, Email) |
| 2️⃣ DbContext Class | AppDbContext.cs | DB connection aur tables manage karta |
| 3️⃣ Migration Files | auto-generate hoti hain | DB me tables create/update karti hain |

---

## 💎 LESSON 3 — Model Class (Basic Example)

```csharp
public class User
{
    public int Id { get; set; }     // Primary key
    public string Name { get; set; }
    public int Age { get; set; }
    public string Email { get; set; }
}
```

🪄 Ye class SQL me “Users” table banne ka base hoti hai.

---

## 💎 LESSON 4 — Entity Framework (ORM)

### 💬 Entity Framework (EF) kya hai?
Entity Framework ek **ORM (Object Relational Mapper)** hai.  
Matlab — tum C# code se directly database ke sath kaam kar sakti ho **without writing SQL queries manually**.

🧠 Simple Line Me:
> “Entity Framework data ko C# objects me convert karta hai, aur phir unhe database me save/fetch karta hai.”

### 💾 Types of Entity Framework:

| Type | Use |
|-------|-----|
| EF 6 (Old) | .NET Framework projects ke liye |
| EF Core (Latest) ✅ | .NET 5, 6, 7, 8 ke liye (use ye hi karte hain) |

👉 Tumhe **Entity Framework Core** use karna chahiye — kyunki ye modern aur cross-platform hai.

---

## 💎 LESSON 5 — Entity Framework Core Install

### 📦 Step 1: Install Package (NuGet)

Visual Studio me jao → Tools → NuGet Package Manager → Package Manager Console me likho:

```
Install-Package Microsoft.EntityFrameworkCore.SqlServer
Install-Package Microsoft.EntityFrameworkCore.Tools
```

---

## 💎 LESSON 6 — Create DbContext Class

### 📄 Example: AppDbContext.cs

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options)
    {
    }

    public DbSet<User> Users { get; set; }
}
```

🧠 “DbSet<User>” ka matlab — ek “Users” table database me create hoga.

---

## 💎 LESSON 7 — Connection String (Database Link)

**appsettings.json** me likho:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=YOUR_SERVER_NAME;Database=MyAppDB;Trusted_Connection=True;TrustServerCertificate=True;"
}
```

**Program.cs** me likho:

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

---

## 💎 LESSON 8 — Migrations (Database Create Karna)

Migration se tumhara model database me convert hota hai 👇

```
Add-Migration InitialCreate
Update-Database
```

🪄 Ye 2 commands:
- **Add-Migration** → Model → SQL table bana deta hai (script ready karta hai)  
- **Update-Database** → us script ko run karke SQL Server me table create karta hai

---

## 💎 LESSON 9 — Final Flow

```
User.cs (Model) 
     ↓
AppDbContext.cs (DbContext)
     ↓
Migration → SQL Server (DB Table)
```

---

## 💎 LESSON 10 — Practical Example (Full Setup)

### // User.cs
```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}
```

### // AppDbContext.cs
```csharp
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }
    public DbSet<User> Users { get; set; }
}
```

---

## 🧠 Summary Table

| Concept | Explanation |
|----------|-------------|
| Model | Data class (represents database table) |
| DbContext | Bridge between C# & Database |
| Entity Framework | ORM that automates SQL |
| Migration | Creates/updates tables |
| EF Core | Latest version used in .NET Core |
