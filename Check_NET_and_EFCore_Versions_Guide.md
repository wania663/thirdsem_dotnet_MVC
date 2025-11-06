
# 💎 Check .NET and EF Core Versions — Step-by-Step Guide

## 🧩 STEP 1 — Check Your .NET Version

### Option 1: From Visual Studio

1️⃣ In **Solution Explorer**, right-click your project name  
2️⃣ Click **Properties**  
3️⃣ Go to the **Application** tab on the left side  
4️⃣ At the bottom, you’ll see something like:

```
Target Framework: .NET 6 / .NET 7 / .NET 8
```

👉 That’s your **.NET version**.

---

### Option 2: From Terminal (Faster Way)

Open your project folder and type:

```
dotnet --version
```

**Example Output:**

```
8.0.101
```

✅ This means you are using **.NET 8**.

---

## 💎 STEP 2 — Check Installed EF Core Version

In **Visual Studio Package Manager Console**, type:

```
Get-Package Microsoft.EntityFrameworkCore
```

**Example Output:**

```
Id: Microsoft.EntityFrameworkCore
Version: 8.0.0
```

👉 This means **EF Core 8** is installed.

---

## 💎 STEP 3 — Compatibility Table

| .NET Version | Compatible EF Core |
|---------------|--------------------|
| .NET 5 | EF Core 5 |
| .NET 6 | EF Core 6 |
| .NET 7 | EF Core 7 |
| .NET 8 ✅ | EF Core 8 ✅ |

💬 If both versions match (for example, .NET 8 + EF Core 8), your setup is **perfect**.

---

## 💡 BONUS TIP

If you ever suspect a version mismatch, you can **update EF Core** easily:

```
Update-Package Microsoft.EntityFrameworkCore
Update-Package Microsoft.EntityFrameworkCore.Tools
```

These commands will update to the **latest compatible versions** 💪
